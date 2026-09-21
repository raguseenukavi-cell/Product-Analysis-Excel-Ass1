Markdown# 📊 Excel Data Exploration & Analysis: Product Dataset

Welcome to the first project in my Data Analysis Portfolio! This project demonstrates fundamental data exploration, aggregation, logical categorization, and text manipulation techniques using **Microsoft Excel**.

---

## 📌 Project Overview
As an aspiring Data Analyst, mastering foundational Excel techniques is critical for cleaning, structuring, and extracting key insights from raw data. 

In this analysis, a dataset containing product details (IDs, names, brands, quantities, categories, and prices) was processed to summarize essential sales metrics, establish custom pricing classifications, and extract transactional metadata from alphanumeric text codes.

---

## 📁 Dataset Summary
- **Source Data:** Product Dataset
- **Attributes Included:** `Product ID`, `Product Name`, `Brand Name`, `Price ($)`, `Quantity`, `Category`
- **Total Records:** 33 Products

---

## 🎯 Key Tasks & Excel Solutions

### 1. Basic Data Exploration (Aggregation & Metrics)
* **Total Price of All Products:** Calculated using `=SUM(D2:D34)` $\rightarrow$ **$10,000**
* **Total Product Count:** Calculated using `=COUNTA(C2:C34)` $\rightarrow$ **33 Products**
* **Average Product Price:** Calculated using `=AVERAGE(D2:D34)` $\rightarrow$ **$303.03**
* **Minimum Product Price:** Identified using `=MIN(D2:D34)` $\rightarrow$ **$30**
* **Maximum Product Price:** Identified using `=MAX(D2:D34)` $\rightarrow$ **$1,000**

---

### 2. Logical Categorization & Conditional Logic
* **Price Range Classification (`IF` Function):**
  Created a custom column named `Price Range` to categorize products based on price thresholds:
  ```excel
  =IF(D2 >= 500, "High Price", "Standard Price")
High Price: Products with a price $\ge \$500$   Standard Price: Products with a price $<\$500$   Electronics Category Total Value (SUMIF Function):Calculated the cumulative sum of all products in the Electronics category:Excel=SUMIF(F2:F35, "Electronics", D2:D35)
$\rightarrow$ $8,050   Budget Product Count (COUNTIF Function):Counted the total number of products priced below $100:Excel=COUNTIF(D2:D35, "<100")
$\rightarrow$ 11 Products   3. Text Extraction & FormattingExtracted underlying metadata structured within the alphanumeric Product ID column (e.g., 28-JAN-US) to generate three new calculated columns:   Output ColumnFunction UsedExcel Formula ExampleSample InputSample OutputDescriptionDayLEFT=LEFT(A2, 2)28-JAN-US   28   First 2 characters   MonthMID=MID(A2, 4, 3)28-JAN-US   JAN   4th to 6th characters   Country CodeRIGHT=RIGHT(A2, 2)28-JAN-US[cite: 1]US[cite: 1]Last 2 characters[cite: 1]🛠️ Skills DemonstratedMathematical Aggregations: SUM, COUNTA, AVERAGE, MIN, MAX[cite: 1]Logical & Conditional Functions: IF, SUMIF, COUNTIF[cite: 1]Text Manipulation Functions: LEFT, MID, RIGHT[cite: 1]Data Structuring & Portfolio Documentation🚀 How to ViewClone or download this repository.Open the .xlsx file included in the root folder using Microsoft Excel or Google Sheets to inspect the formulas and sheet setup.
---

Are there any specific additions you'd like to make to this project, such as adding c
