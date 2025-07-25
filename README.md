# Temperature Data Analysis Project

This project presents a detailed analysis and visualization of global and city-level temperature data using KNIME workflows. The tasks address statistical analysis, classification, comparison with global averages, and interactive visualizations.

---
 
##  Dataset Overview
- **City Data:** Includes yearly average temperature by country.
- **Global Data:** Includes yearly global average temperature.
- Missing values were handled before any calculations.
- The maximum year found in the data: **2015**
## Handling Missing Values
Null values in the city-level temperature dataset were handled by applying forward filling using "Missing Value"  Fill with mean in KNIME.


##  Task Breakdown

###  **Task 1: Calculate Country-Wise Average Temperature**
- Computed using the `GroupBy` node on the `avg_temp` column grouped by `country`.
###  **Task 2: Classify Temperature Levels (Low / Mid / High)**

#### A. Static Classification
- Used **fixed thresholds**:
- Low: 0–30°C
- Mid: 30–60°C
- High: 60–90°C
#### B. Dynamic Classification
- Used min/max values from dataset:
We used two formulas to divide the temperature range into three equal parts:

## Equation 1 – Mid_Low:
- Mid_Low = Min_Temp + (Max_Temp - Min_Temp) / 3
which marks the upper limit of the "Low" range.
It represents the boundary between Low and Mid temperatures.

## Equation 2 – Mid_High:
- Mid_High = Min_Temp + 2 * (Max_Temp - Min_Temp) / 3
Which marks the upper limit of the "Mid" range.
It represents the boundary between Mid and High temperatures.
## Rule Engine Logic
The following KNIME Rule Engine logic was used to classify each country's temperature:
- $avg_temp$ <= $Mid_Low$ => "Low"
- $avg_temp$ <= $Mid_High$ => "Mid"
- $avg_temp$ > $Mid_High$  => "High"
This method ensures the classification adapts to your dataset — it’s not limited by hardcoded thresholds. This makes  solution more flexible, accurate, and applicable to future datasets with different temperature ranges.
###  **Task 3: Country-Year Deviation from Global 24-Year Avg
 For each country and year, compute the deviation from global average temperature over the last 24 years.
- Global Reference Period:
Max year = 2015 → Range: 1992–2015
Steps:
Filter global dataset to years >= 1992 and less than or equal 2015
Compute global average temperature over this period: 9.04°C
Group country-year temperatures using GroupBy
Subtract global average from each country’s yearly avg

###  **Task 4: Top 5 Countries with Highest Deviation
Rank countries by their average difference from global temperature.
Steps:
Group country-year differences by Country
Aggregate using Mean
Sort by descending order
Use Top K Selector for top 5
###  **Task 5: Histogram of Global Yearly Temperatures
Visualize temperature trend over time.
Steps:
Group by Year
Aggregate global avg_temp (mean)
Use JavaScript Histogram node for plotting


###  **Task 6: City vs Global Temperature Trend (Cairo Example)
 Compare temperature trend of one city with global average.
Steps:
Group city_data by Year for Cairo
Group global_data by Year
Join both tables on Year
Visualize using Line Plot (JavaScript) with 2 Y-axes





