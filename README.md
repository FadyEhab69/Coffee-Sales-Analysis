# Coffee Sales Analysis Documentation

# Overview

This report presents a comprehensive analysis of a Coffee Sales dataset, showcasing proficiency in data cleaning, transformation, and visualization using Power Query, Power Pivot, and Excel. The dataset, initially containing raw sales and customer information, was processed to uncover trends in sales performance, customer preferences, and regional demand over a multi-year period (2019–2022).

# Data Cleaning and Transformation

- Before Cleaning (Raw Dataset)
The raw dataset, as provided in the coffeeOrdersData.xlsx file, likely had the following issues, inferred from the documentation and the nature of the data:

Missing or Incomplete Data:
Several rows in the orders sheet have missing values, particularly in the Customer Name, Email, and Sales columns. For example:
Order ID QEV-37451-860 lacks Customer Name, Email, and Sales data.
The Sales column is entirely empty across all rows, which is critical for analysis.
In the customers sheet (partially shown in the truncated section), some entries lack Email or Phone details (e.g., Merell Zanazzi has no email).
Inconsistent Formatting:
Column Headers: Headers might have had extra spaces or quotes (e.g., " Order ID " instead of Order ID).
Cell Values: Values in columns like Customer Name or Email could have leading/trailing spaces or quotes (e.g., " John Doe " or "john.doe@example.com ").
Date Formats: The Order Date column (e.g., 9/5/19) might have inconsistent formats across rows, such as MM/DD/YY vs. DD-MM-YYYY, or unparsed string formats.
Incorrect Data Types:
Numerical fields like Quantity, Unit Price, and Sales might have been stored as text or had inconsistent formats (e.g., Unit Price in the products sheet is numeric, but Sales in the orders sheet is missing and might have been text or misformatted in the raw data).
Dates in the Order Date column were likely stored as strings (e.g., 9/5/19) rather than proper date formats, making time-series analysis difficult.
Categorical fields like Coffee Type and Roast Type might have had inconsistencies (e.g., Ara vs. Arabica, or L vs. Light).
Outliers and Anomalies:
While the raw dataset doesn’t explicitly show outliers, the documentation mentions a flagged outlier (e.g., $840.93 in September 2021 for Liberica sales), indicating that the raw data likely contained unusually high or low values in the Sales column before cleaning.
Duplicate entries or inconsistent Order ID formats might have existed (e.g., same Order ID with different products but inconsistent customer details).
Lack of Relationships:
The orders and products sheets were separate, with no explicit relationships defined between Product ID in both sheets.
Customer data (e.g., Customer ID) was not fully linked to the orders sheet due to missing customer details in some rows.
Cleaning Process (As Described)
The cleaning and transformation steps applied using Power Query and Power Pivot addressed the above issues:

Handling Missing Values:
Rows with missing or invalid entries were discarded. For example, rows missing critical fields like Customer Name or Sales (which is entirely missing in the raw data) were likely removed unless they could be imputed or linked via other data (e.g., Customer ID lookup).
Since the Sales column is empty in the raw dataset, it was likely calculated or populated during cleaning by multiplying Quantity from the orders sheet with Unit Price from the products sheet (e.g., for Order ID QEV-37451-860, R-M-1 with Quantity 2 and Unit Price $9.95 would yield Sales = $19.90).
Standardization:
Column Headers: Headers were cleaned by trimming extra spaces and quotes (e.g., " Order ID " → Order ID).
Cell Values: Leading/trailing spaces and quotes were removed from values (e.g., " John Doe " → John Doe).
Date Formats: The Order Date column was standardized to a consistent format (e.g., 9/5/19 → 2019-09-05 or a proper Excel date format) to enable time-series analysis.
Type Conversion:
Numerical fields like Quantity, Unit Price, and the newly calculated Sales were ensured to be in numeric format.
Categorical variables were normalized:
Coffee Type: Converted shorthand codes (Ara, Rob, Lib, Exc) to full names (Arabica, Robusta, Liberica, Excellsa).
Roast Type: Converted L, M, D to Light, Medium, Dark.
Order Date was parsed from strings to proper date formats for time-series analysis (e.g., 9/5/19 → Excel date serial number or 2019-09-05).
Outlier Detection:
Outliers were flagged for review. For instance, the documentation notes a Liberica sales value of $840.93 in September 2021 as an anomaly. In the raw data, since Sales is missing, this value was likely calculated during cleaning and then flagged as unusually high compared to typical sales values (most sales might range in the tens or low hundreds based on Unit Price and Quantity).
Establishing Relationships:
Using Power Pivot, relationships were created between the orders and products sheets via the Product ID column to calculate Sales and enable analysis by coffee type, roast type, and size.
Relationships between orders and customers were likely established using Customer ID to fill in missing customer details (e.g., Customer Name, Email) where possible.
After Cleaning (Transformed Dataset)
The dataset after cleaning would have the following characteristics:

Complete Data:
Missing values were either filled or rows were removed. For example:
The Sales column, previously empty, is now populated by multiplying Quantity and Unit Price (e.g., Order ID QEV-37451-860, Product R-M-1, Quantity 2, Unit Price $9.95 → Sales = $19.90).
Rows with incomplete customer details (e.g., missing Customer Name and Email) were likely removed unless they could be linked via Customer ID.
Standardized Formatting:
Headers are clean (e.g., Order ID, Customer Name, Sales with no extra spaces or quotes).
Cell values are trimmed (e.g., Customer Name = John Doe, Email = john.doe@example.com).
Order Date is in a consistent format, such as YYYY-MM-DD (e.g., 2019-09-05).
Correct Data Types:
Quantity, Unit Price, and Sales are numeric (e.g., Sales = 19.90).
Order Date is a proper date type (e.g., 2019-09-05 as a date object).
Categorical fields are normalized:
Coffee Type: Arabica, Robusta, Liberica, Excellsa.
Roast Type: Light, Medium, Dark.
Outliers Addressed:
Outliers like the $840.93 Liberica sales in September 2021 were flagged and possibly adjusted or removed if deemed erroneous. In the cleaned data, sales values are more consistent (e.g., most sales might range from $5 to $150 based on typical Quantity and Unit Price combinations).
Relationships Established:
The orders sheet now links to the products sheet via Product ID, allowing Sales calculation and analysis by coffee type, roast type, and size.
Customer details are linked via Customer ID, filling in missing Customer Name and Email where possible.
Calculated measures in Power Pivot (e.g., total sales by country) are now available for analysis.
Example of Cleaned Data (Hypothetical Row):
Raw Row (Before):
Order ID: QEV-37451-860, Order Date: 9/5/19, Customer ID: 17670-51384-MA, Product ID: R-M-1, Quantity: 2, Customer Name: (empty), Email: (empty), Country: (empty), Coffee Type: Rob, Roast Type: M, Size: 1, Unit Price: 9.95, Sales: (empty).
Cleaned Row (After):
Order ID: QEV-37451-860, Order Date: 2019-09-05, Customer ID: 17670-51384-MA, Product ID: R-M-1, Quantity: 2, Customer Name: (filled or row removed), Email: (filled or row removed), Country: (filled or row removed), Coffee Type: Robusta, Roast Type: Medium, Size: 1, Unit Price: 9.95, Sales: 19.90.

# Analytical Approach

The analysis focused on key dimensions to identify trends and patterns:





Sales Over Time: Evaluated monthly sales trends across coffee types (Arabica, Excellsa, Liberica, Robusta) from 2019 to 2022.



Regional Performance: Compared total sales across the United States, Ireland, and the United Kingdom.



Customer Segmentation: Identified top customers by sales volume and analyzed the impact of loyalty card usage.



Product Preferences: Assessed sales by size (0.2kg, 0.5kg, 1kg, 2.5kg) and roast type (Light, Medium, Dark) to determine customer preferences.

# Key Findings



Sales Trends: Total sales fluctuated significantly, with peaks in April 2019 ($1,680.75) and September 2021 ($1,643.49), suggesting seasonal or promotional influences. Robusta and Excellsa showed the highest variability.


Regional Insights: The United States led with $35,638.88 in total sales, followed by Ireland ($6,696.86) and the United Kingdom ($2,798.50), indicating a strong U.S. market dominance.


Top Customers: Allis Wilmore ($317.07) and Brenn Dundredge ($307.04) were the top spenders, with loyalty card holders contributing significantly to sales.


Interesting Fact: An unexpected surge in Liberica sales (e.g., $840.93 in September 2021) highlights a potential emerging preference, possibly driven by marketing or new product launches.

# Visualization

An interactive dashboard was developed in Excel to present the analysis visually:



Total Sales Over Time: A line chart tracked monthly sales by coffee type, revealing seasonal peaks and troughs.


Sales by Country: A bar chart compared total sales across regions, with the U.S. showing the highest volume.


Top 5 Customers: A horizontal bar chart listed the top customers by sales, emphasizing loyalty card impact.


Filters: Dropdowns for Order Date, Size, Loyalty Card, and Roast Type enabled dynamic data exploration.

# Conclusion

This analysis demonstrates a robust approach to transforming raw data into actionable insights using Power Query for cleaning, Power Pivot for modeling, and Excel for visualization. The findings suggest focusing marketing efforts on the U.S. market, targeting top customers, and exploring the growing interest in Liberica. Future analysis could incorporate predictive modeling to forecast sales and optimize inventory.
