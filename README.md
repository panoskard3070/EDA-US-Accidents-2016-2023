# **EDA-US-Accidents-2016-2023**  

This project performs an Exploratory Data Analysis (EDA) on the US Accidents dataset covering the years 2016–2023. The main objective was to understand how car accidents evolve across time, geography, weather conditions, and time-related patterns, using real-world large-scale data (~7.5 Million records). The analysis follows a structured data-science pipeline, emphasizing data cleaning, feature engineering, statistical exploration, and visualization-driven storytelling.  

# **Steps & Methodology**  
As I wanted to take a sample of 500k rows from the whole dataset to check the Time Duration Distribution of an incident lasted, I utilised the GPU by using CUDF. Also I noticed that not all rows included time on date. I wanted to keep as much data as possible so dropping 700k rows was not an option. So I worked for general statistics in the whole dataset using pandas-chunk-approach while time analysis performed on a cudf DataFrame. Of course another option was to take a sample of 50k rows of each chunk the concat them at the end.  

## **Step 1:Data Import & Load**  
*  Imported the dataset in chunks due to large file size ~7.5M rows by Pandas   
*  Imported the dataset in GPU by using CUDF  

## **Step 2: Data Inspection**  
*  Initial exploration of dataset shape, columns, missing values, and variable types  
*  Identified redundant or irrelevant columns to be removed in later stages  

## **Step 3: Data Cleaning**  
*  Missing values for Temperature(F), Visibility(mi), and Wind_Speed(mph) were filled per state, depending on mean/median stability per state (mask threshold 0.02)  
*  Duplicates removed and date columns formatted as proper datetime objects  
*  Designed a custom clean_chunk function for automated column dropping, filling by criterion, dropping na's, duplicates and datetime conversion  

## **Step 4: Feature Engineering**  
*  Extracted time-based features from Start_Time such as: Year, Month, Day of Week, Hour of Day  
*  Created bins for temperature ranges to assess weather–accident correlations  
*  Generated new features for crash duration  
*  Designed a custom feature_engineering_chunk function for automated feature engineering all chunks while in loop  

## **Step 5: Statistical & GroupBy Analysis**  
Performed grouped statistics by:  
*  State  
*  County  
*  Temperature bins  
*  Year, Month and Day of Week  
*  Time bins   

## **Step 6: Visualization**  
*  Created bar plots and a histogram  
*  Accidents per state and county  
*  Temporal 2016–2022 evolution, Month and Day of Week total accidents  
*  Temperature effect  
*  Hour Bin and accidents by Hour of Day  
*  Hour with most accidents per State  
*  Accident Duration Distribution in Hours  

## **Step 7: Conclusion**  
**Key findings** from the analysis:  
*  Top 3 states with most accidents: California, Florida, Texas (Top counties: Los Angeles, Miami-Dade, Harris)  
*  Crashes increased from ~400K in 2016 to ~1.75M in 2022.  
*  December is the month with the highest accident frequency, followed by November.  
*  Friday has the most crashes, showing an upward trend from Monday to Friday.  
*  Most accidents occur at 10–18°C, indicating fewer trips in extreme weather (cold or hot).  
*  Peak hours: 7–8 AM and 4–5 PM, consistent with commuting traffic.  
*  The average crash duration (sample of 500K) is between 35–45 minutes.

#  **Tools & Libraries**  
Python 3.11
Numpy  
Pandas  
Cudf  
Matplotlib  
Seaborn  
Time  
OS  
Kagglehub  
From Google Colab, userdata  

# **Project Insights**  
This analysis demonstrates:  
*  How to efficiently handle large-scale datasets with chunk processing.  
*  How data-driven reasoning can reveal behavioral and temporal patterns in traffic data.  

# **Author**
Panagiotis Kardatos  
Mathematician, Aspiring Machine Learning Engineer  
