# Finance Econometrics – OSEAX Return Analysis

Econometric analysis of the Oslo Stock Exchange All-Share Index (OSEAX) using OLS regression, diagnostic testing, and ARIMA modelling. Monthly data from 2014 to 2024.

## Research Question

What macroeconomic and global market factors explain the monthly returns of the Norwegian stock market (OSEAX)?

## Data

All data downloaded via Yahoo Finance at monthly frequency (last observation per month).

| Variable | Ticker | Description |
|---|---|---|
| OSEAX return | `^OSEAX` | Dependent variable – Oslo Stock Exchange All-Share Index |
| Oil return | `BZ=F` | Brent Crude Oil Futures |
| FTSE 100 return | `^FTSE` | London Stock Exchange benchmark |
| S&P 500 return | `^GSPC` | US equity market benchmark |
| Interest rate change | `^TNX` | US 10-Year Government Bond Yield (proxy) |

All price series are converted to **log returns**. Interest rate is expressed as **first difference**.

## Methodology

### 1. Exploratory Data Analysis
- Descriptive statistics (mean, std, skewness, kurtosis)
- Correlation matrix and heatmap
- Price level and return time series plots
- Return distribution histograms vs. normal curve

### 2. OLS Regression
```
ose_ret = α + β₁·oil_ret + β₂·ftse_ret + β₃·sp500_ret + β₄·rate_change + ε
```

### 3. Diagnostic Tests

| Test | Purpose |
|---|---|
| Jarque–Bera | Normality of residuals |
| Durbin–Watson | First-order serial correlation |
| Ljung–Box (lag 12) | Higher-order serial correlation |
| Breusch–Pagan | Heteroskedasticity |
| White Test | General heteroskedasticity |
| VIF | Multicollinearity |

### 4. Model Correction
- HC0 heteroskedasticity-robust standard errors

### 5. ARIMA on Residuals
- ACF/PACF plots for lag selection
- AIC-based grid search over ARMA(p,q) for p,q ∈ {0,1,2,3}
- Final model: **ARIMA(1,0,1)**

## Project Structure

```
finance-econometrics-oseax/
├── IndividualProject_code_base.ipynb   # Full analysis notebook
└── README.md
```

## Requirements

```bash
pip install yfinance pandas numpy scipy statsmodels matplotlib seaborn tabulate
```

## Author

Huong Giang Tran — MSc Finance, University College Dublin (2024–2025)
