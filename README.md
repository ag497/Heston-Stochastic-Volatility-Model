# Heston-Stochastic-Volatility-Model
This repository is dedicated to implementing and exploring the Heston stochastic volatility model using stochastic process for modeling asset and derivative prices. It allows for the volatility of the underlying asset to fluctuate stochastically over time, addressing a key limitation of simpler models like the Black-Scholes model.
# Heston Option Pricing Model

The Heston Option Pricing Model is a type of stochastic volatility model. Stochastic volatility models assume that both the underlying asset price and its variance follow stochastic processes. This contrasts with the Black-Scholes model, which incorrectly assumes constant implied volatility of the underlying asset. In reality, volatility changes over time, especially during periods of market stress, resulting in varying implied volatilities across different strike prices and option maturities.

Moreover, historical returns typically exhibit fatter tails than assumed by the normal distribution used in the Black-Scholes model, indicating a greater probability of extreme negative returns. To address these issues, stochastic volatility models like the Heston Model treat the variance of the asset price as a stochastic process.

The Heston Option Pricing Model provides a more realistic framework for pricing options by accounting for the stochastic nature of both asset price and its volatility. This makes it a valuable tool in financial modeling and risk management, particularly in volatile markets where constant volatility assumptions fail to capture market dynamics effectively.

## Key Features of the Heston Model

1. **Stochastic Processes**: The Heston Model assumes that both asset price and its variance follow stochastic processes.
   
2. **Correlation**: There exists negative correlation between asset price and its variance.
   
3. **Mean-Reverting Variance**: The variance process follows a mean-reverting stochastic process, specifically modeled using the CIR (Cox-Ingersoll-Ross) process. This reflects the empirical observation that volatility tends to return to its average level over time.

4. **Asset Price Dynamics**: The asset price follows a Geometric Brownian Motion (GBM), a common assumption in option pricing models.

## Empirical Observations and Motivations

Empirical observations, particularly on indices like the S&P 500, show that periods of high volatility are often followed by continued high volatility, while low volatility periods tend to persist. This supports the mean-reverting nature of volatility assumed by the Heston Model.

Additionally, there is a negative correlation between volatility changes and asset returns in general. Higher volatility tends to be associated with negative asset returns due to factors like risk aversion and the leverage effect.

## Brief Introduction To Heston Model Maths
Under real world probability P:

dS(t) = μ S(t) dt + √(v(t)) S(t) dW₁(t) (GBM model)

dv(t) = κ(θ - v(t)) dt + σ √(v(t)) dW₂(t) (CIR model)

dW₁(t)×dW₂(t)= ρ × dt

S(t), v(t) are underlying asset price and instantaneous variance at time t respectively

(√(v(t))) is instantaneous volatility

κ is speed of mean reversion (velocity at which process will return to its mean) 

θ is long term mean of variance 

σ is volatility of variance 

dW₁(t ), dW₂(t) are Weiner processes under probability p representing the randomness(stochasticity) of asset price and variance respectively

ρ is the correlation between dW₁(t ) and dW₂(t) (negative for stocks usually)

Feller’s Condition:  2κθ>σ ^2 is a condition for non-negativeness of variance over time to get stable solution for PDE

Let v(0) be initial variance
v(0) and θ control volatility of asset return while σ controls the kurtosis of its distribution accounting for thicker tails ( i.e. extreme movements) when its value is higher
ρ controls the skewness of the distribution (asymmetry) with a negative value of ρ increasing probability of having negative returns
This solves the problem of the BM model and is closer to real world behaviour
Note that basically what we are doing is dealing with higher order central moments to better explain the behaviour of asset returns and model it
Also, A higher κ indicates that volatility changes are  short-lived, while a lower κ suggests that volatility changes persist for longer periods

Since, we cannot estimate our p probabilities in advance we use q probabilities(risk neutral probabilities) for no arbitrage pricing instead to price our asset(this makes our discounted asset price a martingale):

dS(t) = r S(t) dt + √(v(t)) S(t) dW’₁(t) (GBM model)

dv(t) = κ’(θ ‘- λ dt + σ √(v(t)) dW₂’(t) (CIR model)

dW₁’(t)×dW₂’(t)= ρ × dt

k’=k+ λ

θ ‘=k θ /(k+ λ)

dW’₁(t)= dW₁(t)+ (μ-r/√(v(t)))*dt (to shift between real world probability p and risk neutral probability q)

dW₂’(t)= dW₂(t)+ (λ v(t)/ σ (v(t)))*dt(to shift between real world probability p and risk neutral probability q)

S(t), v(t) are underlying asset price and instantaneous variance at time t respectively, (√(v(t))) is instantaneous volatility

r is risk-free interest rate 

κ’ is speed of mean reversion (velocity at which process will return to its mean) under q

θ’ is long term mean of variance under q

σ is volatility of variance 

dW₁’(t ), dW₂’(t) are Weiner processes under probability q representing the randomness(stochasticity) of asset price and variance respectively

ρ is the correlation between dW₁’(t ) and dW₂’(t) (negative for stocks usually)

λ is variance risk premium (additional compensation for holding volatility risk)

(λ v(t)/ σ (v(t))) is market price of volatility risk taken on by the investor

Using Girsanov’s theorem(when extend to 2 dimensions), it is proved that q probability exists but not unique

## Idea Behind Option Pricing with Heston

The price of a call option is a function of the 5 parameters (v(0), κ’, θ’, σ, ρ).

The parameters implied by option prices can be determined by the argument that minimises the pricing error between model prices and market prices( found by options with different strikes and time to maturity).

The Heston model is a widely used stochastic volatility model in finance, particularly in option pricing. Its characteristic function plays a crucial role in understanding the dynamics of asset prices under the model.

## Heston Characteristic Function Brief Introduction

The intuition behind the characteristic function in the Heston model lies in its ability to capture the joint distribution of the asset price and its volatility. 

In the Heston model, the asset price follows a stochastic process, typically modeled as a geometric Brownian motion, while the volatility follows a separate stochastic process, often modeled as a mean-reverting process.

The characteristic function encapsulates the entire distribution of the asset price at a given time, given its initial value, volatility, and other parameters of the model. 

It allows for the calculation of option prices and other financial derivatives by integrating over the entire distribution of possible asset prices.

One key advantage of using characteristic functions in the context of the Heston model is that they can often be expressed analytically, facilitating efficient computation of option prices through Fourier inversion techniques. 

This analytical tractability is a significant advantage compared to alternative methods, such as Monte Carlo simulation, especially when pricing complex derivatives or performing risk management calculations in real-time.

## Heston In Detail

## Stochastic Volatility Equation Derivation 
Ornstein-Uhlenbeck Process (used to derive stochastic variance equation of Heston) aka Mean Reverting Process

dh(t) = -βh(t)dt + σdW(t )

V = h(t)²

Applying Ito's Lemma to Ornstein Uhlenbeck Process,

∂V / ∂t = 0 as variance is a function of h(t)

∂V / ∂h(t) = 2h(t)

∂²V / ∂h(t)² = 2

μ=-βh(t)

σ=𝛿

dV = ( 𝛿² - 2βV) dt + (2𝛿√V) dW(t)

Use k=2β, θ=𝛿²/2β , σ=2𝛿

dV = κ(θ - V)dt + (σ√V)dWt

Hence derived stochastic volatility equation in P measure (real world probability)

## Risk Neutral Valuation Equations Derivation
The equations are in p-measure, so to price appropriately, we need to convert them to q-measure probabilities.

To do so we need to convert the asset into a martingale aka make it driftless (μ=0)

## Girsanov's Theorem
Use Girsanov's Theorem to convert our equations from P probability measure to Q probability measure

W^P + at = W^Q

dW^P + adt = dW^Q

Applying to GBM Equation in P measure:

dS(t) = (μ-r) S(t) dt + σ S(t) dW^P (t)

dS(t) = (μ-r) S(t) dt + σ S(t) (dW^Q (t) - adt)

dS(t) = (μ-r-aσ) S(t) dt + σ S(t) dW^Q (t)

For it to be a martingale drift term should be 0:

(μ-r-aσ)=0 or a=μ-r/σ

dS(t) =  σ S(t) dW^Q (t)

W^P + (μ-r/σ) t = W^Q

So our final Heston Model Equations under risk neutral valuation would be:

dS(t) = μ S(t) dt + √v S(t) dW^Q (t)

μ=r (expected rate of return in q measure is riskfree IR)

dS(t) = r S(t) dt + √v S(t) dW^Q (t)

dv(t) = (k(θ - v(t)) dt+ σ √v dW^P (t) (under p measure)

dv(t) = (k(θ - v(t) - λ) dt+ σ √v dW^Q (t) (when tranformed t under q measure)

k* = k + λ

θ* = (θ * k) / (k + λ)

dv(t) = (k*(θ* - v(t)) dt+ σ √v dW^Q (t)

λ is called the volatility risk premium term

## CIR Model for Variance Process In Brief
dv(t) = a (b - r(t)) dt + σ √(r(t))dW(t)

where a is speed of mean reversion and b is long term mean

a and b analogous to k and θ respectively

## Cholesky Decomposition
Cholesky Decomposition Matrix is used to convert correlated Brownian Motions into Independent Brownian Motions

A Positive Definite Matrix (PDM)  has unique factorisation C = L L^T where L is lower triangular matrix with positive diagonal values

This factorisation is called Cholesky Decomposition

W=L*Z

W is correlated (dependent) Brownian Motion Matrix 

W^T = [ W1(t) , W2(t) ]

Z is independent Brownian Motion Matrix 

Z^T = [Z1(t) , Z2(t) ]

W1(t) = Z1(t)

W2(t) = ρ(1,2) Z1(t) + √ (1-ρ(1,2)^2) Z2(t)

This helps deal with multidimensional asset pricing processes like with Heston Model

cov[W1(t), W2(t)] = E[W1(t) W2(t)] - E[W1(t)] E[W2(t]

= E[ Z1(t) (ρ(1,2) Z1(t) + √ (1-ρ(1,2)^2) Z2(t)) ] - 0

because E[W1(t)] = 0 and  E[W2(t] = 0 

= ρ(1,2) E[ Z1(t)^2 ] + √ (1-ρ(1,2)^2) E[ Z1(t)] E[Z2(t)]
​
= ρ(1,2) E[ Z1(t)^2 ] + 0

because E[Z1(t)] = 0 and  E[Z2(t] = 0 

= ρ(1,2) var[Z1(t)]

cov[W1(t), W2(t)] = ρ(1,2) t

σ̅(t,X(t))  is correlation matrix structure. Instantaneous covariance matrix representing correlation between 
the Brownian Motions via Cholesky Decomposition.

(L dZ(t)) (L dZ(t))^T = (L dZ(t) dZ(t)^T L^T)

= (σ̅(t,X(t)),σ̅(t,X(t))^T) diag(dt)

beacuse Z(t) dZ(t)^T = diag(dt)

(L dZ(t)) (L dZ(t))^T = Cdt

 Every C has unique Cholesky Decomposition  aka factorization of the form LL^T
 
## FOR CORRELATED BROWNIAN SDE
dX=μ̅ dt+ ∑̅ dW

## FOR INDEPENDENT BROWNIAN SDE
dX=μ̅ dt+ ∑̅  LdZ

dX=μ̅ dt+ ∑̅  σ̅ dZ

## ITO'S LEMMA For  Vector Process
 X(t)=[ X1(t) X2(t) X3(t) X4(t) .... Xn(t)]
 
 g = g(t,X(t))
 
 dg(t,X(t)) = (∂g / ∂t) dt + ∑{j=1 to n}
 (∂g / ∂Xj) dXj(t) + 1/2 ∑{i,j=1 to n}
 (∂²g / ∂Xi ∂Xj) dXi(t) dXj(t)

distinguishing for μ̅  and σ̅  :

(∂g / ∂t + ∑{i=1 to n} μ̅ i(t,X(t))
 (∂g / ∂Xi) + 1/2 ∑{i,j,k=1 to n} σ̅ i,k(t,X(t)) σ̅ j,k(t,X(t))
 (∂²g / ∂Xi ∂Xj)) dt + ∑{i,j =1 to n} σ̅ i,j(t,X(t) (∂g / ∂Xi) dZj(t)


 ## HESTON PRICING PDE 
 ### Using Martingale Method
 


