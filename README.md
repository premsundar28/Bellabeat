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

### 3.1 Tools & Environment
I utilized **Python** within **Jupyter Notebooks** for a reproducible and documented workflow.
*   **Data Processing:** `Pandas` for merging 12 raw CSV files and `NumPy` for numerical validation.
*   **Visual Analysis:** `Matplotlib` and `Seaborn` for identifying patterns and correlations.

### 3.2 Cleaning & Transformation Pipeline
I implemented a standardized pipeline to ensure data integrity:
1.  **Data Consolidation:** Merged datasets from two time periods to create a single source of truth for each metric (Activity, Sleep, Weight).
2.  **Naming Conventions:** Standardized all headers to `snake_case` (e.g., `TotalSteps` -> `total_steps`) for consistency.
3.  **Temporal Consistency:** Converted date strings into `datetime` objects, enabling time-series analysis.
4.  **Deduplication:** Verified and removed redundant records (e.g., handling duplicates in `sleepDay`).
5.  **Quality Check:** Identified that ~8.2% of total records contained zero steps, which I categorized as "non-wear days".

### 3.3 Visual Analysis & Interpretations

#### A. Distribution of Core Metrics
![Distribution of Daily Activity Metrics](images/distribution_histograms.png)
*   **Interpretation:** The **Total Steps** and **Distance** histograms show a right-skewed distribution with a significant peak at zero. This confirms "non-wear" days where the tracker was likely not used. **Calories** follows a near-normal distribution, indicating most users burn between 1,800 and 2,800 kcal daily.

#### B. Correlation Analysis
![Correlation Heatmap](images/correlation_heatmap.png)
*   **Interpretation:** 
    *   **High Impact:** A near-perfect correlation (0.98) exists between **Total Steps** and **Total Distance**.
    *   **Calorie Burn:** **Very Active Minutes** and **Total Steps** show the strongest positive correlation with calories burned, highlighting these as key metrics for weight management features.
    *   **Sedentary Insight:** **Sedentary Minutes** has a weak negative correlation with calories, suggesting that simply reducing inactivity is a vital "nudge" for user health.

### 3.4 Process Validation (Guiding Questions)
*   **Tools Choice:** Python was chosen for its efficiency in merging millions of rows (especially heart rate data) and its superior visualization capabilities.
*   **Data Integrity:** Verified that unique user counts (33 users) remained consistent across merged activity files.
*   **Cleaning Documentation:** All steps—from header standardization to duplicate handling—are documented in the `EDA.ipynb` notebook.
*   **Verification:** Used `df.info()` and summary statistics to ensure structural integrity and absence of nulls in key analytical columns.

### 3.5 Phase 3 Deliverable
**Processed Data Summary:**
*   **Consolidation:** 12 raw CSVs merged into 6 master DataFrames.
*   **Formatting:** Applied `snake_case` headers and parsed all date-time strings.
*   **Validation:** 0 duplicates in `dailyActivity`; identified non-wear patterns (8.2% zeros).

---

## Phase 4: Analyze

### 4.1 Data Organization & Formatting
To perform this analysis, I organized the data into a consolidated schema where the `dailyActivity` dataframe served as the central table.
*   **Aggregated View:** Data is aggregated by `id` and `activity_date` to provide a daily snapshot of user behavior.
*   **Formatting:** All datasets have been standardized to use `snake_case` column names and `datetime` objects for date fields, ensuring seamless joining and time-series plotting.

### 4.2 Key Discoveries & Surprises
*   **Sedentary Dominance:** Users spend a significant portion of their day sedentary (avg. ~990 minutes/day). Even active users often have high sedentary time, suggesting a "weekend warrior" or "gym-only" active profile rather than consistent movement.
*   **Non-Wear Days:** Approximately 8.2% of days have zero steps, indicating users often take the device off for extended periods or forget to charge/wear it.
*   **Lack of Manual Logging:** 96.6% of distance records are automated, meaning users rely almost entirely on the device's auto-detection. Features requiring manual input (like water or weight logging) may have low engagement.

### 4.3 Trends & Relationships
My analysis highlighted several critical relationships:
*   **Activity vs. Calories:** There is a strong positive correlation between `total_steps` / `very_active_minutes` and `calories`. High-intensity activity is the most efficient driver of calorie burn.
*   **Sedentary Impact:** There is a negative correlation between sedentary minutes and calorie burn. Reducing sedentary time—even without intense exercise—positively impacts daily energy expenditure.
*   **Consistency:** The "non-wear" days suggest a gap in habit formation. Users who track consistently likely see better results, but the device needs to encourage daily wear.

### 4.4 Business Insights (Answering the Questions)
*   **Focus on Consistency:** Since non-wear days are common, Bellabeat could introduce "streak" features or battery reminders to encourage 24/7 wear.
*   **Nudge Inactivity:** Given the high sedentary time, the Bellabeat app can benefit from "inactivity alerts" or "movement breaks" to break up long periods of sitting, independent of scheduled workouts.
*   **Automate Everything:** The lack of manual logging suggests that Bellabeat's "Spring" bottle (smart tracking) is a better product strategy than relying on users to manually log water intake in the app.

### 4.5 Guiding Questions & Answers
*   **How should you organize your data to perform analysis on it?**
    Data should be organized in a long format, aggregated by user and day, to allow for trend analysis over time.
*   **Has your data been properly formatted?**
    Yes, verified in Phase 3 with standard naming and date types.
*   **What surprises did you discover in the data?**
    The extremely high percentage of sedentary minutes and the significant number of days with zero activity (non-wear).
*   **What trends or relationships did you find in the data?**
    Steps and very active minutes are the strongest predictors of calorie burn; sedentary time is negatively correlated with health metrics.
*   **How will these insights help answer your business questions?**
    They point directly to feature recommendations: automated tracking, inactivity nudges, and gamification of consistency.

### 4.6 Deliverable
**Summary of Analysis:**
*   Identified that sedentary time is the dominant user state.
*   Confirmed that high intensity and step count are the primary drivers of calorie expenditure.
*   Uncovered a "consistency gap" with ~8% non-wear days.
*   Concluded that automated tracking is superior to manual logging for this user base.

---

## Phase 5: Share

### 5.1 Visualization Strategy
In this phase, I translated my technical findings into high-level, executive-ready visualizations. My goal was to use **contrast** and **color** to highlight the most actionable insights for the Bellabeat executive team.
*   **Contrast:** Used clear color distinctions in heatmaps and histograms to differentiate between sedentary (neutral/cool) and active (vibrant/warm) states.
*   **Focus:** Focused on the "Activity vs. Inactivity" story, showing exactly where users lose momentum.

### 5.2 The Story: "Bridging the Consistency Gap"
The data tells a story of users who have the tools but lack the consistent habits to maximize their health outcomes.
1.  **The Sedentary Trap:** Most users spend over 16 hours a day sedentary, regardless of their activity level.
2.  **The Automation Preference:** Users prefer features that require zero effort (auto-tracking steps) over manual logs (water, weight).
3.  **The Tracking Gap:** Frequent "non-wear" days (8.2%) interrupt data flow and habit reinforcement.

### 5.3 Guiding Questions & Answers
*   **Were you able to answer the business questions?**
    Yes. I identified specific usage trends (sedentary dominance and non-wear gaps) that directly inform Bellabeat’s marketing and product strategy.
*   **What story does your data tell?**
    It’s a story of "passive tracking." Users are engaged with the device but aren't yet using it to actively break sedentary patterns.
*   **How do your findings relate to your original question?**
    My original goal was to find growth opportunities. The discovery of high sedentary time and non-wear days reveals a clear opportunity to differentiate Bellabeat via better "consistency features" and "active lifestyle nudges."
*   **Who is your audience?**
    Urška Sršen and Sando Mur (Bellabeat Founders/Executives). The best way to communicate is through concise, visual, and action-oriented slides.
*   **Is your presentation accessible to your audience?**
    Yes, I ensured high-contrast visuals and avoided technical jargon, focusing instead on business impact and user behavior.

### 5.4 Deliverable
**Supporting Visualizations & Key Findings:**
*   **Correlation Heatmap:** Proving that Very Active Minutes are the most efficient way to burn calories.
*   **Distribution Histograms:** Identifying the ~8% non-wear day gap.
*   **Key Finding:** Automation is preferred. Bellabeat should emphasize products like the Leaf or Time that offer "invisible" and continuous tracking.

---

## Phase 6: Act

### 6.1 Final Conclusion
The analysis of smart device usage reveals that while users are capable of high activity, they are predominantly sedentary and struggle with consistent daily wear. The key to Bellabeat's growth lies in **shifting from passive tracking to active nudging**. Users need devices that don't just record their history but actively interrupt sedentary patterns and reward consistency.

### 6.2 High-Level Recommendations
Based on the data, I propose the following strategies for the Bellabeat marketing and product teams:

1.  **"Break the Cycle" Campaign (Marketing):**
    *   **Insight:** Users spend ~990 minutes/day sedentary.
    *   **Action:** Market the *Leaf* and *Time* as "wellness guardians" that gently vibrate to remind users to move after 30 minutes of inactivity. Position this as a stress-relief and metabolism-boosting feature, not just a fitness reminder.

2.  **Gamify Consistency (Product):**
    *   **Insight:** 8.2% of days are "non-wear" days.
    *   **Action:** Introduce a "Consistency Score" or "Wellness Streak" in the Bellabeat app. Reward users for simply wearing the device 7 days a week, regardless of activity intensity. This builds the habit of daily use.

3.  **The "Invisible" Advantage (Product/Marketing):**
    *   **Insight:** Manual logging (weight/distance) is rarely used (<4%).
    *   **Action:** Emphasize Bellabeat's advantage in *automated* wellness. Promote the *Spring* water bottle's ability to track hydration automatically, contrasting it with the tedious manual logging required by competitors.

### 6.3 Next Steps
*   **Stakeholder Presentation:** Present these findings to Urška Sršen and the executive team using the prepared visualizations.
*   **Expand Analysis:** Request access to demographic data (age, location) to refine these recommendations for specific user segments.
*   **A/B Testing:** Propose a pilot program to test if "inactivity nudges" actually reduce sedentary time in a small user group.

### 6.4 Guiding Questions & Answers
*   **What is your final conclusion based on your analysis?**
    Users need active intervention (nudges) to break sedentary habits and features that automate tracking to ensure consistency.
*   **How could your team and business apply your insights?**
    By updating marketing copy to focus on "wellness automation" and prioritizing app features that reward daily device wear.
*   **What next steps would you or your stakeholders take based on your findings?**
    Launch a targeted marketing campaign focused on the benefits of reducing sedentary time and develop a "streak" feature for the app.
*   **Is there additional data you could use to expand on your findings?**
    Yes, demographic data and sleep quality metrics would allow for more personalized recommendations.

### 6.5 Deliverable
**Top High-Level Insights:**
1.  **Sedentary Behavior is the Enemy:** Marketing should pivot from just "fitness" to "fighting the sitting epidemic."
2.  **Consistency > Intensity:** Building the habit of wearing the device daily is the first hurdle to retention.
3.  **Automation is King:** Any feature requiring manual input will likely fail; prioritize smart, sensor-based tracking.



