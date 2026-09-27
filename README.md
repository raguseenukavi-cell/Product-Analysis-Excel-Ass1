Data Cleaning & Transformation — E-Commerce Product Dataset
An end-to-end data-cleaning project on a messy e-commerce product dataset. The raw data contained missing values, inconsistent text formatting, spelling errors, duplicate records, and composite fields that had to be split and standardised. This repository documents the complete process, from auditing the raw data to delivering an analysis-ready, formatted dataset.
📊 Project Overview


Domain
E-commerce / Retail
Raw dataset
34 products × 6 columns
Cleaned dataset
31 products × 6 columns
Tools used
Microsoft Excel (find & replace, number formats, conditional formatting) and Python (pandas, openpyxl)
The cleaned file Assignment_2_Cleaned.xlsx contains two sheets: Original Data (the untouched raw data, for before/after comparison) and Cleaned Data (the final, analysis-ready output).
🗂️ The Raw Data
Each product record had six fields:
Column
Description
Example
Product ID
Composite code: DD-MMM-CC (day-month-country)
28-JAN-US
Product Name
Name of the product
laptop
Brand Name
Manufacturer
Dell
Price ($)
Product price
1000
Quantity
Units in stock
30
Category
Product category
Electronics
🧹 Data Cleaning Process
1. Handling Missing Values
An audit of the dataset found:
•
3 missing prices — Sony Headphones, Coleman Camping Tent, Ray-Ban Sunglasses
•
4 missing categories — North Face Backpack, Adidas Sneakers, Nespresso Coffee Maker, Xiaomi Fitness Tracker
Missing prices — approach: Prices were imputed with the median price of each product's own category. The category median was chosen over the mean because it is robust to the outliers in this data (e.g. a $1,000 laptop would inflate the mean of the Electronics group).
Product
Category
Imputed Price
Sony Headphones
Electronics
$600.00
Coleman Camping Tent
Outdoor
$130.00
Ray-Ban Sunglasses
Fashion
$70.00
Alternative considered: dropping the rows (only ~9% of data, but the rows still carry useful quantity/brand information) or leaving them blank (breaks downstream aggregations like total inventory value).
Missing categories — approach: Categories were imputed by mapping the product to its category elsewhere in the dataset — the same product family already appears in the data with a known category, so no guesswork was involved:
Product
Imputed Category
Evidence in data
Backpack
Accessories
Laptop Bag → Accessories
Sneakers (Adidas)
Fashion
Sneakers (Nike) → Fashion
Coffee Maker
Kitchen
Coffee Maker (Keurig) → Kitchen
Fitness Tracker
Electronics
Fitness Tracker (Garmin) → Electronics
2. Correcting Inconsistent Data
•
Product Name (text format): 5 entries were in lowercase (laptop, smartphone, headphones) while the rest used Title Case. Standardised all values to Title Case using find & replace (laptop → Laptop, smartphone → Smartphone, headphones → Headphones).
•
Category (typos): 5 entries contained the misspelling `Electroni` instead of Electronics. Fixed with find & replace (Electroni → Electronics), then verified the Category column contains only 5 valid values: Accessories, Electronics, Fashion, Kitchen, Outdoor.
3. Removing Duplicates
A full-row duplicate check found 3 records entered twice (6 duplicate rows in total, keeping the first occurrence of each):
•
HP Laptop — 17-JUN-IN
•
Bose Headphones — 16-APR-ES
•
Samsonite Laptop Bag — 21-AUG-CA
The second occurrence of each was removed, taking the dataset from 34 rows to 31 rows.
4. Splitting and Merging Data
•
Split `Product ID` into two columns, removing the - separators:
•
Manufacturing Date — the DD-MMM part, parsed into a true date (e.g. 28-JAN → 28 January). Note: the ID encodes only day and month, so the year 2024 was assumed for all records.
•
Country Code — the final two-letter part (US, UK, IN, CA, AU, DE, ES, CN, IT, RU, BR, FR).
•
Merged `Brand Name` + `Product Name` into a single `Product Brand` column (e.g. Dell + Laptop → Dell Laptop), giving a single human-readable identifier per product.
5. Number Formatting
•
Price formatted as currency: $#,##0.00 (e.g. 1000 → $1,000.00).
•
Manufacturing Date formatted as DD-MM-YYYY (e.g. 28-01-2024), stored as real dates so they remain sortable and filterable.
6. Conditional Formatting
•
Data bars on the Price column — an in-cell gradient bar makes expensive vs. cheap products instantly visible (laptops at ~$1,000 stand out against accessories at ~$50).
•
Custom rule on the Category column — cells where the category equals Electronics are highlighted in yellow, using the custom conditional-formatting rule =$F2="Electronics". This makes the largest product group easy to scan.
📈 Before → After Summary
Check
Raw Data
Cleaned Data
Rows
34
31 (−3 duplicates)
Missing prices
3
0
Missing categories
4
0
Misspelled categories (Electroni)
5
0
Inconsistent product-name casing
5
0
Columns
6 (incl. composite Product ID)
6 (incl. split date/country + merged Product Brand)
Number/date formats
Unformatted
Currency + DD-MM-YYYY
📁 Repository Structure
code
├── README.md                          # Project documentation (this file)
├── Assignment_2_-_Data_Cleaning_and_Transformation.xlsx   # Raw dataset (as received)
├── Assignment_2_Cleaned.xlsx          # Final cleaned workbook (Original Data + Cleaned Data sheets)
└── data_cleaning.py                   # Python script reproducing every cleaning step
🔁 Reproducing the Cleaned File
bash
pip install pandas openpyxl
python data_cleaning.py
The script reads the raw workbook, applies all six cleaning steps in order (fix text → de-duplicate → impute), and writes Assignment_2_Cleaned.xlsx. Every imputed value and removed duplicate is printed to the console so the transformation is fully auditable.
💡 Key Takeaways
•
Audit before you clean — profiling the raw data first (missing-value counts, category frequencies, duplicate checks) revealed exactly six distinct problems to solve.
•
Impute with domain logic, not blind defaults — category medians for prices and product-to-category mapping produced imputations that are defensible, not arbitrary.
•
Median beats mean for skewed price data — a single $1,000 laptop would pull a mean-based imputation far above the typical product price.
•
De-duplicate before imputing — otherwise duplicate rows bias the medians used for imputation.
•
Keep formatting semantic — dates stored as real dates (displayed DD-MM-YYYY) rather than text, and prices as true numbers with a currency format, so the file remains usable by pivot tables and further analysis.
