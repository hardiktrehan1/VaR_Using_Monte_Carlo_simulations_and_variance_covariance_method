## Value at Risk (VaR) Modeling for Stock Portfolio
This project implements and compares two standard approaches to calculate Value at Risk (VaR) for a portfolio of financial stocks: Monte Carlo Simulation and Variance-Covariance Method.

**Portfolio Composition**

The portfolio consists of the following four stocks:
- JPMorgan Chase (JPM)
- Goldman Sachs (GS)
- BNY Mellon (BK)
- HSBC Holdings (HSBC)

The stock weights are adjustable and represent the proportion of the total investment allocated to each asset.

**1. Monte Carlo Simulation-Based VaR**

**Overview**

- Monte Carlo simulation estimates potential future losses by generating a large number of hypothetical return scenarios based on the historical distribution and correlation of asset returns.

**Steps Involved**

- Fetch Historical Data
- Daily adjusted closing prices are downloaded using yfinance for each asset.
- Calculate Log Returns
- Logarithmic daily returns are computed to model asset price changes.
- Estimate Mean and Covariance
- The average return and covariance matrix are calculated from historical returns.
- Apply Cholesky Decomposition
- The covariance matrix is decomposed using Cholesky decomposition to generate correlated random returns.
- Simulate Returns
- A large number of normally distributed random returns are generated and transformed using the Cholesky matrix to match the real correlation structure.
- Construct Portfolio Returns
- Portfolio returns are calculated for each simulation by taking the dot product of simulated returns with portfolio weights.
- Calculate VaR
- VaR at 99%, 95% and 90% confidence is calculated as the percentile of losses.


**2. Variance-Covariance Method (Parametric VaR)**

**Overview**

- This analytical method assumes returns are normally distributed and uses the portfolio’s mean and standard deviation to directly calculate VaR.

**Steps Involved**

- Fetch and Prepare Data
- Historical stock prices and log returns are computed.
- Compute Covariance Matrix
- The sample covariance matrix is used to capture relationships between asset returns.
- Calculate Portfolio Variance 
- Calculate Portfolio Standard Deviation
- The square root of the variance gives the standard deviation.
- Compute Daily Portfolio Return
- Weighted average of individual asset returns.
- Calculate Parametric VaR using **VaR = - (portfolio_mean - z_score * portfolio_std)**
- where z-score corresponds to the desired confidence level (e.g., 1.65 for 95%).

**Comparison**

**Monte Carlo Simulation**

- Assumes normality of shocks, but is otherwise distribution-free
- Captures asset correlations using Cholesky decomposition
- Highly flexible — supports non-linear portfolios and custom return behavior
- Computationally intensive due to large number of simulations
- Suitable for portfolios with options or other path-dependent instruments

**Variance-Covariance Method**

- Assumes returns are normally distributed
- Captures asset correlations using the covariance matrix
- Moderately flexible — best suited for linear portfolios
- Much faster to compute due to its closed-form formula
- Ideal for quick, approximate risk estimation in stable markets
