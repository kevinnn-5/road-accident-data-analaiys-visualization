EDA ASSIGNMENT 2 - ROAD ACCIDENT ANALYSIS (TEAM 6)
===================================================

PROJECT
-------
Clean, explore and visualise a road accident dataset (1,500 accidents, 8 Tamil Nadu
cities, 2023-2024) and build machine-learning models that predict accident severity
(Minor / Serious / Fatal).

NOTE: the dataset is randomly generated for practice. Findings are illustrative only.


FILES
-----
EDA_Assignment_2_Team6.ipynb
    Full notebook with code and outputs: data quality check, cleaning, feature
    engineering, 14 charts, 5 models, feature importance, key insights.

Team 6 - original data ,cleaned data.xlsx
    Sheet "Original Data"    : raw messy data (1,560 rows, 15 columns)
    Sheet "Cleaned Data"     : cleaned data (1,500 rows, 23 columns)
    Sheet "Cleaning Summary" : every problem found and the fix applied

EDA_Assignment_2_Report.pdf
    Written report (8 pages): objective, data, cleaning, EDA, modelling, conclusions.

EDA_Assignment_2_Presentation.pptx
    7-slide presentation with editable charts.

model_comparison.csv
    Test-set scores of the 5 models (CV accuracy, test accuracy, weighted
    precision/recall/F1, macro F1), sorted best first.

feature_importance.csv
    Permutation importance of each feature for the best model (drop in macro-F1
    when the feature is shuffled), with standard deviation.


HOW TO RUN (Google Colab)
-------------------------
1. Open https://colab.research.google.com and upload EDA_Assignment_2_Team6.ipynb
   (File > Upload notebook).
2. Upload "Team 6 - original data ,cleaned data.xlsx" using the folder icon on the
   left (Upload to session storage). It must be in the same folder as the notebook.
3. Runtime > Run all.
4. The notebook re-creates road_accidents_cleaned.csv, model_comparison.csv and
   feature_importance.csv in the Colab file panel. Download them before the
   session ends.
Libraries used: pandas, numpy, matplotlib, seaborn, scikit-learn, openpyxl
(all pre-installed in Colab).


DATA DICTIONARY (cleaned data)
------------------------------
accident_id       Unique accident id
date, time        When the accident happened
city              Tiruchirappalli, Chennai, Coimbatore, Madurai, Salem, Erode, Tirunelveli, Vellore
road_type         National Highway / State Highway / City Road / Rural Road
weather           Clear / Rain / Fog / Cloudy / Unknown
light_condition   Daylight / Dusk/Dawn / Dark
vehicle_type      Two-Wheeler / Car / Bus / Truck / Auto Rickshaw / Pedestrian Involved
cause             Over-speeding, Drunk Driving, Distracted Driving, Wrong-Side Driving,
                  Poor Road Condition, Signal Violation, Unknown
severity          Target: Minor / Serious / Fatal
num_vehicles      Vehicles involved
num_casualties    People injured or killed (not used for prediction: data leakage)
driver_age        Driver age (invalid values replaced by the median)
driver_gender     Male / Female / Unknown
speed_limit       Posted speed limit (km/h)
Derived columns   hour, year, month, month_name, weekday, is_weekend, age_group, time_of_day


CLEANING STEPS
--------------
1. Removed 60 duplicate rows (1,560 -> 1,500)
2. Trimmed spaces and standardised case in text columns
3. Merged city aliases (Trichy = Tiruchirappalli); M/F -> Male/Female
4. Parsed 3 different date formats into one
5. Set impossible ages (<16 or >90) and casualty counts (<0 or >20) to missing
6. Imputed: median (age; casualties by severity; speed limit by road type),
   'Unknown' for missing categories, hour inferred from light condition
7. Added derived time and age-group features


KEY RESULTS
-----------
- 13.3% of accidents are fatal; 28% happen between 17:00 and 20:59 (peak 19:00)
- Fatal share: 23% in the dark vs 8% in daylight; 24% on National Highways;
  26% (fog) and 20% (rain) vs 10% in clear weather
- Two-wheelers are in 42% of accidents; over-speeding is the most common cause;
  drunk driving (26% fatal) and over-speeding (22% fatal) are the most dangerous
- Best model: Gradient Boosting - 63.7% test accuracy, macro-F1 0.57
  (baseline of always predicting "Minor": about 53%)
- Top predictors: cause, vehicle type, light condition, road type
