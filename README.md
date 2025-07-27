 uber-fares-analysis27688

My Work (https://drive.google.com/drive/folders/1SaPHFnKxcvI1UeHY6SXlBnqHMtuLf6Py?usp=drive_link)

Uber Fares Dataset Analysis

This project analyzes the Uber Fares dataset from Kaggle to explore fare patterns, peak hours, and geographic distribution using Python (for data cleaning & feature engineering) and Power BI (for interactive visualization).

 Project Structure
- `data/`: Raw and cleaned datasets (`uber.csv`, `uber_fares_cleaned.csv`, `uber_fares_features.csv`)
- `eda.py`: Python script for exploratory data analysis & cleaning
- `screenshots/`: Documentation of each project stage (data loading, cleaning, dashboard)
- `uber_fares_dashboard.pbix`: Power BI dashboard
- `report.md`: Analytical report with findings and recommendations

Tools Used
- Python (Pandas, Matplotlib, Seaborn)
- Power BI Desktop
- GitHub

How to run
1. Clone this repository
2. Run `eda.py` to generate cleaned datasets
3. Open `uber_fares_dashboard.pbix` in Power BI Desktop to explore the dashboard

Key Insights
- Average fares by hour, weekday, and month
- Peak vs off-peak fare patterns
- Geographic distribution of pickups



Methodology – Data Preparation
Downloaded dataset from Kaggle (uber.csv)
Loaded & cleaned in Python (pandas)
Removed missing values and unrealistic fares
Exported:
uber_fares_cleaned.csv
 screenshot of your Python notebook or code
import pandas as pd

print(" Step 1: Load dataset")
 a) Load dataset
df = pd.read_csv('uber.csv')

print(" Loaded dataset")
print("Shape:", df.shape)
print("Columns:", df.columns.tolist())
print("Data types:\n", df.dtypes)

print("\n Step 1c: Initial data quality check")
print("Missing values per column:\n", df.isnull().sum())
print("\nDescriptive statistics:\n", df.describe(include='all'))

d) Handle missing values and remove invalid data
print("\n Step 1d: Clean data")
df_cleaned = df.dropna(subset=['fare_amount', 'pickup_datetime'])
df_cleaned = df_cleaned[df_cleaned['fare_amount'] > 0]

print("New shape after cleaning:", df_cleaned.shape)
print("Missing values after cleaning:\n", df_cleaned.isnull().sum())

e) Export cleaned dataset
df_cleaned.to_csv('uber_fares_cleaned.csv', index=False)
print(" Exported: uber_fares_cleaned.csv")

  Feature Engineering
print("\n Step 3: Feature engineering")
 Convert pickup_datetime
df_cleaned['pickup_datetime'] = pd.to_datetime(df_cleaned['pickup_datetime'], errors='coerce')
df_cleaned = df_cleaned.dropna(subset=['pickup_datetime'])

 Add new columns
df_cleaned['hour'] = df_cleaned['pickup_datetime'].dt.hour
df_cleaned['day'] = df_cleaned['pickup_datetime'].dt.day
df_cleaned['month'] = df_cleaned['pickup_datetime'].dt.month
df_cleaned['weekday'] = df_cleaned['pickup_datetime'].dt.weekday

 Peak hours flag
peak_hours = [7,8,9,16,17,18]
df_cleaned['is_peak'] = df_cleaned['hour'].apply(lambda x: 1 if x in peak_hours else 0)

print(" Added features: hour, day, month, weekday, is_peak")
print("Columns now:\n", df_cleaned.columns.tolist())

 Save enhanced dataset
df_cleaned.to_csv('uber_fares_enhanced.csv', index=False)
print(" Exported: uber_fares_enhanced.csv")

print("\n DONE! Your cleaned and enhanced datasets are ready for Power BI")
 Methodology – Feature Engineering
Extracted: Hour, day, month, weekday
Created:is_peak feature for peak vs non-peak hours
Prepared dataset for visualization
 screenshot of dataset columns in Power BI

Visual: histogram or boxplot of fare_amount


Visual Analysis in Power BI
Line chart: average fare by hour

Bar chart: trips by weekday & month

Box plot: fare distribution

Map: pickup location
Results – Key Findings
Peak hours → higher average fares
More trips on Fridays & weekends
Dense pickup clusters around city center & airports
Clear seasonality in monthly patterns

Conclusion
 Builtcleaned & enhanced dataset
Handled missing values & removed outliers
Added analytical features: hour, day, month, weekday, peak/off-peak Created interactive Power BI dashboard
Visualized fare patterns (histograms, box plots, time series)
Added filters & drill-downs for deeper exploration
 Identified key patterns
Higher fares during morning & evening peak hours
More trips on Fridays & weekends
Hotspots around airports & downtown areas
 Design suggestion
Title: Conclusion (bold, large font)
 sections with small icons 
Optionally add
Screenshot of dashboard (right side)
Footer: “Uber Fares Dataset Analysis | July 2025”
Recommendations
 Use surge pricingin peak hours
Maximize revenue by adjusting fares during morning and evening rush hours
Focus marketing on high-demandareas
Target areas with high ride frequency, like city centers and airports
 Add external data (weather/events) for deeper analysis
Incorporate weather, holidays, and events to improve demand forecasting
Tip
Use 3 bullet points only (as above) for clarity
Add icons (clock for surge, pin for location, cloud for weather) to make it visual
Use green checkmark or colored icons to draw attention

Author: Mutamba Alice  
Instructor:Eric Maniraguha  
Course:INSY 8413 - Introduction to Big Data Analytics
