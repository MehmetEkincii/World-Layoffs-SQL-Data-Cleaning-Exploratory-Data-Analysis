# World-Layoffs-SQL-Data-Cleaning-Exploratory-Data-Analysis
This project involves cleaning and exploring a real-world dataset of global tech layoffs using MySQL. The goal was to take raw, messy data and transform it into a clean, reliable dataset ready for analysis — then use SQL to uncover patterns and trends in layoffs across companies, industries, and countries.

Phase 1: Data Cleaning

All cleaning was performed on a staging table to keep the original raw data untouched as a backup.

Step 1 — Remove Duplicates

Used ROW_NUMBER() with PARTITION BY across all columns to flag exact duplicates
Deleted any row with a row number greater than 1
5 duplicate rows removed

Step 2 — Standardize Data & Fix Errors

Scanned industry values with SELECT DISTINCT to identify inconsistencies
Converted blank industry strings to NULL, then used a self-join to populate them from matching company records
Consolidated crypto variations (Crypto Currency, CryptoCurrency) → Crypto
Removed trailing periods from country names (United States. → United States)
Converted the date column from TEXT to proper DATE type using STR_TO_DATE()

Step 3 — Handle NULL Values

NULL values in total_laid_off, percentage_laid_off, and funds_raised_millions were intentionally kept
Replacing with 0 would skew aggregates — SQL functions like AVG() and SUM() ignore NULL automatically

Step 4 — Remove Unnecessary Columns & Rows

Removed rows where both total_laid_off and percentage_laid_off were NULL — no usable layoff data
Dropped the temporary row_num column after duplicate removal was complete

Phase 2: Exploratory Data Analysis

Looked at the maximum layoffs in a single event
Explored the range of percentage_laid_off across all companies
Identified companies that laid off 100% of their workforce
Ordered those companies by funds_raised_millions to understand their size
