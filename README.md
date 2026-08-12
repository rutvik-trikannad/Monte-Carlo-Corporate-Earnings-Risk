# Monte Carlo Corporate Earnings Risk (C-VaR)

A Corporate Value-at-Risk (C-VaR) analysis measuring a multinational firm's pre-tax earnings downside risk from three sources: EUR/USD exchange rate movements, aluminum input costs, and short-term interest rates. Based on the HBR case study framework "Understanding Corporate-Value-at-Risk through a Comprehensive and Simple Example."

Quarterly data from 1999–2023 is bootstrapped into 4,000 Monte Carlo scenarios to forecast pre-tax earnings for the year ending 12/31/2024. Risk is measured using 95% C-VaR: the expected earnings shortfall in the worst 5% of outcomes.

## Scenarios analyzed

| Scenario | 95% C-VaR | C-VaR as % of Benchmark |
|---|---|---|
| Base Case (unhedged) | $10,966.73K | 8.89% |
| Stress (50% higher volatility) | $16,599.22K | 13.51% |
| FX Rate Locked-In | $10,053.23K | 8.14% |
| Commodity Price Locked-In | $3,786.77K | 3.04% |
| Robustness Check (15,000 scenarios) | $10,296.17K | 8.37% |

**Key finding:** Aluminum price hedging delivered the largest reduction in downside risk, cutting C-VaR from 8.89% to 3.04% of benchmark earnings, indicating commodity cost volatility was the dominant driver of tail risk for this firm, more so than FX exposure.

## Files
- `Monte_Carlo_Earnings_Risk_Report.pdf` — full write-up: methodology, all five scenarios, scenario comparison, and hedging recommendation
- `Base_Case_Unhedged_CVaR.xlsx` — data inputs and base-case C-VaR calculation
- `Stress_Scenario_Increased_Volatility.xlsx` — 50%-amplified volatility scenario
- `FX_Hedging_Exchange_Rate_Locked.xlsx` — EUR/USD locked-in scenario
- `Commodity_Hedging_Aluminum_Price_Locked.xlsx` — aluminum price locked-in scenario
- `Robustness_Check_15000_Scenarios.xlsx` — robustness check with 15,000 simulations
