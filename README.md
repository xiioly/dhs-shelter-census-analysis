-- Convert MM/DD/YYYY text dates to ISO format
CREATE VIEW dhs_clean AS
SELECT substr("Date of Census",7,4) || '-' || substr("Date of Census",1,2) || '-' || substr("Date of Census",4,2) AS census_date,
"Total Adults in Shelter" AS total_adults, "Total Children in Shelter" AS total_children,
"Total Individuals in Shelter" AS total_individuals, "Single Adult Men in Shelter" AS single_men,
"Single Adult Women in Shelter" AS single_women, "Total Single Adults in Shelter" AS total_single_adults,
"Families with Children in Shelter" AS families_with_children
FROM dhs_daily;

-- Data quality: date range and duplicates
SELECT COUNT(*) AS rows_total, COUNT(DISTINCT census_date) AS unique_dates, MIN(census_date), MAX(census_date) FROM dhs_clean;

-- Data quality: nulls
SELECT SUM(total_adults IS NULL), SUM(total_children IS NULL), SUM(total_individuals IS NULL), SUM(families_with_children IS NULL) FROM dhs_clean;

-- Data quality: totals reconcile
SELECT COUNT(*) FROM dhs_clean WHERE total_adults + total_children <> total_individuals;

-- Yearly averages
SELECT substr(census_date,1,4) AS year, COUNT(*) AS days, ROUND(AVG(total_individuals)) AS avg_individuals, MAX(total_individuals) AS peak_individuals, ROUND(AVG(total_children)) AS avg_children, ROUND(AVG(total_single_adults)) AS avg_single_adults FROM dhs_clean GROUP BY year ORDER BY year;

-- Monthly averages (exported to monthly_trend.csv)
SELECT substr(census_date,1,7) AS month, ROUND(AVG(total_individuals)) AS avg_individuals, ROUND(AVG(total_children)) AS avg_children, ROUND(AVG(total_single_adults)) AS avg_single_adults, ROUND(AVG(families_with_children)) AS avg_families FROM dhs_clean GROUP BY month ORDER BY month;
