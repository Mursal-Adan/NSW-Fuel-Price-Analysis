# NSW Fuel Price Analysis

## Business Problem
Which fuel types, brands, or regions have the highest/lowest prices, and how much does price vary across service stations and time — useful for a consumer-facing or fleet-management business question.

## Dataset
**NSW FuelCheck Price History (October 2025)** — 69,132 real fuel price records from the NSW Government's FuelCheck program, covering 8 fuel types and 40+ brands across NSW service stations.
Source: [Data.NSW](https://data.nsw.gov.au/data/dataset/fuel-check)

## Tools
Excel (cleaning, analysis) · Tableau (visualization)

## Dashboard
🔗 [View live dashboard on Tableau Public](https://public.tableau.com/views/NSWFuelPriceAnalysisDashboard/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## Process
1. **Investigation** — checked row count, duplicates, brand/fuel code consistency, price range, and date format.
2. **Cleaning** — resolved a significant date parsing issue: the `PriceUpdatedDate` column mixed real date values with text strings in day-first (DD/MM/YYYY) format, which Excel's locale-based parser misread or failed on inconsistently; fixed by rebuilding the column from raw text using explicit day/month/year extraction.
3. **Analysis** — answered the business problem across 4 dimensions: fuel type, brand, suburb/region, and day of week, using average price (not summed price) and applying a minimum sample size filter (500+ records) to avoid misleading small-sample results.
4. **Visualization** — built a 4-chart Tableau dashboard, pairing average price with record count on every chart to keep reliability visible.

## Key Findings

**By fuel type**
- P98 is the most expensive fuel (204.26 average), followed by P95 (197.71) and E85 (194.55).
- LPG is dramatically cheaper (116.92 average), about 43% lower than P98 — expected, as it's a different fuel category.

**By brand** (minimum 500 records to ensure reliability)
- Reddy Express has the highest average price (203.35), followed by Coles Express (202.36) and Ampol Foodary (195.72).
- 7-Eleven, despite having by far the most records (20,381), sits mid-pack (191.48) — market presence doesn't predict price level.
- Several small independent brands (1–23 records) showed extreme averages in both directions; excluded from ranking as statistically unreliable.

**By suburb** (minimum 500 records)
- Penrith (200.50) and Campbelltown (200.04) are the most expensive suburbs in this dataset.
- Cessnock (174.15) and Bankstown (174.66) are the cheapest — a ~26-point spread.
- Only 12 of roughly 500 suburbs met the reliability threshold; this is a high-traffic slice of NSW, not a full geographic picture.

**By day of week**
- Monday has the highest average price (191.49); Thursday the lowest (186.03) — a modest ~3% spread across the week.
- Prices trend slightly higher early in the week (Mon/Sat/Sun) and slightly lower midweek (Wed/Thu).

## Recommendations
- For cost-conscious consumers or fleets: prioritize P95/E10/U91 over P98 where the vehicle allows, and consider Thursday/Wednesday for marginally lower average prices.
- Brand loyalty should not be assumed to correlate with price — Reddy Express and Coles Express carry a real premium over larger brands like 7-Eleven.
- Regional price differences (Penrith/Campbelltown vs Cessnock/Bankstown) suggest route planning for fleet refueling could yield modest savings, though this is based on a small set of reliably-sized suburbs.

## Files
- `nsw_fuel_price_analysis.xlsx` — raw and cleaned data, pivot tables, analysis
- Tableau dashboard: see link above

## Limitations
- Single month of data (October 2025) — no seasonal or long-term trend analysis possible.
- Many brands and suburbs have too few records for reliable comparison; only groups with 500+ records (fuel type: all; brand: 10 of 40+; suburb: 12 of ~500) are reported as findings.
- 15 duplicate rows found with no unique transaction ID to confirm whether they're genuine repeats or data errors; kept as-is, not removed.
- Significant time was spent resolving a date-format parsing bug (mixed DD/MM/YYYY text and real date values); documented as a real-world data cleaning challenge.
