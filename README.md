# Cyclistic Bike-Share Case Study

### Understanding rider behaviour to support annual membership growth

**Data analytics portfolio project | Python / JupyterLab | Tableau Desktop | Business analytics**

> **Business question:** How do casual riders and annual members use Cyclistic bikes differently, and how can those differences inform marketing strategies that encourage annual membership?

## Project overview

Cyclistic is a fictional Chicago-based bike-share company featured in the Google Data Analytics Capstone case study. In the business scenario, the marketing team wants to increase annual memberships because annual members are considered more profitable than casual riders.

This project compares the riding patterns of **casual riders** and **annual members** using historical bike-share trip records. It examines ride volume, duration, time of day, day of week, seasonality, and bike type, then translates those findings into testable marketing recommendations.

**My role:** Junior Data Analyst, Cyclistic marketing analytics team (case-study scenario).  
**Business stakeholder:** Marketing leadership and Cyclistic executives.  
**Analysis period:** October 2025–September 2026, **as labelled in the Tableau workbook**; the underlying CSV date range still needs independent confirmation.  
**Data source:** Public Divvy historical trip data, used for the fictional Cyclistic scenario.  
**Analysis unit:** Trips/rides, **not unique riders**.

## Business objectives

1. Identify the main differences between casual and member riding behaviour.
2. Explain how those patterns could inform membership marketing.
3. Recommend **three actionable, measurable strategies** to encourage casual riders to consider annual membership.

## Tools and methods

| Tool | Role in the project |
| --- | --- |
| **Python / JupyterLab** | Data preparation and exploratory analytical workflow |
| **Tableau Desktop** | Visual comparison of member and casual riding patterns |
| **PowerPoint** | Presentation of findings, business implications, and recommendations |
| **GitHub** | Documentation and publication of the portfolio case study |

The analytical workflow covers preparing trip records, comparing membership segments, reviewing ride-duration statistics, exploring hourly/weekly/monthly patterns, assessing bike types, and presenting recommendations. Exact Python cleaning operations should be checked against the final notebook before being described as completed steps.

## Dataset and analytical fields

The analysis uses anonymized trip records from the [Divvy historical trip data](https://divvybikes.com/system-data) source. The case-study analysis references these fields and derived measures:

- `ride_id` — trip identifier
- `member_casual` — rider membership category
- `rideable_type` — bicycle category (such as classic or electric)
- `started_at`, `ended_at` — trip timestamps
- Ride duration in minutes, plus derived ride-start hour, weekday, and month

**Data access:** Download the relevant monthly source files from Divvy rather than committing large raw datasets to this repository. The exact source months and any filtering or cleaning rules should be confirmed against the original files and notebook.

## Key findings

The Tableau analyses show **approximately 4.1 million rides** across the two membership groups.

| Metric | Casual rides | Member rides | Interpretation |
| --- | ---: | ---: | --- |
| Annual ride count (volume chart) | **1,414,599** | **2,683,384** | Members account for approximately **65.48%** of rides; casual rides account for **34.52%**. |
| Average ride duration | **20.11 min** | **12.29 min** | Casual rides last **7.82 minutes**, or **63.6%**, longer on average. |
| Median ride duration | **12 min** | **9 min** | The typical casual trip is longer. |
| Electric-bike share of group rides | **~61.5%** | **~54.0%** | Electric bikes account for a larger share of casual rides. |

### 1. Members generate most rides

Members account for nearly two-thirds of the rides shown in the annual volume chart. Casual rides still represent more than one-third of total activity, making this a substantial segment for marketing research and testing.

### 2. Casual rides are longer and more variable

The average casual ride lasts **20.11 minutes**, compared with **12.29 minutes** for members. The duration summary also reports greater variation for casual trips (standard deviation **42 minutes** versus **25 minutes** for members, rounded). This suggests different usage patterns, although **trip purpose cannot be established from trip records alone**.

### 3. Members are more active on weekdays; casual riding increases on weekends

Member ride volume peaks around **Tuesday (~440K)** and **Wednesday (~437K)**. Casual rides peak on **Saturday (~299K)**, around **85% above** the approximately **162K** casual rides on Tuesday or Wednesday. The weekday pattern is consistent with some routine travel, while the weekend pattern may indicate more discretionary use; neither trip purpose is directly observed.

### 4. The groups differ by hour of day

At **8 AM**, approximately **7.4%** of member rides start, compared with **3.6%** of casual rides. Both groups show substantial activity at **5 PM** (approximately **10.9%** of member rides and **9.5%** of casual rides). These percentages describe the **within-group distribution of rides by hour**, not the share of all customers.

### 5. Riding peaks in summer

Casual ride volume reaches approximately **227K in July**, while member rides reach approximately **341K in August**. Casual volume falls to approximately **17K in January**, showing particularly strong seasonality. The monthly chart is arranged by calendar month; the associated year for each month should be checked against the source data.

### 6. Electric bikes are important to both segments

Electric bikes account for approximately **870K casual rides** and **1,449K member rides**. Their share is higher within the casual segment (**61.5%**) than within the member segment (**54.0%**). These are **shares of rides**, not survey-based rider preferences.

## Three business recommendations

### Recommendation 1 — Test spring and summer membership campaigns

**Evidence:** Casual activity rises during warmer months and peaks in July.  
**Action:** Test membership messages and offers as demand increases in spring and summer.  
**Measure:** Casual-to-member conversion rate, new memberships, and acquisition cost.

### Recommendation 2 — Tailor messages to weekend and longer-trip use

**Evidence:** Casual rides peak on Saturdays and are longer on average.  
**Action:** Test weekend-focused campaigns that explain the value of annual membership for riders who use the service repeatedly.  
**Measure:** Campaign response, membership sign-ups, and subsequent member engagement.

### Recommendation 3 — Explain electric-bike membership value

**Evidence:** Electric bikes account for approximately **61.5%** of casual rides.  
**Action:** Test messaging that clearly explains actual membership pricing, electric-bike terms, and potential value for frequent users.  
**Measure:** Membership conversion among eligible electric-bike users and retention.

**Implementation principle:** Treat these as **hypotheses to test**, not proven conversion drivers. A/B testing and customer-level, permissioned campaign data would be needed to establish marketing effectiveness.

## Project deliverables

This README is the entry point to the full project. The following files are planned for the repository; add links once each file has been prepared and uploaded:

| Deliverable | Planned location |
| --- | --- |
| Business problem and objectives | `reports/Business_Problem_and_Objectives.md` |
| Data sources and methodology | `reports/Data_Sources_and_Methodology.md` |
| Data cleaning and transformation | `reports/Data_Cleaning_and_Transformation.md` |
| Exploratory data analysis | `reports/Exploratory_Data_Analysis.md` |
| Detailed findings | `reports/Key_Findings_and_Insights.md` |
| Business recommendations | `reports/Business_Recommendations.md` |
| Conclusion and limitations | `reports/Conclusion_and_Limitations.md` |
| Tableau workbook | `tableau/` |
| Tableau chart images | `visualizations/` |
| Jupyter notebook | `notebooks/` |
| Executive presentation | `presentation/` |

## Limitations and validation notes

- **Ride counts are not unique customer counts.** One person may contribute many trips.
- **Trip purpose is unknown.** Commute and leisure interpretations are hypotheses based on temporal patterns, not observed labels.
- **No customer-level conversion data** is available in the presented summaries, so the recommendations have not been shown to increase sign-ups.
- **A small count discrepancy remains:** the annual volume chart totals **4,097,983 rides**, while the duration summary totals **4,098,003 rides** (a **20-ride difference**). These figures are reported as displayed and should be reconciled before final publication.
- **The date range requires validation:** October 2025–September 2026 comes from the Tableau workbook name and has not been independently confirmed against source CSV dates.
- **Chart formatting:** some Tableau labels show currency symbols even though the measures represent ride counts or minutes; those symbols should not be interpreted as money.
- **Source and cleaning reproducibility:** final notebook, file inventory, filters, and row-level quality checks should be reviewed before claiming the analysis is fully reproducible.

## Conclusion

Cyclistic's casual and member rides differ in volume, trip duration, weekly and hourly activity, seasonality, and bike type. These differences offer a useful basis for **targeted marketing experiments**. The next step is to validate the underlying data and test whether tailored seasonal, weekend, and electric-bike messaging can generate more annual memberships efficiently.

## Source and attribution

- **Case-study scenario:** Google Data Analytics Capstone — Cyclistic bike-share case study (fictional company).
- **Trip-data provider:** [Divvy historical trip data](https://divvybikes.com/system-data).
- **Analysis and visualisations:** Tableau workbook and project presentation supplied for this case study.

*This is an independent portfolio case study and is not an official Cyclistic or Divvy business report.*
