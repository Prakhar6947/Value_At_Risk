# Quantitative Market Risk & VaR Engine (C++)

A high-performance market risk and portfolio analytics engine developed in modern C++. This engine implements enterprise-grade risk metrics, including Value at Risk (VaR) and Expected Shortfall (CVaR), using multiple statistical methodologies. It leverages the **Eigen** library for optimized linear algebra (Cholesky decomposition) and **Boost.Math** for statistical distributions, concluding with Kupiec's binomial backtesting to validate model accuracy against historical portfolio drawdowns.

## 🚀 Key Features & Methodologies

*   **Historical Simulation:** Non-parametric VaR calculation based on empirical historical return distributions.
*   **Bootstrap Method:** Resampling with replacement to generate robust empirical distributions of portfolio returns.
*   **Variance-Covariance (Parametric) Method:** Analytical risk estimation utilizing portfolio mean and covariance matrices, assuming normally distributed asset returns.
*   **Monte Carlo Simulation:** Simulates thousands of correlated asset price paths. Utilizes **Cholesky decomposition** of the covariance matrix to generate correlated multivariate normal distributions.
*   **Expected Shortfall (CVaR):** Calculates the conditional tail expectation, measuring the average loss in the worst-case scenarios.
*   **Binomial Backtesting (Kupiec Test):** Statistically evaluates the proportion of failures (exceptions) against the chosen confidence interval to validate the predictive power of the VaR models.

## 🛠️ Technology Stack & Dependencies

*   **Language:** C++17
*   **Eigen3:** Used for high-speed matrix operations, vector manipulations, and `Eigen::LLT` for Cholesky decomposition.
*   **Boost C++ Libraries:**
    *   `Boost.Math`: For binomial and normal distribution evaluations.
    *   `Boost.Random`: Mersenne Twister and normal distribution generators for Monte Carlo paths.

## 🏗️ System Architecture

The core logic is heavily object-oriented, structured around three primary classes:

1.  **`Porfolio_object`**: Handles data ingestion, calculates daily asset returns, generates the portfolio mean vector, and computes the $N \times N$ covariance matrix.
2.  **`multi_random`**: An Eigen-backed random generator that maps standard uncorrelated normal variables into correlated multi-asset variables using the Cholesky factor ($L L^T = \Sigma$).
3.  **`VaR_object`**: Inherits from `Porfolio_object`. Contains the execution logic for the four risk models, sorts and aggregates simulated/historical paths to find confidence-level quantiles, and executes the binomial backtest.


## 📊 Usage & Data Formatting

### Input Data (`stock.txt`)
The engine requires historical price data to be placed in `stock.txt` in the root directory. 
*   **Format:** A space-separated matrix of floats/doubles without headers.
*   **Rows:** Consecutive trading days (historical data points).
*   **Columns:** Individual financial assets in the portfolio.
