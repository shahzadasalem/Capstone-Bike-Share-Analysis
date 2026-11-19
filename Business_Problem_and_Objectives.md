# Business Problem and Objectives

**Project:** Cyclistic Bike-Share Case Study  
**Portfolio focus:** Understanding differences between casual and annual-member ride patterns to inform membership-growth marketing  
**Role:** Junior Data Analyst, Cyclistic marketing analytics team *(fictional case-study role)*

> **Central business question:** How do annual members and casual riders use Cyclistic bikes differently?

## 1. Company background

Cyclistic is a **fictional Chicago-based bike-share company** used in the Google Data Analytics Capstone case study. The scenario describes a network of **5,824 bicycles and 692 docking stations**. These are figures from the *case-study narrative*, not a verified description of Divvy's current fleet.

Cyclistic offers different ways to access its bicycles:

- **Casual riders:** People using single-ride or day-pass options.
- **Annual members:** People purchasing an annual membership.

The project uses **public Divvy historical trip records** as the analytical dataset for the fictional Cyclistic business scenario. Cyclistic and Divvy should not be treated as the same company in business conclusions.

## 2. Business context and problem

In the case-study scenario, Cyclistic's leadership considers **annual members more profitable than casual riders**. Consequently, the marketing team wants to increase the number of annual memberships, particularly by encouraging existing casual users to consider joining.

However, the team cannot design a well-targeted conversion strategy based only on this objective. It first needs to understand **how ride activity differs across the two membership categories**. Differences in ride frequency at particular times, trip duration, seasonality, and bicycle type may help the team identify relevant messages and campaign windows.

**The business problem is therefore:**

> Cyclistic needs evidence about differences in casual and member riding behaviour to design and test marketing strategies intended to convert casual riders into annual members.

The analysis does **not** directly measure why individual people ride, how often the same person returns, whether a particular casual rider is likely to convert, or the financial return of a membership campaign. Those questions require additional customer-level and commercial data.

## 3. Stakeholders and decision to support

| Stakeholder | Role in the case study | What they need from this analysis |
| --- | --- | --- |
| **Lily Moreno** | Director of Marketing | A clear, evidence-based explanation of segment differences and actionable marketing proposals |
| **Cyclistic marketing analytics team** | Analytical support | Reliable comparisons, clear visualisations, and transparent assumptions |
| **Cyclistic executive team** | Business decision-makers | A concise business case for which campaign ideas to test and how success should be measured |

**Decision to support:** Which marketing approaches should Cyclistic **test first** to encourage casual riders to purchase annual memberships?

## 4. Project aim

To analyse twelve months of historical bike-share trips, compare **casual** and **member** ride patterns, and translate the observed differences into **three practical, measurable marketing recommendations**.

The Tableau workbook is named for **October 2025–September 2026**. That period is treated as a **workbook label**, not yet as an independently verified range of underlying trip timestamps.

## 5. Specific analytical objectives

### Objective 1 — Compare ride volume and segment mix

- Calculate the number and percentage of rides attributed to casual riders and annual members.
- Establish the relative contribution of each segment to total recorded trips.
- Avoid interpreting ride counts as counts of distinct customers.

**Business relevance:** Indicates the scale of casual riding activity that membership campaigns might address.

### Objective 2 — Compare ride duration

- Compare mean and median ride durations by membership type.
- Examine quartiles and variability to describe how trip lengths differ.
- Distinguish observed trip-length differences from unobserved trip purpose.

**Business relevance:** Helps tailor membership-value messaging to the kinds of journeys reflected in each segment's recorded trips.

### Objective 3 — Identify when each segment rides

- Compare ride patterns by **hour of day**, **day of week**, and **month**.
- Identify peak periods for casual and member activity.
- Consider whether seasonal or weekend campaigns warrant testing.

**Business relevance:** Helps prioritise campaign timing and audience context.

### Objective 4 — Compare bicycle types

- Examine classic-bike and electric-bike ride volumes by membership category.
- Calculate each bike type's share **within** casual and member rides.

**Business relevance:** Helps determine whether electric-bike-specific membership messaging is worth testing.

### Objective 5 — Recommend and evaluate marketing actions

- Synthesize the behavioural evidence into **three testable marketing recommendations**.
- Propose appropriate performance indicators and validation steps.
- State the limits of what trip-level descriptive analysis can establish.

**Business relevance:** Connects analysis to an actionable marketing decision rather than ending with charts alone.

## 6. Analytical scope

| Dimension | Included in this project | Not established by the available summaries |
| --- | --- | --- |
| **Population** | Recorded bike-share trips categorised as casual or member | Number of unique people in each segment |
| **Time** | Twelve-month period labelled October 2025–September 2026 in the Tableau workbook | Verified minimum and maximum trip dates in source CSVs |
| **Measures** | Ride counts, shares, durations, time-of-use patterns, bike type | Revenue, profit, lifetime value, acquisition cost |
| **Approach** | Descriptive comparison and visual exploration | Causal explanation of riding behaviour |
| **Output** | Tableau visuals, key findings, presentation, campaign hypotheses | Demonstrated increases in membership conversion |

**Data source:** Public Divvy historical trip data used in the Cyclistic capstone exercise.  
**Primary tools:** Python/JupyterLab for data-preparation and analytical work; Tableau Desktop for visualisation; PowerPoint for communicating results.

The exact data-cleaning operations and source date coverage should be confirmed from the final notebook and raw-data inventory before publishing a reproducible methodology.

## 7. Early evidence motivating the objectives

The project's Tableau summaries report the following descriptive patterns:

| Observation | Tableau result | Why it matters to the business question |
| --- | --- | --- |
| **Substantial casual activity** | **1,414,599 casual rides** versus **2,683,384 member rides** in the annual volume chart | Casual trips represent approximately **34.52%** of the recorded activity, making this a meaningful segment to understand |
| **Longer casual trips** | Average duration **20.11 minutes** for casual rides versus **12.29 minutes** for member rides | Supports testing messages relevant to riders who make longer trips |
| **Weekend concentration** | Casual rides peak on **Saturday (~299K)** | Suggests weekend campaign timing may be worth testing |
| **Seasonal concentration** | Casual rides peak in **July (~227K)** | Suggests spring and summer may be useful campaign windows |
| **Electric-bike use** | Electric bikes represent approximately **61.5%** of casual rides | Supports testing clear electric-bike membership-value messages |

These findings describe **rides**, not unique users or confirmed customer motivations. The annual volume chart totals **4,097,983** rides, while a separate duration summary totals **4,098,003**; the **20-ride discrepancy** requires reconciliation before final numerical publication.

## 8. Marketing hypotheses to test

The descriptive analysis motivates three **hypotheses**, rather than proving any campaign will work:

1. **Seasonal and weekend outreach:** Membership messaging delivered when casual ride activity is high may generate more qualified interest than untargeted outreach.
2. **Electric-bike value messaging:** Clear explanations of applicable membership pricing and electric-bike terms may resonate with casual riders who use electric bikes.
3. **Repeat-use conversion messaging:** If permissioned customer-level data becomes available, offers tailored to repeat casual users may outperform generic promotions.

These are hypotheses because the current charts do not provide customer identity, campaign exposure, conversion outcomes, or controlled comparisons.

## 9. Success criteria and measurement plan

A useful business outcome is **more annual memberships acquired efficiently and retained over time**. To evaluate that outcome, Cyclistic would need campaign and membership records beyond the ride-level summaries.

| KPI | How to use it | Additional data required |
| --- | --- | --- |
| **Casual-to-member conversion rate** | Compare conversion among eligible, reached casual users | Customer-level membership status and campaign exposure |
| **New annual memberships** | Count sign-ups attributed to a campaign using an appropriate measurement design | Membership transaction records |
| **Customer acquisition cost** | Compare campaign spend per acquired annual member | Campaign spending and attributable sign-ups |
| **Retention / renewal** | Assess whether acquired members remain members over time | Membership history |
| **Incremental conversion lift** | Compare test and control groups, preferably via A/B testing | Randomised assignment or a defensible comparison design |

**Suggested evaluation approach:** Define a target audience, test a clear membership-value message against a control, track conversions over an agreed period, and review acquisition cost and retention before scaling the campaign.

## 10. Expected project deliverables

1. A documented business problem and set of analytical objectives.
2. A transparent description of data sources, cleaning, and methodology.
3. Tableau visualisations comparing casual and member ride behaviour.
4. A concise set of evidence-supported findings and limitations.
5. Three actionable marketing recommendations with proposed measures of success.
6. An executive presentation and GitHub portfolio documentation.

## 11. Assumptions and limitations

- **Fictional scenario:** Cyclistic, the stated fleet size, the stakeholder names, and the profitability premise come from the case-study narrative; they are not verified facts about today's Divvy business.
- **Trips are not customers:** Multiple rides may belong to the same individual.
- **Purpose is not observed:** Weekday peaks can be *consistent with* commuting, but the trip data do not establish commuting or leisure intent.
- **Profitability is assumed by the scenario:** This analysis does not calculate profit differences between membership categories.
- **Conversion cannot be measured here:** No linked customer-level marketing or membership outcomes are shown.
- **Date range remains to be checked:** The workbook filename indicates October 2025–September 2026; source timestamps have not been independently verified.
- **Counts need reconciliation:** Tableau views differ by 20 rides, as noted above.

## 12. Business question restated

**How can Cyclistic use the observed differences in casual and annual-member ride patterns to prioritise and test marketing campaigns that encourage annual membership?**

This question keeps the project focused on a defensible progression: **describe the data → identify behavioural differences → form marketing hypotheses → test business impact**.

---

### Sources and project references

- **Google Data Analytics Capstone:** Cyclistic case-study scenario (fictional business and stakeholder brief).
- **[Divvy historical trip data](https://divvybikes.com/system-data):** Public trip-data source used for the case-study analysis.
- **Project artifacts:** `README.md`, `Cyclistic_Opening_Slides.pptx`, `Cyclistic_Complete_Case_Study_Presentation.pptx`, and the supplied Tableau workbook and graph screenshots.

*Independent educational portfolio analysis; not an official report issued by Cyclistic or Divvy.*
