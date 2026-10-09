# Problem-Set-1-Econ_3916_PS1.ipynb
Problem Set 1
# The Cost of Living Brief: A Household Price Index vs. the Official CPI

## Objective
I built a price index for one household's spending and compared it with official CPI series to test whether the CPI overstates or understates what that household faces.

## Methodology
- Built a basket of six categories (milk, eggs, bread, ground beef, gasoline and chicken) with 2019 and 2024 prices and spending weights that sum to 1.
- Wrote a function for a weighted Laspeyres index (2019 = 100) and compared it with a simple unweighted average of the six price changes.
- Pulled five series from FRED with no API key: headline CPI (`CPIAUCSL`), rent (`CUSR0000SEHA`), food at home (`CUSR0000SAF11`), used vehicles (`CUSR0000SETA02`) and average gasoline price (`APU00007471A`). For each, I wrote down why it is a fair proxy for my household and what it misses.
- Converted each series to annual averages, rebased them to 2019 = 100 and plotted them on one chart with my household index.
- Audited every series for its first and last observation, frequency and missing months.
- Found the common sample across all five series and compared average annual growth over each series' full history against the common sample only.
- Plotted the seasonally adjusted and unadjusted used-vehicle series over the last five years to see what seasonal adjustment removes.
- Used an AI model to write a weight-sensitivity sweep. The sweep moves each category's weight from 0% to 50% and rescales the others in proportion. I checked the code against an independent calculation, added warnings for rescaled weights and weights above 50%, and wrote a 250-word finding for the director.

## Key Findings
- **My household's costs rose 48.4% from 2019 to 2024** (index 148.43), against 22.7% for headline CPI. On this basket, the CPI understates the household's costs rather than overstating them.
- The unweighted average price change was 58.31%, 9.88 points above the weighted index. Giving every item equal importance overstates the increase for this household.
- Every official series rose less than my index. Food at home rose 26.8%, rent 26.9%, used vehicles 28.7% and gasoline 32.6%.
- Eggs drive the result. They carry only a 10% weight, but their price rose 170%, so they account for 17 of the 48 points of increase. The index is most sensitive to the egg weight: 13.5 points per 10 percentage points of weight, against 3.6 points at most for any other category.
- The main conclusion holds anyway. With eggs removed the index is still 134.9, the lowest value across every sweep, which is well above CPI.
- The sample period changes the story. The common sample starts in January 1981, runs 547 months and drops 408 months of CPI history. Over full histories, gasoline grew faster than CPI (4.05% vs. 3.51% a year). Over the common sample it grew more slowly (2.74% vs. 2.99%), because the full history includes the 1970s oil shocks.
- Four of the five series are missing October 2025. Used vehicles has no gaps.
- The gap between the adjusted and unadjusted used-vehicle series is the seasonal pattern. I used the unadjusted series because it reflects the prices people actually paid and matches the gasoline series, which is only published unadjusted.
- My confidence in the finding is moderate. I am confident the household's costs outpaced CPI, but much less confident in the exact 48% figure.

## Limitations
- The basket covers only food and gasoline. It leaves out housing, the largest expense for most households, so the index measures food-and-fuel costs, not the full cost of living.
- Weights are fixed at 2019 spending. If the household bought fewer eggs as their price rose, the true increase is lower than my index shows.
- A 10% weight on eggs is high for most households, so the realistic figure is closer to the low end of my range.
- My index has only two points, 2019 and 2024, so it cannot show the path between them.

## Tools and Data
- Python (pandas, NumPy, matplotlib) in Google Colab
- FRED series listed above
- Basket prices entered by hand for 2019 and 2024
