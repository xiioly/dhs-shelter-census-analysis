# NYC DHS Shelter Census Analysis

Analysis of daily shelter population counts from the NYC Department of Homeless Services (DHS) Daily Report, March 2021 to October 2026.

## Data
- Source: NYC Open Data, DHS Daily Report (https://data.cityofnewyork.us/d/k46n-sa2m)
- 2,065 daily records, 13 columns (adults, children, single adults, families)

## Process
1. Loaded the CSV into SQLite (DB Browser for SQLite)
2. Converted text dates (MM/DD/YYYY) to ISO format with a SQL view
3. Ran data quality checks: no duplicate or missing dates, no null values, and totals reconcile on every row
4. Aggregated yearly and monthly averages with SQL
5. Built a Power BI dashboard of monthly trends

## Key findings
- Average daily individuals in shelter rose from 47,077 (2021) to 87,105 (2024), then declined to 84,072 (2026, through October)
- Average children in shelter fell 12.2% from 2024 to 2026 (32,839 to 28,817)
- Average single adults rose 25.2% from 2024 to 2026 (20,502 to 25,665)

## Notes
- 2021 (March to December) and 2026 (January to October 25) are partial years
- Counts are aggregate daily totals; no individual-level data is used

## Files
- `analysis.sql`: all queries
- `monthly_trend.csv`: monthly averages used in the dashboard
- `dashboard.png`, `dashboard_full.png`: Power BI report screenshots

## Tools
SQL (SQLite), Power BI
