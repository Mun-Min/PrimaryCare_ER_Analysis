# Primary Care & Emergency Room Utilization Analysis

<img align="middle" width="850" height="500" src="Images/cover_img.jpg">


#### 📊 Exploring whether primary care physician (PCP) availability reduces emergency room (ER) visit rates, and how socioeconomic factors influence this relationship.


## Table of Contents
1. [Project Overview](#project-overview)

2. [How to Access and Run the Project](#how-to-access-and-run-the-project)

3. [Notebook Summaries](#notebook-summaries)

4. [Project Limitations and Challenges](#project-limitations-and-challenges)

5. [PowerBI Dashboard](#power-bi-dashboard)

6. [Final Interpretation](#final-interpretation)
   
7. [External Sources](#external-sources)


---


## Project Overview

This project investigates a central research question:

#### Hypothesis: Is PCP density negatively associated with ER visits, and to what extent do socioeconomic variables moderate this relationship?

Using datasets from <u>PolicyMap</u>, <u>HRSA</u>, the <u>U.S. Census</u>, and <u>Data.gov</u>, we analyze population, insurance, income, and healthcare utilization patterns. The goal is to understand whether increasing access to primary care can meaningfully reduce ER utilization — especially in lower-income areas.

The analysis combines multiple years of data (2018–2023), cleans and merges datasets, performs exploratory analysis, builds regression models, and presents insights using a Power BI dashboard.

#### 📁 Project Structure

    PRIMARYCARE_ER_ANALYSIS/
        └─── Data_Files_Cleaned/
        │       income_insurance_merged.csv
        │       insurance_and_population_merged_2019_2023_us_cleaned.csv
        |       merged_regression_data.csv
        │       primary_care_physicians_2018_2021_cleaned.csv
        │       us_healthcare_visits_cleaned.csv
        │       us_household_median_income_cleaned.csv
        |
        └─── Data_Files_Uncleaned/
        │       Estimated_Population_2019_2023.csv
        │       Household_Median_Income_2019_2023.csv
        │       Insured_By_County_2019_2023_US.csv
        │       Primary_Care_Physicians_2018.csv
        │       Primary_Care_Physicians_2019.csv
        │       Primary_Care_Physicians_2020.csv
        │       Primary_Care_Physicians_2021.csv
        |       Uninsured_By_County_2019_2023_US.csv
        │       us_censusbureau_population_1990_2023.csv
        │       US_Healthcare_Visits.csv
        │
        └───Images/
        |       cover_img.jpg
        |       PowerBi_Sheet_1.png
        |       PowerBi_Sheet_2.png
        |
        ├── Data_Analysis_Notebook_1.ipynb
        ├── Data_Analysis_Notebook_2.ipynb
        ├── Data_Analysis_Notebook_3.ipynb
        ├── Data_Analysis_Notebook_4.ipynb
        ├── Regression_Analysis_Notebook.ipynb
        ├── PowerBI_Dashboard.pbix
        ├── README.md


## How to Access and Run the Project

#### Requirements: 

    - Python 3.12+

    - Jupyter Notebook or VS Code with Python/Jupyter Extensions

    Python libraries:

        - pandas

        - numpy

        - matplotlib

        - statsmodels

        - Power BI Desktop (for dashboard viewing)

#### Instructions: 

* Clone/download the repository.

* Open the .ipynb files in Jupyter or VS Code to view cleaning steps and analysis.

* Open [PowerBI_Dashboard.pbix](https://github.com/Mun-Min/PrimaryCare_ER_Analysis/blob/master/PowerBI_Dashboard.pbix) in Power BI Desktop to view visualizations.


## Notebook Summaries

📘 <span style="text-decoration: underline;">**Notebook 1 — Primary Care Physicians (2018–2021)**</span>

Sources: PolicyMap, HRSA

| Tasks     | Insights |
| -------- | ------- |
|Clean & merge PCP datasets (2018–2021)  | PCP supply increased slightly from 2018–2021    |
| Standardize variable names and handle missing values  | Growth rate is flattening — consistent with current workforce research   |
| Conduct early trend checks| Variation across states indicates uneven healthcare access     |

<br>

📘 <span style="text-decoration: underline;">**Notebook 2 — Insurance, Income & Population (2019–2023)**</span>

Sources: PolicyMap / Census: Decennial Census and American Community Survey (ACS)

| Tasks     | Insights |
| -------- | ------- |
|Combine insured, uninsured, and population datasets  | Most counties have 85–95% insured, limiting variance in statistical modeling    |
| Address missing or inconsistent values | Broad insurance access does not necessarily translate to primary care access    |
| Merge variables into a unified socioeconomic dataset| Lower-income counties often show high insurance rates due to Medicaid expansion     |

<br>

📘 <span style="text-decoration: underline;">**Notebook 3 — U.S. Healthcare Visits (2000–2018)**</span>

Source: Data.gov / U.S. Department of Health & Human Services

| Tasks     | Insights |
| -------- | ------- |
|Clean & restructure annual national healthcare visit counts  | Physician office visits dominate utilization    |
| Create trend visualizations | ER visits steadily rise across all years    |
| Prepare ER visits for regression analysis| Data limitation did not hinder the ability to gain meaningful insights     |

#### Important Data Limitation: The U.S. healthcare visits dataset has no state or county identifiers. It is national-level only, derived from survey/administrative summaries. This made it impossible to directly assess county-level ER use, limiting how precisely we can match local PCP supply to ER utilization patterns.

<br>

📘 <span style="text-decoration: underline;">**Notebook 4 — Income, Insurance & Moderation Analysis**</span>

Source: PolicyMap / Census: Decennial Census and American Community Survey (ACS)


| Tasks     | Insights |
| -------- | ------- |
| Build quartiles for median household income  | Insurance coverage remains high across all income quartiles    |
| Visualize insurance distribution by income group | Histograms and box plots show very little variation, explaining why income and insurance have low predictive power individually    |
| Evaluate socioeconomic variation    | Differences in ER utilization are more strongly explained by healthcare access, not insurance alone    |

<br>

📈 <span style="text-decoration: underline;">**Notebook 5 — Regression Analysis Notebook**</span>

Datasets Used:

* [income_insurance_merged.csv](https://github.com/Mun-Min/PrimaryCare_ER_Analysis/blob/master/Data_Files_Cleaned/income_insurance_merged.csv)

* [primary_care_physicians_2018_2021_cleaned.csv](https://github.com/Mun-Min/PrimaryCare_ER_Analysis/blob/master/Data_Files_Cleaned/primary_care_physicians_2018_2021_cleaned.csv)

* [us_healthcare_visits_cleaned.csv](https://github.com/Mun-Min/PrimaryCare_ER_Analysis/blob/master/Data_Files_Cleaned/us_healthcare_visits_cleaned.csv)

        Model: OLS Regression

        Dependent variable: ER_Visits_Rate


    | Key Findings     | Variable Interpretation |
    | -------- | ------- |
    | PCP_per_100k = -45.91  | More PCPs → fewer ER visits (key finding)    |
    | Median_Household_Income = -0.24 | Wealthier areas rely less on the ER     |
    | PCP × Income Interaction = +0.0004    | PCPs matter <i>most</i> in low-income counties    |
    | Percent_Insured = -376.02    | More insured → much fewer ER visits



    Conclusion:

    * PCP density is negatively associated with ER visits

    * Income moderates this relationship

    * Effect is strongest in low-income areas
                    
    This fully supports the hypothesis.


## Project Limitations and Challenges

1. Lack of county-level ER visit data

    * National dataset only — no geographic identifiers

    * Could not compare ER rates across counties

    * Forced analysis to rely on state-level inference instead of granular evaluation

2. High insurance uniformity

    * Most counties report >85% insured

    * Limited variance → weak predictor in models

3. Merging datasets from multiple agencies

    * Variable naming inconsistencies

    * Different time periods + measurement definitions

    * Required careful standardization

4. Model multicollinearity

    * Insurance & income correlated

    * High condition number flagged by regression output

    * Despite these constraints, the direction and magnitude of results remained stable across multiple tests.


## Power BI Dashboard

The dashboard summarizes the full analysis in two pages.

📌 Sheet 1 — Overview & Key Insights

<img align="middle" width="850" height="500" src="Images\PowerBi_Sheet_1.png">

<br>

Visuals included:

* Data disclaimer (healthcare visits = 2018 max)

* KPI Cards (Avg PCP per 100k, Avg ER visit rate, Avg median household income, Avg percent insured)

* Scatter Plot: ER Visit Rate vs PCP per 100k

* Bar Chart: ER visits (millions) by year (2000–2018)

<br>

📌 Sheet 2 — Socioeconomic Moderation Analysis

<img align="middle" width="850" height="500" src="Images\PowerBi_Sheet_2.png">

<br> 

Visuals included:

* Box plot: Percent insured by income quartile

* Line chart: Average PCP per year (2018–2021)

* Line chart: U.S. population (1990–2023)


## Final Interpretation

#### Does PCP supply reduce ER visits?

- Yes. Across thousands of observations, more PCPs per capita are strongly associated with fewer emergency room visits.

#### Do socioeconomic factors matter?

- Yes — income significantly moderates the relationship.

- In low-income areas, increasing PCP density has the strongest impact on reducing ER reliance.

- In higher-income areas, the relationship weakens because residents have more stable healthcare access pathways.

#### Overall conclusion:

- Improving primary care access — particularly in underserved, lower-income regions — is a powerful strategy for reducing avoidable ER utilization.

- Although insurance coverage is relatively high, insurance alone does not guarantee access — especially when the primary care workforce is not keeping pace with population growth. 
    
- National research reinforces this concern: the American Association of Medical Colleges (AAMC) projects a shortage of 14,800 to 49,300 primary care physicians by 2030, the Health Resources and Services Administration (HRSA) forecasts a deficit of more than 87,000 primary care clinicians by 2037, and additional studies predict more than 57,000 clinicians will be needed by 2040 due to aging populations and workforce attrition. 
    
- Rural areas are expected to be hit hardest, with only about 68% of primary care demand projected to be met in coming decades. These national trends align with our analysis, supporting the idea that limited access to primary care may be driving increased ER utilization. 
    
- To address these gaps, expanding residency funding, strengthening retention and burnout-prevention programs, adopting team-based care models with NPs and PAs, bolstering federal incentives such as National Health Service Corps (NHSC) programs, and expanding telehealth and mobile clinic capacity are all evidence-based strategies shown to improve access. 


## External Sources

* [US Primary Care Workforce Growth](https://pubmed.ncbi.nlm.nih.gov/39443342/)
  
* [State of the Primary Care Workforce, 2024](https://bhw.hrsa.gov/sites/default/files/bureau-health-workforce/state-of-the-primary-care-workforce-report-2024.pdf?)

* [Association of American Medical Colleges Physician Shortages Research](https://www.aamc.org/news/press-releases/new-research-shows-increasing-physician-shortages-both-primary-and-specialty-care?)

* [U.S. Department of Health & Human Services | Public Dataset](https://catalog.data.gov/dataset/visits-to-physician-offices-hospital-outpatient-departments-and-hospital-emergency-departm-6ef16)

* [PolicyMap Data Warehouse](https://www.policymap.com/)

