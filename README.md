# Monte Carlo Corporate Earnings Risk (C-VaR)

An Excel Monte Carlo model that measures how far a multinational firm's pre-tax earnings could fall short of expectations because of three risks: the EUR/USD exchange rate, aluminum input prices, and short-term interest rates. It then tests whether hedging one risk at a time reduces that downside. It follows the Corporate Value-at-Risk framework from the HBR case "Understanding Corporate-Value-at-Risk through a Comprehensive and Simple Example" and was built at UMass Boston.

## Key finding

Locking the aluminum price cut 95% C-VaR from 8.89% to 3.04% of benchmark earnings, a drop of about 65%. Locking the EUR/USD rate only moved it to 8.14%. For this firm, input cost volatility drives most of the tail risk, so the report recommends hedging the dominant exposure instead of hedging everything.

## Results

| Scenario | 95% C-VaR ($K) | % of benchmark | Change vs base |
|---|---|---|---|
| Base case, unhedged | 10,966.73 | 8.89% | |
| Stress, 50% higher volatility | 16,599.22 | 13.51% | +51% |
| FX locked at 12/31/2023 | 10,053.23 | 8.14% | -8% |
| Aluminum locked at 12/31/2023 | 3,786.77 | 3.04% | -65% |
| Robustness check, 15,000 scenarios | 10,296.17 | 8.37% | Same setup as base |

The benchmark is mean simulated pre-tax earnings for the year ending 12/31/2024.

## How C-VaR is measured

95% C-VaR is the gap between the benchmark and the 5th percentile of simulated earnings. It looks at the firm's earnings rather than its stock price, which is the view a CFO or treasury team uses when deciding what to hedge.

## How the model works

1. **Data.** Quarterly history from 1999 to 2023 for EUR/USD, aluminum per metric ton, and the 3-month interbank rate, converted to quarterly changes.
2. **Bootstrapping.** Each scenario randomly draws four historical quarters, one for each quarter of 2024, and applies that quarter's EUR/USD, aluminum, and interest rate changes together to the 12/31/2023 levels. Drawing all three from the same quarter keeps their historical co-movement and avoids assuming a normal distribution.
3. **Earnings.** Each scenario runs through an income statement covering translated euro revenue, aluminum purchases, FX gains and losses on euro receivables, and interest expense, which produces one pre-tax earnings figure. The base case uses 4,000 scenarios.
4. **Scenarios.** The base case, a stress case where every growth rate is scaled by 1.5, an FX lock, an aluminum lock, and a 15,000 scenario check.

## Reproducing the numbers

The workbooks draw scenarios with Excel's RAND function, so the figures move by a fraction of a percentage point each time Excel recalculates. The table above comes from the run in the PDF. The copies saved here show slightly different values, for example 9.05% for the base case and 2.97% for the aluminum lock, and the ordering of scenarios is the same.

## Limits

- Hedges are modeled as perfect price locks. Costs, basis risk, and accounting treatment are ignored.
- Hedges are static, and only annual pre-tax earnings are modeled, not cash flow timing or covenants.
- The simulation draws from history, so it assumes the past is informative about the future.
- The firm is a case-study company with fixed inputs for U.S. sales, expenses, and debt.

## Files

- `Monte_Carlo_Earnings_Risk_Report.pdf`: the full write-up, with the earnings distribution and C-VaR for every scenario and the hedging recommendation
- `Base_Case_Unhedged_CVaR.xlsx`: data, sampled quarters, projections, income statement, histogram, and C-VaR calculation for the base case
- `Stress_Scenario_Increased_Volatility.xlsx`: the 50% higher volatility case
- `FX_Hedging_Exchange_Rate_Locked.xlsx`: the EUR/USD lock
- `Commodity_Hedging_Aluminum_Price_Locked.xlsx`: the aluminum lock
- `Robustness_Check_15000_Scenarios.xlsx`: the 15,000 scenario check

This is a student project and not investment or hedging advice.
