# Key Learnings and Skills

## Key learnings
1. **Cleaning decisions need documenting.** Repeated order IDs and reused customer IDs were flagged and explained rather than silently dropped, so every later result could be traced back.
2. **Check joins before trusting them.** Joining on `Customer_ID` alone attached wrong attributes to reused IDs. Joining on ID plus name, and checking row counts and revenue totals, fixed it.
3. **Choose the method the data supports.** With one order per customer, cohort, retention and churn analysis were impossible, so I used segmentation instead and said why.
4. **Test your own insights.** In Task 4, none of eight hypothesis tests was significant. Patterns I had called findings in Task 2 (the Q4 lead, Electronics preference) were within random variation.
5. **A null result is still a result.** Reporting "no evidence of a difference" protects a business from acting on noise.
6. **Context matters in statistics.** Electronics' 36% revenue share matched having 2 of 6 products, so it showed no stronger customer preference.

## Limitations (stated honestly)
- Unit prices barely differ by product, so the dataset appears synthetic and product-level pricing conclusions are not reliable.
- Customer IDs are reused, so repeat-purchase analysis was not possible.
- Segments are rule-based with median cut-offs; the boundaries are a choice, not a natural gap.
- The dashboard is built as an interactive web page rather than in Tableau, Power BI or Looker Studio.

## Skills summary
| Area | Evidence |
|---|---|
| Python for analysis | Task 1 cleaning script, Task 2 charts, Task 4 tests |
| SQL | Task 2: 7 queries with joins, CTEs and a window function |
| Statistics | Task 4: t-test, ANOVA, chi-square, correlation, binomial, bootstrap |
| Dashboards and BI | Task 2 Excel mock-up, Task 3 interactive dashboard |
| Storytelling | Task 4 stakeholder deck and video |
| Reproducibility | Every task ships scripts, data and README |

## What I would do next
Collect repeat-purchase data for retention and lifetime value, run a proper A/B test on a bundle offer, and rebuild the dashboard in Power BI or Looker Studio.
