# Task 3: Deep-Dive Analysis & Interactive Dashboarding

**Data:** cleaned sales dataset from Task 1 (1,000 orders). Revenue in INR (assumed).
**Deep-dive chosen:** Segmentation analysis using business rules.
**Dashboard:** `sales_dashboard.html` (interactive; link in README).

## 1. Core KPIs
| KPI | Formula | Business rationale | Current value |
|---|---|---|---|
| Total Revenue | Sum of Total_Sales | Headline measure of business size | 139.4M |
| Average Order Value (AOV) | Total Revenue / Number of Orders | Shows how much each order is worth; the main lever for upselling | 139.4K |
| Units per Order | Total Quantity / Number of Orders | Shows basket size; separates "more items" from "pricier items" | 5.4 |
| Top Category Share | Revenue of the largest category / Total Revenue | Measures concentration risk | 36.4% (Electronics) |
| MoM Revenue Growth | (Revenue this month - last month) / last month | Detects seasonality and momentum | Dec 2025: -2.6% |

Conversion rate and churn were considered but **cannot be computed**: the dataset has no website visits and each customer appears in only one order (see Limitations).

## 2. Why segmentation
Cohort and retention analysis need repeat purchases, and this data has none (1,000 orders from 1,000 distinct customer ID + name pairs). Funnel analysis needs stage data, which is missing. Segmentation works on what the data does have: order price, quantity and spend.

## 3. Segmentation method
Each order is placed in one of four segments using two median split points: unit price (25.4K) and quantity (5 units).

| Segment | Rule |
|---|---|
| Big Spenders | Unit price >= 25.4K and quantity > 5 |
| Premium Single-Item | Unit price >= 25.4K and quantity <= 5 |
| Bulk Value Buyers | Unit price < 25.4K and quantity > 5 |
| Light Buyers | Unit price < 25.4K and quantity <= 5 |

## 4. Results
| Segment | Orders | % Orders | Revenue (M) | % Revenue | AOV (K) | Avg Age | Avg Qty |
|---|---|---|---|---|---|---|---|
| Big Spenders | 242 | 24.2% | 73.2 | **52.5%** | 302.3 | 42.1 | 7.9 |
| Premium Single-Item | 258 | 25.8% | 29.5 | 21.1% | 114.2 | 40.5 | 3.1 |
| Bulk Value Buyers | 239 | 23.9% | 26.1 | 18.7% | 109.3 | 39.7 | 8.0 |
| Light Buyers | 261 | 26.1% | 10.7 | 7.6% | 40.8 | 43.0 | 3.1 |

## 5. Key findings
1. **Concentration:** Big Spenders are 24% of orders but 52.5% of revenue. Their AOV (302K) is more than twice the overall average.
2. **Light Buyers are the weakest segment:** 26% of orders but only 7.6% of revenue (AOV 40.8K).
3. **Two routes to a mid-sized order:** Premium Single-Item customers (high price, few units) and Bulk Value Buyers (low price, many units) have almost the same AOV (114K vs 109K).
4. **Segments are behavioural, not demographic.** Average age is 40 to 43 in every segment, and Electronics is the top category in all four (33% to 41%). Targeting by age or city would not find Big Spenders; basket size and price tier would.
5. **Small category tilts (treat with caution):** Bulk Value Buyers are the most Electronics-heavy (41%), Premium Single-Item buyers lean to Fashion (20% vs 13-15% elsewhere), and Big Spenders buy more Grocery than Bulk Value Buyers (19% vs 12%).
6. **Seasonality:** monthly growth swung from +36.2% (Oct) to -19.6% (Aug), consistent with the Aug-Sep dip found in Task 2 (not statistically confirmed in Task 4).

## 6. Recommendations
- **Protect Big Spenders** with early access, bundles and loyalty offers, since losing a few of them costs the most revenue.
- **Convert Premium Single-Item buyers into multi-item buyers** with bundle offers and "buy more, save more" pricing. They already accept high prices, so increasing units has the biggest upside.
- **Raise the basket of Light Buyers** with add-ons at checkout; they are the largest group by orders but contribute least revenue.
- **Test a pre-September promotion** with a proper A/B test before rolling it out; the seasonal dip was not statistically confirmed in Task 4.

## 7. Limitations
- Each customer appears once, so repeat purchase, retention, lifetime value and churn cannot be measured.
- Segments are rule-based with median cut-offs; they are easy to explain, but the boundaries are a choice, not a natural gap in the data (price and quantity are spread fairly evenly).
- Unit prices do not differ by product (noted in Task 2), so the data appears synthetic.
- 13 orders have an unknown city and 20 ages were imputed.
