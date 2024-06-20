# Heston-Stochastic-Volatility-Model
This repository is dedicated to implementing and exploring the Heston stochastic volatility model using stochastic process for modeling asset and derivative prices. It allows for the volatility of the underlying asset to fluctuate stochastically over time, addressing a key limitation of simpler models like the Black-Scholes model.
# Heston Option Pricing Model

The Heston Option Pricing Model is a type of stochastic volatility model. Stochastic volatility models assume that both the underlying asset price and its variance follow stochastic processes. This contrasts with the Black-Scholes model, which incorrectly assumes constant implied volatility of the underlying asset. In reality, volatility changes over time, especially during periods of market stress, resulting in varying implied volatilities across different strike prices and option maturities.

Moreover, historical returns typically exhibit fatter tails than assumed by the normal distribution used in the Black-Scholes model, indicating a greater probability of extreme negative returns. To address these issues, stochastic volatility models like the Heston Model treat the variance of the asset price as a stochastic process.

The Heston Option Pricing Model provides a more realistic framework for pricing options by accounting for the stochastic nature of both asset price and its volatility. This makes it a valuable tool in financial modeling and risk management, particularly in volatile markets where constant volatility assumptions fail to capture market dynamics effectively.

## Key Features of the Heston Model

1. **Stochastic Processes**: The Heston Model assumes that both asset price and its variance follow stochastic processes.
   
2. **Correlation**: There exists correlation between asset price and its variance.
   
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

Feller’s Condition:  2κθ>σ ^2 is a condition for non-negativeness of variance over time

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

