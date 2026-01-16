# Bellabeat Data Analysis Case Study

## Project Overview
In this case study, I assume the role of a junior data analyst at Bellabeat, a high-tech manufacturer of health-focused products for women. Although Bellabeat is a successful small company, they have the potential to become a larger player in the global smart device market. 

**Urška Sršen**, Bellabeat’s cofounder and Chief Creative Officer, believes that analyzing smart device fitness data could help unlock new growth opportunities. I have been tasked with analyzing smart device data to gain insight into how consumers are using their smart devices. These insights will help guide the company's marketing strategy.

## About Bellabeat
Bellabeat is a high-tech company that manufactures health-focused smart products for women. Founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women.
*   **Mission:** Empower women with knowledge about their own health and habits.
*   **Key Products:** Bellabeat app, Leaf tracker, Time watch, Spring water bottle, and Bellabeat membership.

---

## Phase 1: Ask

### 1.1 Business Task
The primary objective of this project is to analyze smart device usage data from non-Bellabeat smart devices. The goal is to identify trends in consumer behavior and apply these insights to a specific Bellabeat product. Ultimately, these findings will inform high-level marketing recommendations to help Bellabeat unlock new growth opportunities.

### 1.2 Key Stakeholders
*   **Urška Sršen:** Bellabeat’s cofounder and Chief Creative Officer. Primary stakeholder interested in data-driven insights.
*   **Sando Mur:** Mathematician and Bellabeat’s cofounder; key member of the executive team.
*   **Bellabeat Marketing Analytics Team:** A team of data analysts responsible for guiding Bellabeat’s marketing strategy.

### 1.3 Guiding Questions
To guide my analysis, I am addressing the following key questions:
*   What is the problem I am trying to solve?
*   How can these insights drive business decisions?
*   What are some existing trends in smart device usage?
*   How could these trends apply to Bellabeat customers?
*   How could these trends help influence Bellabeat marketing strategy?

### 1.4 Key Tasks
1.  **Identify the business task:** Analyze non-Bellabeat smart device usage to improve Bellabeat's marketing strategy.
2.  **Consider key stakeholders:** Focus on the needs of Urška Sršen, Sando Mur, and the broader marketing team.

### 1.5 Deliverable
A clear statement of the business task: Analyze smart device usage data to identify trends in how consumers use non-Bellabeat smart devices, then apply these insights to a specific Bellabeat product to provide high-level recommendations for the company's marketing strategy.

---

## Phase 2: Prepare

### 2.1 Data Sources Used
For this analysis, I am using the **FitBit Fitness Tracker Data** (CC0: Public Domain), which is available on Kaggle via Mobius. This dataset contains personal fitness tracker data from thirty Fitbit users who consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring.

### 2.2 Guiding Questions & Answers

*   **Where is your data stored?**
    The data is stored locally in my project directory across two main folders: `mturkfitbit_export_3.12.16-4.11.16` and `mturkfitbit_export_4.12.16-5.12.16`.
*   **How is the data organized? Is it in long or wide format?**
    The data is organized in several CSV files. Most of the files (like `dailyActivity_merged.csv` and `heartrate_seconds_merged.csv`) are in **long format**, where each row represents a specific time point or day for an individual user ID.
*   **Are there issues with bias or credibility in this data? Does your data ROCCC?**
    *   **Reliable:** Low. The sample size is only 30 users, which is small for a representative population.
    *   **Original:** Low. This is a third-party dataset collected via Amazon Mechanical Turk.
    *   **Comprehensive:** Medium. It covers activity, sleep, and heart rate, but lacks demographic information like age or gender, which is critical for Bellabeat's female-focused strategy.
    *   **Current:** Low. The data is from 2016 (nearly 10 years old), so usage trends may have shifted significantly.
    *   **Cited:** High. The source is clearly identified and publicly available.
*   **How are you addressing licensing, privacy, security, and accessibility?**
    The dataset is CC0 (Public Domain), ensuring no licensing issues. All data is anonymized (User IDs only), maintaining privacy. I am working with the data in a secure local environment.
*   **How did you verify the data’s integrity?**
    I performed initial data profiling to check for consistent formatting, unique user counts (confirming 30+ users), and identifying any obvious outliers or missing values.
*   **How does it help you answer your question?**
    By analyzing daily steps, calories, and sleep patterns, I can identify common behavior "nudges" (e.g., when users are most active) that can be integrated into Bellabeat's app features.
*   **Are there any problems with the data?**
    Yes—the small sample size, age of the data, and lack of demographic context (specifically gender) are significant limitations. I will need to acknowledge these when presenting recommendations.

### 2.3 Key Tasks
1.  **Download and store data:** Completed. Files are organized in the project folder.
2.  **Identify organization:** Verified long format for primary activity files.
3.  **Determine credibility:** Identified limitations in sample size and currency (ROCCC analysis).

### 2.4 Deliverable
A description of all data sources used, including the specific datasets selected for analysis:

*   **dailyActivity_merged.csv:** Contains daily summary data for steps, distance, intensities (minutes and distance), and calories. This is the most comprehensive daily file.
*   **dailyCalories_merged.csv:** Focuses specifically on the total calories burned per day.
*   **dailyIntensities_merged.csv:** Breaks down daily activity into sedentary, lightly active, fairly active, and very active minutes/distances.
*   **sleepDay_merged.csv:** Provides daily records of sleep, including the number of sleep sessions, total minutes spent asleep, and total time spent in bed.
*   **weightLogInfo_merged.csv:** Tracks weight in kilograms and pounds, BMI, and whether the entry was a manual report.
*   **Source Summary:** The primary data source is the FitBit Fitness Tracker Data (2016), consisting of 18 CSV files detailing the daily habits of 30+ Fitbit users.

---

## Phase 3: Process

### 3.1 Tools Chosen
For this analysis, I am using **Python** (specifically libraries like **Pandas**, **NumPy**, and **Matplotlib/Seaborn**) within a Jupyter Notebook environment (`EDA.ipynb`). 
*   **Why?** Python is highly efficient for handling large datasets, performing complex transformations, and creating reproducible data cleaning scripts. Jupyter Notebooks allow for a clear, step-by-step documentation of the process.

### 3.2 Initial Data Profiling Findings (Daily Activity)
A preliminary profile of the `dailyActivity_merged.csv` dataset revealed the following insights regarding data quality and relationships:

*   **High Correlations:**
    *   **Calories** is highly correlated with `TotalSteps`, `TotalDistance`, `TrackerDistance`, and `VeryActiveMinutes`.
    *   **Activity Intensities:** `FairlyActiveMinutes` and `ModeratelyActiveDistance` are strongly linked, as are `LightlyActiveMinutes` and `LightActiveDistance`.
    *   **Distance Metrics:** `TotalDistance` and `TrackerDistance` show near-perfect correlation with `TotalSteps`.

*   **Data Quality Observations (Zero Values):**
    *   **TotalSteps/Distance:** Approximately **8.2-8.3%** of entries are zeros, likely representing days the tracker was not worn.
    *   **LoggedActivitiesDistance:** **96.6%** zeros, suggesting that very few users manually log their distance-based activities.
    *   **SedentaryActiveDistance:** **91.3%** zeros.
    *   **High Intensity Activity:** `VeryActiveMinutes` (**43.5%**) and `FairlyActiveMinutes` (**40.9%**) have a significant number of zero values, indicating many users have days without high-intensity exercise.

*   **Distribution:** `ActivityDate` is uniformly distributed, confirming a consistent period of data collection.

### 3.3 Visual Verification
I generated histograms to visualize the distribution of key activity metrics:
![Distribution of Daily Activity Metrics](images/distribution_histograms.png)
*   **Steps & Distance:** Both show a slightly right-skewed distribution, consistent with the finding that some days have zero activity (8%+ zeros).
*   **Calories:** Shows a more normal distribution, centered around the 2000-2500 range.

### 3.4 Guiding Questions & Answers

*   **Have you ensured your data’s integrity?**
    Yes. I checked for unique user counts to ensure consistency with the dataset description and verified that all data falls within the expected 2016 timeframe.
*   **What steps have you taken to ensure that your data is clean?**
    1.  **Duplicate Removal:** Identified and removed duplicate rows (especially in sleep data).
    2.  **Formatting:** Converted date/time strings into proper `datetime` objects.
    3.  **Naming:** Standardized column names to `snake_case` or `PascalCase` for consistency across all merged tables.
    4.  **Handling Nulls:** Identified columns with missing data (like 'Fat' in weight logs) and decided whether to drop them or fill them based on their impact.
*   **How can you verify that your data is clean and ready to analyze?**
    I used summary statistics (`df.describe()`) to check for outliers and confirmed that the count of unique IDs remains consistent across related datasets after cleaning.
*   **Have you documented your cleaning process?**
    Yes, all cleaning steps are documented both in this README and through code comments in my Jupyter Notebook.

### 3.3 Key Tasks
1.  **Check for errors:** Found and removed duplicates in the sleep dataset.
2.  **Choose tools:** Set up a Python environment with necessary data science libraries.
3.  **Transform data:** Merged daily activity and sleep datasets into a single dataframe for correlation analysis.
4.  **Document process:** Maintained a record of all transformations performed.

### 3.4 Deliverable
Documentation of any cleaning or manipulation of data:
*   Initial cleaning performed in `EDA.ipynb`.
*   Combined `dailyActivity` and `sleepDay` datasets on `Id` and `Date`.
*   Standardized date formats across all CSVs to `YYYY-MM-DD`.
*   Removed 3 duplicate entries from the `sleepDay_merged.csv` file.

