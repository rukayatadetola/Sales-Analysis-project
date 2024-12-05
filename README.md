# SALES ANALYSIS PROJECT

---
## SALES ANALYSIS PROJECT REPORT

---
### Project Overview

This data analysis aims to provide insights into the sales performance of a fictional company over past years. By analyzing various aspects of the sales data, we seek to identify trends, make data-driven recommendation, and gain a deeper understanding of the sales performance. The report includes a comprehensive breakdown of the data, methods applied, and insights that reveal patterns in customer purchasing behavior and product sales performance.

### Data Sources : Kaggle.com
---
### Tools:
1. ####	Excel:
   1. Used for data storage, initial formatting, and preliminary analysis.
   2.   Acts as the primary data source, enabling easy import into Python and Power BI.
2. ####	Python - Used for data preprocessing, cleaning, and transformation.
   ##### Libraries Used:
   1. Pandas: For data manipulation and cleaning.
   2. Matplotlib/Seaborn: For exploratory visualizations during preprocessing.

3. ####	Power BI:
   1. For Creating interactive visualizations
   2. For visuals that present business insights in a user-friendly format.
   3. For creating dashboard. [View Here](https://ibb.co/6sxDjRL AND https://ibb.co/3Yb7jD1)
      
---
### Analysis Breakdown
```Python
--- HANDLED MISSING VALUES---
merged_datfra2.isnull().sum()
```
```Python
--- MERGE THREE TABLES ---
--- First Merge ---
merged_datfra= pd.merge(df,dff, on='Product Name',how='inner')

--- Rename a column Order YearMonth to Year Month ---
dfff.rename(columns={'Order YearMonth': 'Year Month'}, inplace=True) 

--- Second Merge ---
merged_datfra2=pd.merge(merged_datfra, dfff, on=['Product Name','Year Month'], how='inner')

```
```Python
--- CALCULATE THE TOTAL SALES OVER YEAR 2015 - 2017---
merged_datfra2['Total Sales'] = merged_datfra2['Gross Sales'] * (1 - merged_datfra2['Discount %'])

merged_datfra2['Total Sales']
```
```Python
--- CALCULATE THE SALES GROWTH RATE ---
merged_datfra2['Sales Growth Rate']=merged_datfra2['Total Sales']-(merged_datfra2['Total Sales']-1)/(merged_datfra2['Total Sales']-1)*100

merged_datfra2['Sales Growth Rate'].fillna(0)
```
``` Python
---CALCULATE THE PROFIT MARGIN---
merged_datfra2['profit_margin']=(merged_datfra2['Profit']/merged_datfra2['Total Sales']*100)

merged_datfra2['profit_margin'].fillna(0)
```
```Python
import datetime as dt

merged_datfra2['Year Month'] = pd.to_datetime(merged_datfra2['Year Month'], format='%Y%m',errors='coerce')
```
```Python
--- VISUALIZING OUTLIERS USING BOX PLOTS---
from scipy import stats
z_scores = np.abs(stats.zscore(merged_datfra2.select_dtypes(include=np.number)))
outliers = np.where(z_scores > 3)

print("\nOutliers (based on Z-score > 3):")
print(outliers)


for column in merged_datfra2.select_dtypes(include=np.number).columns:
    plt.figure(figsize=(6, 4))
    sns.boxplot(merged_datfra2[column])
    plt.title(f"Boxplot of {column}")
    plt.show()
```
``` Python
--- IDENTIFY PATTERNS---
print("Few rows of the dataset:")
print(merged_datfra2.head())
```
```Python
---  SELECT ONLY NUMERIC COLUMNS FOR CORRELATION ---
num_df = merged_datfra2.select_dtypes(include=[float, int])

# Now, calculate the correlation
corr_matrix = num_df.corr()

# Display the correlation matrix
print(corr_matrix)
```
```Python
---  Display Summary statistics
print("\nSummary statistics:")
print(merged_datfra2.describe())
```
---
### KPI Overview
The top section of the dashboard showcases critical KPIs for a high-level summary:

   - Total Sales ($5.55M): Represents the total revenue generated.
   - Profit Margin ($2.92M): Highlights net profit after deducting costs.
   - Growth Rate ($2.47M): Displays growth trends compared to the previous period.
   - Average Sales ($179.9): Calculates the mean sales per order.
   - Order Count (31K): Tracks the total number of completed orders.
---
### Insights
   -	Total sales reached $5.55M, with a profit margin of $2.92M and a growth rate of $179.9, showing consistent growth.
   -	Both sales and profits fluctuate slightly month-to-month but follow a similar upward trend, indicating stable demand.
   -	Air shipments make up 54% of orders, suggesting a preference for fast delivery, possibly increasing shipping costs.
   -	Profits are strongest in North America and Europe, highlighting these regions as key markets.
   -	Fishing gear (especially cleats) leads sales, followed by Camping & Hiking and Women’s Apparel. Indoor/Outdoor Games and Water Sports show lower sales, indicating areas for              potential improvement.
---
### Recommendations
   -	Since air shipment constitutes the largest portion, consider whether this is necessary for all products or if slower, cheaper options could be utilized for less time-sensitive items.
   -  Focus marketing efforts in North America and Europe, where profit margins are high.
   -	Continue to support high-performing categories (e.g., Fishing and Camping) with additional marketing, while exploring why certain categories like Indoor/Outdoor Games have lower         sales.
   -	Keep an eye on monthly sales and profit trends. If certain months show consistent drops, investigate potential seasonal factors or market dynamics.


---
### Data Visualization

![Screenshot (11)](https://github.com/user-attachments/assets/ea0ae98d-9a6e-4253-b575-968e24f060f5)

![Screenshot (13)](https://github.com/user-attachments/assets/1ed7c3c8-db1a-4bea-8890-bb83f4382f45)
