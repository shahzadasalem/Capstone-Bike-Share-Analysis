# Business Recommendations and Implementation Plan

**Project:** Cyclistic Bike-Share Case Study  
**Study period:** October 2025–September 2026, based on the monthly input filenames  
**Business objective:** Develop evidence-informed marketing strategies to encourage casual riders to purchase annual memberships.  
**Evidence:** Python notebook outputs and seven Tableau analyses documented in [Key Findings and Insights](Key_Findings_and_Insights.md) and [Exploratory Data Analysis](Exploratory_Data_Analysis.md).

> **Decision-making principle:** These are **recommendations to test**, not demonstrated conversion results. The available data records rides, not unique customers, purchasing decisions, marketing exposure, or profitability. Pricing, membership benefits, and permissions must be verified before campaign launch.

## Executive recommendation

Cyclistic should pursue **three coordinated membership-conversion experiments**: (1) weekend and spring/summer campaigns, (2) electric-bike-focused value messaging, and (3) targeted offers to identifiable repeat casual customers where appropriately permissioned customer-level data exists. These proposals align with observed differences in ride timing, duration, and bike type. A staged pilot with holdout groups will establish whether the strategies actually increase annual memberships.

### Evidence at a glance

| Observed measure | Casual rides | Member rides | Strategic implication |
|---|---:|---:|---|
| Segment share, notebook-aligned Tableau duration summary | **1,414,607 (34.52%)** | **2,683,396 (65.48%)** | Casual rides represent a substantial activity segment |
| Mean ride duration | **20.11 min** | **12.29 min** | Test value messages relevant to longer trips |
| Saturday ride volume | **~299K** | **~327K** | Saturday is a key casual-activity day |
| Monthly peak | **July: ~227K** | **August: ~341K** | Spring/summer offers may reach users during active periods |
| Electric-bike share within segment | **~61.5%** | **~54.0%** | Test electric-bike-specific membership messaging |

*Approximate values (`~`) come from rounded Tableau labels. The annual-volume worksheet totals 4,097,983 rides, 20 fewer than the notebook and duration-summary total of 4,098,003; the discrepancy is not resolved.*

---

## Recommendation 1 — Launch weekend and spring/summer membership campaigns

### Evidence from the analysis

- **Saturday is the busiest casual day:** approximately **299,000 casual rides**, compared with about **162,000** on Tuesday and Wednesday. This is approximately **85% higher** than either weekday, based on rounded labels.
- **The casual share of Saturday rides is approximately 48%**, versus approximately **27%** on Tuesday. The membership mix is therefore substantially more balanced on Saturday.
- **Casual riding peaks in July at approximately 227,000 rides**, versus approximately **17,000 in January**. These rounded counts indicate pronounced seasonality.
- Casual rides average **20.11 minutes**, compared with **12.29 minutes** for members, suggesting that longer-ride value propositions deserve testing.

### Proposed action

Run a campaign designed around **high-casual-activity periods**, with an initial pilot beginning during the spring ramp-up and additional creative or placements on weekends. Messaging should describe the actual annual membership benefits and fees clearly, rather than promising savings without a verified pricing comparison.

**Possible messages to test (illustrative, subject to pricing review):**

- “Ride more often? See whether an annual membership fits your routine.”
- “Planning more rides this season? Compare casual and member options.”
- “Make the most of your weekend rides—explore annual membership.”

### Implementation plan

1. **Validate campaign timing:** Use the full hourly/day/month data, not only rounded Tableau labels, to select test windows.
2. **Confirm the offer:** Marketing and finance should verify annual pricing, casual fees, included minutes, electric-bike surcharges, and any restrictions.
3. **Choose reachable placements:** Test approved in-app messages, ride-completion screens, station signage, or other channels that can reach casual customers.
4. **Randomise eligible exposure:** Assign comparable eligible users or sessions to campaign and holdout groups where technically and legally feasible.
5. **Evaluate incremental annual memberships:** Compare sign-ups attributable to the campaign, not simply clicks or riding volume.

### Hypothesis and measurement

**Hypothesis:** A seasonally timed, weekend-relevant membership message will produce a higher annual-membership conversion rate than the current/default message.

**Primary KPI:** Incremental annual membership conversion rate versus holdout.  
**Secondary KPIs:** New annual memberships, qualified click-through rate, acquisition cost per incremental membership, 30/90-day retention where measurable, and unsubscribes or complaints.

**Guardrail:** Do not infer that all weekend rides are recreational; trip purpose was not measured.

---

## Recommendation 2 — Make electric-bike membership value easier to understand

### Evidence from the analysis

- Electric bikes account for approximately **61.5% of casual rides**, compared with approximately **54.0% of member rides**—a difference of **7.5 percentage points**.
- In rounded Tableau counts, casual riders made approximately **870K electric-bike rides** versus **544K classic-bike rides**.
- Members also use electric bikes extensively (**~1,449K rides**), showing that electric-bike usage and annual membership are not mutually exclusive.

### Proposed action

Create a simple, accurate **electric-bike membership explainer** that compares what a casual user pays with what an annual member pays under real pricing rules. Make any extra per-minute, unlock, or usage fees visible. Pair the explainer with an experiment comparing electric-bike-focused messaging to general membership messaging.

### Implementation plan

1. **Audit current pricing and benefits:** Obtain official, up-to-date membership and electric-bike terms from the business team.
2. **Create comparison examples:** Use realistic ride scenarios, clearly labelling assumptions and avoiding guaranteed savings claims.
3. **Build two message variants:** One highlights electric-bike terms; the other explains general membership value.
4. **Test on eligible audiences:** Where allowed, display variants after electric-bike ride activity or in relevant digital channels; include a holdout group.
5. **Check segment-level outcomes:** Assess whether electric-bike-focused messaging changes actual membership purchase decisions.

### Hypothesis and measurement

**Hypothesis:** Clear electric-bike-specific membership information will increase annual membership conversion among eligible casual customers compared with generic membership information.

**Primary KPI:** Incremental annual membership conversion rate.  
**Secondary KPIs:** Pricing-page engagement, offer comprehension (if surveyed), cost per incremental membership, retention, and customer support complaints about fees.

**Guardrail:** The chart measures the **share of rides** made on electric bikes, not stated customer preference, unique electric-bike users, or expected savings.

---

## Recommendation 3 — Pilot permission-based, personalised conversion offers

### Evidence from the analysis

- Casual trips represent approximately **34.52% of the final analysed ride records**.
- Casual and member trips differ in mean duration (**20.11 vs 12.29 minutes**), hourly distribution (8 AM: **~3.6% casual vs ~7.4% member**, within each segment), and weekly pattern (casual Saturday peak vs member Tuesday peak).
- These differences suggest that a single generic message may not be equally relevant across riding contexts, but **do not establish which individuals will convert**.

### Proposed action

If Cyclistic maintains **separate, appropriately permissioned customer-level records**, identify eligible casual customers who have used the service repeatedly and test tailored membership information. For example, users with multiple eligible rides could receive a factual cost comparison based on their own usage, subject to privacy, consent, and applicable policy.

**Important data boundary:** The current trip dataset has a `ride_id`, **not a customer ID**. It cannot identify repeat casual riders, track individual conversion, or calculate customer lifetime value. This proposal depends on additional authorised systems.

### Implementation plan

1. **Confirm data access and consent:** Work with privacy, legal, and CRM teams to establish what identifiers and communication permissions are available.
2. **Define eligibility without overreach:** Specify a transparent rule for repeat casual activity using authorised data; avoid sensitive or intrusive profiling.
3. **Design relevant messages:** Test usage-based value explanations against a general membership message, with no unverified savings claims.
4. **Randomise treatment and holdout:** Use a controlled test to separate campaign effects from natural membership sign-ups.
5. **Monitor quality, not only volume:** Evaluate acquisition cost, incremental conversion, early cancellations, and retention.

### Hypothesis and measurement

**Hypothesis:** Permission-based messages relevant to observed repeat use will outperform generic membership promotions on incremental annual sign-ups.

**Primary KPI:** Incremental annual membership conversion rate among eligible customers.  
**Secondary KPIs:** Incremental memberships, cost per incremental acquisition, retention, opt-outs, and customer complaints.

**Guardrail:** Do not claim the current analysis has already identified repeat riders or measured their likelihood of subscribing.

---

## Prioritised action plan

The schedule below is a **proposed pilot sequence**, not a record of activities already completed.

| Phase | Suggested timing | Owner(s) | Deliverable | Decision gate |
|---|---|---|---|---|
| **1. Validate evidence and offers** | Weeks 1–2 | Analytics, marketing, pricing | Reconciled chart counts; verified membership terms; audience/consent review | Data and offer approved |
| **2. Build campaigns** | Weeks 3–4 | Marketing, design, CRM/product | Weekend/seasonal creative; electric-bike explainer; experiment plan | Creative, targeting and instrumentation approved |
| **3. Run pilots** | Weeks 5–8 | Growth marketing, analytics | Controlled campaign tests with holdouts | Sufficient sample and tracking quality |
| **4. Evaluate and iterate** | Weeks 9–10 | Analytics, finance, marketing | Incremental conversion, cost, retention and guardrail readout | Scale, revise, or stop each campaign |

**Sequencing:** Start with broad, low-dependency weekend/seasonal messaging and electric-bike information. Run personalised CRM tests only after customer-level data access and permissions are confirmed.

## Measurement framework

| Metric | Definition | Required data | Why it matters |
|---|---|---|---|
| **Incremental conversion rate** | Difference in annual-membership purchase rate between treatment and holdout | Campaign assignment + customer purchase events | Main test of causal campaign impact |
| **Incremental memberships** | Extra annual memberships attributable to campaign versus control | Same as above | Business outcome |
| **Customer acquisition cost** | Campaign cost ÷ incremental new members | Marketing spend + incremental memberships | Cost efficiency |
| **Retention** | Share of newly acquired members remaining active or subscribed after a defined period | Customer subscription/activity data | Quality and sustainability of acquisition |
| **Click-through/engagement** | Interactions ÷ eligible impressions | Campaign delivery analytics | Diagnostic, not a substitute for conversion |
| **Complaints/opt-outs** | Negative response rates | Support/CRM records | Customer-experience guardrail |

Set baseline values, test sample sizes, minimum detectable effects, and stopping rules **before** launch. No numerical lift or ROI target is asserted here because the case-study data does not contain marketing outcomes, membership pricing, or costs.

## Risks, dependencies and mitigations

| Risk or dependency | Consequence | Proposed mitigation |
|---|---|---|
| **Missing station data:** 2,073,763 of 6,171,785 initial records excluded (~33.60%) | Possible selection bias in analysed ride patterns | Compare excluded and retained records by segment/bike type/month before scaling conclusions |
| **20-ride mismatch between Tableau worksheets** | Reduced confidence in exact totals | Reconcile worksheet filters, null handling, and source connection |
| **No customer-level identifiers in trip data** | Cannot target repeat riders or observe conversion | Use separate authorised CRM and subscription data only if available |
| **No pricing or cost fields** | Cannot calculate customer savings or marketing ROI | Obtain approved pricing and finance data before value claims |
| **Rounded Tableau counts** | Minor imprecision in reported peak volumes | Use underlying verified aggregations for campaign decisions |
| **Seasonal confounding** | Summer uplift may occur without marketing | Randomised holdout and seasonally comparable analysis |
| **Consent and communication preferences** | Privacy/compliance and trust risks | Privacy review, permissions, frequency limits, opt-outs |

## What success would look like

The project is successful when Cyclistic can answer **which of the three tested approaches produces additional annual memberships at an acceptable acquisition cost**, while preserving customer experience and retention. The strongest strategy should be selected based on measured outcomes rather than on ride patterns alone.

## Final recommendation to stakeholders

> **Prioritise targeted, measurable experiments—not assumptions about rider intent.** Use the observed weekend, seasonal, duration and electric-bike patterns to design relevant membership messages, then validate their effectiveness with controlled conversion data.

## Supporting documentation

- [Business Problem and Objectives](Business_Problem_and_Objectives.md)
- [Data Sources and Methodology](Data_Sources_and_Methodology.md)
- [Data Cleaning and Transformation](Data_Cleaning_and_Transformation.md)
- [Exploratory Data Analysis](Exploratory_Data_Analysis.md)
- [Key Findings and Insights](Key_Findings_and_Insights.md)
- [Jupyter Notebook](../notebooks/all_trips_v2.ipynb) (once uploaded to the repository)

**Data attribution:** Cyclistic is a fictional Google Data Analytics Capstone company. The trip data originates from the public [Divvy system data](https://divvybikes.com/system-data). The large cleaned CSV is intentionally not hosted in the repository.
