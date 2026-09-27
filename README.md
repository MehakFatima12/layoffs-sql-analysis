# Tech Layoffs — SQL Data Cleaning & EDA (MySQL)

## 📌 Overview
Cleaned and analyzed a raw, messy global tech layoffs dataset using pure MySQL — from a messy `layoffs` table to a clean `layoffs_staging2` table, followed by exploratory analysis to surface layoff trends.

## 🧹 Part 1: Data Cleaning
**File:** `data_cleaning.sql`

- Removed duplicate rows using `ROW_NUMBER()` (no primary key existed)
- Standardized inconsistent text (trimmed whitespace, merged industry labels like `Crypto`/`CryptoCurrency`, fixed trailing punctuation in country names)
- Converted `date` from text to a proper `DATE` type
- Converted blank strings to real `NULL`s, then backfilled missing `industry` values via a self-join on `company`
- Deleted rows with no usable layoff data, dropped the helper `row_num` column

## 📊 Part 2: Exploratory Data Analysis
**File:** `eda.sql`

Key questions explored on the cleaned data:
- **Scale of layoffs:** max single-company layoffs and highest % of workforce cut
- **Companies that shut down entirely:** filtered `percentage_laid_off = 1`, ranked by size and by funds raised
- **Top companies, industries, and countries** by total layoffs (`GROUP BY` + `SUM`)
- **Time range** covered by the dataset (`MIN`/`MAX` date)
- **Layoffs by year and by company stage** (Post-IPO, Series C, etc.)
- **Monthly trend + rolling total** of layoffs over time using a CTE + window function
- **Top 5 companies per year** by layoffs using `DENSE_RANK()` over a company-year CTE

## 🛠️ Tools Used
MySQL 8.0 · Window Functions (`ROW_NUMBER`, `DENSE_RANK`, running `SUM() OVER`) · CTEs · Self-joins · Date/string functions

## 📂 Files
- `data_cleaning.sql` — full cleaning script
- `eda.sql` — exploratory analysis queries

## 🚀 Next Steps
Visualize these findings in Power BI (trends by year, top industries/companies, rolling layoff totals).
