#Cyclistic Bike-Share Case Study

This repository contains the files, code, and documentation for a case study analyzing historical bike trip data from Cyclistic, a Chicago-based bike-share company. The goal is to identify trends in how casual riders and annual members use the bikes differently, with the aim of informing marketing strategies to convert casual riders into annual members.
This project was completed as part of a data analytics portfolio, using spreadsheets for initial cleaning, SQL for deeper manipulation and analysis, and Tableau for visualization.

Table of Contents

1)Project Overview

2)Business Problem

3)Data Sources

4)Tools and Technologies

5)Data Cleaning and Preparation
  --Using Microsoft Excel
  --Using SQL in BigQuery
6)Exploratory Data Analysis

7)Quarterly Analysis

8)Full-Year Analysis

9)Key Findings and Insights

10)Visualizations and Dashboard

1)Project Overview:

Cyclistic is a bike-share program in Chicago with over 5,800 bicycles and 600 docking stations. The company offers flexible pricing plans: single-ride passes, full-day passes (for casual riders), and annual memberships (for members). Financial analysis shows that annual members are more profitable than casual riders. The marketing team aims to maximize annual memberships by converting casual riders.
This case study focuses on the question: How do annual members and casual riders use Cyclistic bikes differently? Insights from this analysis will help design targeted marketing strategies.
The project analyzes 12 months of historical trip data of year 2022 to uncover usage patterns.

2)Business Problem

Primary Goal: Design marketing strategies to convert casual riders into annual members.

Key Questions:

How do annual members and casual riders use Cyclistic bikes differently?
Why would casual riders buy annual memberships?
How can Cyclistic use digital media to influence casual riders to become members?


Stakeholders: Director of Marketing, Cyclistic Executive Team, Marketing Analytics Team.
Business Task: Analyze historical data to identify trends and provide insights for targeted marketing.
3)Data Sources:
The data is reliable, original, comprehensive, current, and cited (ROCCC criteria):

Primary Data: Cyclistic's historical bike trip data for the last 12 months (2022), publicly available from Motivate International Inc. under this license.

12 CSV files, one per month (e.g., 2022-01_divvy_trip-data.csv to 2022-12_divvy_trip-data.csv).
Fields: ride_id, rideable_type, started_at, ended_at, start_station_name, start_station_id, end_station_name, end_station_id, start_lat, start_lng, end_lat, end_lng, member_casual.

Secondary Data: Bike station data from the City of Chicago, available here.
Data is anonymized, structured in rows (trips) and columns, with each trip having a unique ride_id.

Note: Data privacy prohibits using personally identifiable information, so no analysis on repeat usage or geographic connections to residences.
4)Tools and Technologies:

Spreadsheets: Microsoft Excel for initial cleaning and basic transformations.
SQL: BigQuery for handling large datasets, further cleaning, aggregation, and analysis.
Visualization: Tableau for creating dashboards and interactive visualizations.
Version Control: GitHub for hosting the repository.
Other: Google Cloud Storage for uploading large CSV files to BigQuery.
Using Microsoft Excel
For each monthly CSV file:

Converted to XLSX format.
Formatted started_at and ended_at as custom DATETIME (yyyy-mm-dd h:mm:ss).
Added columns:

ride_length: =ended_at - started_at, formatted as TIME (HH:MM:SS).
ride_date: =DATE(YEAR(started_at), MONTH(started_at), DAY(started_at)), formatted as YYYY-MM-DD.
ride_month: Month number (e.g., 1 for January).
ride_year: Year (e.g., 2022).
start_time and end_time: Extracted from started_at/ended_at, formatted as TIME.
day_of_week: =WEEKDAY(started_at, 1) (1=Sunday, 7=Saturday), formatted as number.


Saved cleaned files as new CSVs.

Using SQL in BigQuery

Uploaded CSVs to Google Cloud Storage, then imported to BigQuery as datasets.
Initial queries: Checked for duplicates, nulls, and distinct counts (e.g., trip counts per month). Summer months (June-August) had the highest trips.
Created quarterly tables (e.g., 2022_Q1, 2022_Q2) using UNION DISTINCT to combine months, adding a quarter column.
Further transformations:

Cast day_of_week to STRING and updated values (e.g., '1' to 'Sunday') using CASE WHEN.


Deleted original monthly tables to save storage costs.
SQL files: initial_setup_query.sql, cyclistic_cs_initial_setup_pt2.sql, cyclistic_cs_initial_setup_pt3.sql.

6)Exploratory Data Analysis
Analysis was conducted quarterly and then for the full year. SQL queries focused on totals, averages/medias, modes, and groupings by rider type.
7)Quarterly Analysis

Example for Q1 (Jan-Mar 2021): 278,118 trips (66% members, 34% casual).
Metrics explored:

Total trips by rider type.
Average/median ride lengths (medians used due to outliers; casual: ~18 min, members: ~10 min).
Max ride lengths (outliers in casual rides, e.g.,s 22 hours, often docked bike).
Busiest days (Saturday for both).
Median ride length per day (higher for casual on weekends).
Total rides per day.
Popular start stations (casual favor waterfront/tourist areas; members favor downtown/retail).


SQL files: analysis_2022_Q1.sql, analysis_2022_Q2.sql, etc.

Full-Year Analysis

Combined quarters into a full_year table.
Metrics:

Total trips: 55% members, 45% casual.
Seasonal trends: Peak in Q3 (summer); drop in Q1 (winter). Members dominate except in Q3.
Median ride length: Casual consistently longer (~2x members).
Day of week: Casual prefer Saturdays; members prefer Wednesdays. U-shaped pattern in ride lengths (longer weekends).
Bike type: Classic bikes preferred (members: 60%, casual: 56%); docked bikes only used by casual (cause of outliers).
Stations: Casual rides concentrated at few waterfront stations; member rides more distributed.


SQL file: analysis_full_year.sql.

Key Findings and Insights

Rider Proportions: Members take more trips overall, but casual dominate in summer(July,August,September)
Ride Duration: Casual rides are longer, especially on weekends (leisure-oriented).
Day Patterns: Casual: "Weekend warriors" with variable durations. Members: Consistent mid-week use (commuting).
Bike Preferences: Classic > Electric; docked bikes skew casual data.
Station Usage: Casual favor tourist spots (e.g., Streeter Dr & Grand Ave); members favor urban areas (e.g., Clark St & Elm St).
Hypotheses: Casual use for entertainment/tourism; members for commuting/errands.

Visualizations and Dashboard

Tableau Dashboard: Interactive views of trends, maps, and comparisons. View on Tableau Public.

Includes area charts for seasonal trends, bar charts for ride lengths/days, maps for stations.


Presentation: Slides summarizing analysis and recommendations. View Slides (replace with actual link if available).






Recommendations

Recommendations
Based on insights:

Target Weekend Leisure Riders: Promote memberships with weekend perks (e.g., extended ride times) via digital ads near popular casual stations.
Seasonal Campaigns: Focus summer marketing on casual riders at waterfront areas to highlight membership benefits like cost savings for frequent use.
Address Docked Bike Outliers: Investigate docked bike usage; offer incentives for classic/electric to casual riders. Use geo-targeted media to convert tourist-heavy users.




