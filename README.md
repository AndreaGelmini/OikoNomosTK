# OikoNomosTK
[![Latest Stable Version](https://img.shields.io/packagist/v/AndreaGelmini/oikonomostk.svg?style=flat-square)](https://packagist.org/packages/AndreaGelmini/oikonomostk) [![Total Downloads](https://img.shields.io/packagist/dt/AndreaGelmini/oikonomostk.svg?style=flat-square)](https://packagist.org/packages/AndreaGelmini/oikonomostk) [![License](https://img.shields.io/packagist/l/AndreaGelmini/oikonomostk.svg?style=flat-square)](https://packagist.org/packages/AndreaGelmini/oikonomostk) 

A comprehensive PHP Toolkit for financial mathematics, micro/macroeconomic calculations, financial analysis, and forecasting.

OikoNomosTK aims to provide a robust and well-tested set of tools for developers needing to implement common formulas and models from finance and economics within their PHP applications.

## Key Features

* **Financial Mathematics:** Simple/Compound Interest, Annuities, Amortization Schedules (French, Italian, etc.), NPV, IRR, Bond Pricing basics.
* **Financial Statement Analysis:** Key Ratios (ROE, ROI, Liquidity, Leverage, Efficiency).
* **Investment & Portfolio:** Risk/Return calculations, CAPM, Performance Metrics (Sharpe, Treynor).
* **Microeconomics:** Consumer Theory (Utility, MRS), Producer Theory (Production Functions, Costs, MRTS), Market Structures (Perfect Competition, Monopoly profit maximization).
* **Macroeconomics:** National Accounts (GDP), IS-LM basics, AD-AS basics, Inflation, Growth Models (Solow basics).
* **Forecasting:** Moving Averages, Basic Exponential Smoothing, Simple Linear Regression.
* **Taxation:** Generic calculations for VAT, simple income tax. *(Note: Taxation is country-specific, this library provides general formulas)*.
* Built with precision in mind (recommends using BCMath).

## Installation

The recommended way to install OikoNomosTK is through [Composer](https://getcomposer.org/):

```bash
composer require oikonomos-tk/oikonomos-tk
```
## Basic Usage
```php
<?php

require 'vendor/autoload.php';

use OikoNomosTK\Finance\Basic\CompoundInterest;
use OikoNomosTK\Finance\Corporate\FinancialRatios;
use OikoNomosTK\Finance\InvestmentAppraisal; // Assuming NPV is here

// Example 1: Calculate Future Value (Compound Interest)
$principal = 1000;  // e.g., €1000
$annualRate = 0.05; // 5% annual rate
$years = 10;
// Ensure BCMath is enabled or use a library that handles precision
bcscale(10); // Set precision for BCMath

$futureValue = CompoundInterest::calculateFutureValue((string)$principal, (string)$annualRate, $years);
echo "Future Value: " . $futureValue . "\n"; // Output: Future Value: 1628.894627

// Example 2: Calculate ROE (Return on Equity)
$netIncome = '150000'; // From Income Statement
$shareholdersEquity = '1000000'; // From Balance Sheet

$roe = FinancialRatios::calculateROE($netIncome, $shareholdersEquity);
echo "ROE: " . bcmul($roe, '100', 2) . "%\n"; // Output: ROE: 15.00%

// Example 3: Calculate Net Present Value (NPV)
$initialInvestment = '-100000'; // Initial outflow
$cashFlows = ['30000', '40000', '50000', '60000']; // Cash flows for years 1-4
$discountRate = '0.10'; // 10% discount rate

$npv = InvestmentAppraisal::calculateNPV($initialInvestment, $cashFlows, $discountRate);
echo "NPV: " . $npv . "\n";

?>
```
*(Note: Examples assume usage of BCMath for precision, adjust according to your implementation).*

## Feature Status

This table highlights the status of key features. See Issues for detailed planning.
| Namespace                                  | Class                 | Function Name                 | Static | Use Case Example                                    | Status  |
| ------------------------------------------ | --------------------- | ----------------------------- | ------ | --------------------------------------------------- | ------- |
| OikoNomosTK\\Finance\\Basic                | CompoundInterest      | calculateFutureValue          | Yes    | Calculate investment growth over time               | Planned |
| OikoNomosTK\\Finance\\Basic                | Annuity               | calculatePresentValueOrdinary | Yes    | Value a series of future payments (e.g., loan)      | Planned |
| OikoNomosTK\\Finance\\Corporate            | Amortization          | calculateFrenchPayment        | Yes    | Determine fixed loan payment amount                 | Planned |
| OikoNomosTK\\Finance\\Corporate            | FinancialRatios       | calculateROE                  | Yes    | Assess company profitability relative to equity     | Planned |
| OikoNomosTK\\Finance\\Corporate            | FinancialRatios       | calculateCurrentRatio         | Yes    | Evaluate short-term liquidity                       | Planned |
| OikoNomosTK\\Finance\\Corporate            | InvestmentAppraisal   | calculateNPV                  | Yes    | Decide if an investment is worth its cost           | Planned |
| OikoNomosTK\\Finance\\Investments          | Models\\CAPM          | calculateExpectedReturn       | Yes    | Estimate required return for an asset's risk        | Planned |
| OikoNomosTK\\Finance\\Investments          | PerformanceIndicators | calculateSharpeRatio          | Yes    | Evaluate risk-adjusted investment performance       | Planned |
| OikoNomosTK\\Microeconomics                | ConsumerTheory        | calculateMRS                  | Yes    | Model consumer trade-offs between goods             | Planned |
| OikoNomosTK\\Microeconomics                | ProducerTheory        | calculateMarginalProduct      | Yes    | Analyze impact of adding one unit of input          | Planned |
| OikoNomosTK\\Microeconomics\\MarketStruct. | Monopoly              | findProfitMaximizingOutput    | Yes    | Determine optimal production level for a monopolist | Planned |
| OikoNomosTK\\Macroeconomics                | NationalAccounts      | calculateGDPExpenditure       | Yes    | Calculate Gross Domestic Product (expenditure)      | Planned |
| OikoNomosTK\\Macroeconomics                | NationalAccounts      | calculateInflationRateCPI     | Yes    | Measure the rate of price level increase            | Planned |
| OikoNomosTK\\Finance\\Forecasting          | MovingAverages        | calculateSMA                  | Yes    | Smooth out data fluctuations to identify trends     | Planned |
| OikoNomosTK\\Common                        | MathUtils             | preciseAdd                    | Yes    | Perform high-precision addition (e.g., currency)    | Planned |

## Contributing

Contributions are welcome! Whether it's reporting a bug, suggesting a feature, or submitting code, your help is appreciated.

**Bug Reports & Feature Requests:** Please use the [GitHub Issues](https://www.google.com/search?q=https://github.com/AndreaGelmini/oikonomostk/issues) tracker. Before creating a new issue, please check if a similar one already exists.

**Pull Requests:**

1.  **Fork** the repository on GitHub.
2.  **Clone** your fork locally (`git clone git@github.com:your-username/oikonomostk.git`).
3.  Create a **new branch** for your changes (`git checkout -b feature/your-feature-name` or `bugfix/issue-number`).
4.  Make your changes. Ensure you follow the existing coding style (e.g., PSR-12).
5.  **Add tests** for your changes in the `tests/` directory. Ensure all tests pass (`composer test` - _you'll need to set up PHPUnit_).
6.  **Commit** your changes with clear commit messages.
7.  **Push** your branch to your fork (`git push origin feature/your-feature-name`).
8.  Open a **Pull Request** on the main `oikonomostk` repository. Provide a clear description of your changes.

## License

This project is licensed under the **MIT License**. See the [LICENSE](https://www.google.com/search?q=MIT) file for details.

## Contact
If you have any questions or comments, please feel free to contact me at [github@andreagelmini.it](mailto:github@andreagelmini.it) or open a issue


## Donations
If you find this project useful, you can support my work with a donation:
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/X8X415RASI)