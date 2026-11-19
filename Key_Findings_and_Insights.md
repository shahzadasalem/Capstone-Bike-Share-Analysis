# Key Findings and Insights

**Project:** Cyclistic Bike-Share Case Study  
**Business question:** How do casual riders and annual members use bike-share differently, and what opportunities could encourage casual riders to become annual members?  
**Study period:** October 2025–September 2026, according to the source-file names  
**Tools:** Python, pandas, JupyterLab, Tableau Desktop  
**Source documents:** [Exploratory Data Analysis](Exploratory_Data_Analysis.md) · [Data Sources and Methodology](Data_Sources_and_Methodology.md) · [Data Cleaning and Transformation](Data_Cleaning_and_Transformation.md)

> **How to read this report:** Findings describe **rides**, not unique riders. `~` indicates a value read from a rounded Tableau chart. Interpretations about commuting, leisure, or conversion potential are hypotheses, not observed customer motivations or outcomes.

## Executive summary

The notebook's final processed dataset contains **4,098,003 rides**. Its matching Tableau duration summary reports **2,683,396 member rides (65.48%)** and **1,414,607 casual rides (34.52%)**. Members contribute most trips, but casual activity is substantial and differs by duration, hour, weekday, season, and bike type.

**Five headline insights**

1. **Members account for roughly two-thirds of trips; casual riders account for one-third.** This establishes the scale of casual activity but not the number of prospective customers.
2. **Casual rides last longer.** Their mean duration is **20.11 minutes**, versus **12.29 minutes** for member rides.
3. **Weekly and hourly rhythms differ.** Member rides are relatively concentrated on weekdays and at 8 AM; casual rides are more concentrated on Saturdays and in afternoon/late-night hours.
4. **Summer is especially important for casual rides.** Casual volume peaks at **~227K in July**, compared with **~17K in January**.
5. **Electric bikes are a larger part of the casual ride mix.** **~61.5%** of casual rides use electric bikes, compared with **~54.0%** of member rides.

**Overall implication:** Cyclistic should **test segmented membership marketing**, particularly weekend/seasonal messaging, electric-bike value explanations, and targeted offers where permissioned customer-level data exists.

---

## Finding 1 — Members generate most recorded rides

**Tableau visual:** Annual rides by membership category.

| Segment | Annual-volume chart | Approximate share |
|---|---:|---:|
| Member | 2,683,384 | 65.48% |
| Casual | 1,414,599 | 34.52% |
| **Total** | **4,097,983** | **100%** |

### Three evidence-based observations

1. **Member rides dominate total volume:** around **65.5%** of the annual-volume chart.
2. **Members make about 1.90 times as many rides as casual users**, a difference of **1,268,785 trips** in this worksheet.
3. **Casual trips still exceed 1.4 million**, representing a sizeable share of recorded usage.

**Business interpretation:** The casual segment merits dedicated marketing attention, while the member segment appears more active in total ride volume. The dataset does not show how many distinct casual customers are available for conversion.

**Marketing opportunity:** Test clear annual-membership value messages among reachable casual customers, measuring *incremental sign-ups* rather than just impressions or ride volume.

**Important reconciliation:** This annual-volume worksheet totals **4,097,983**, **20 rides fewer** than the Python notebook and Tableau duration summary (**4,098,003**). The discrepancy is unresolved; do not silently mix the two totals.

## Finding 2 — Casual rides are longer and more variable

**Tableau visuals:** Duration statistical summary and average ride duration.

| Duration measure | Casual | Member |
|---|---:|---:|
| Mean (precise chart) | **20.11 min** | **12.29 min** |
| Median | **12 min** | **9 min** |
| First quartile | 7 min | 5 min |
| Third quartile | 22 min | 15 min |
| Interquartile range | **15 min** | **10 min** |
| Standard deviation | **42 min** | **25 min** |

### Three evidence-based observations

1. **The mean casual trip is 7.82 minutes longer**, approximately **63.6% longer** than the mean member trip.
2. **The median is also longer:** **12 minutes casual** versus **9 minutes member**, so the difference is not limited to the average.
3. **Casual ride lengths vary more:** standard deviation **42 vs 25 minutes**, and IQR **15 vs 10 minutes**.

**Business interpretation:** The groups differ in both typical ride length and variation. Longer casual rides may reflect different use cases, but trip purpose and willingness to subscribe are not directly recorded.

**Marketing opportunity:** Test membership benefit explanations tailored to riders who make longer trips, checking actual fee rules before suggesting any savings.

## Finding 3 — Hourly activity suggests different usage rhythms

**Tableau visual:** Hourly ride distribution (% within each membership group).

| Ride-start hour | Member share of member rides | Casual share of casual rides |
|---|---:|---:|
| 8 AM | ~7.4% | ~3.6% |
| 2 PM | ~5.2% | ~7.0% |
| 5 PM | ~10.9% | ~9.5% |
| Midnight | ~0.8% | ~2.0% |

### Three evidence-based observations

1. **8 AM is much more prominent in the member distribution:** ~**7.4%** of member trips versus ~**3.6%** of casual trips.
2. **5 PM is a strong hour for both groups**, at ~**10.9%** for members and ~**9.5%** for casual rides.
3. **Casual rides have higher relative shares at 2 PM and midnight**, indicating a broader timing profile.

**Business interpretation:** Member patterns are *consistent with* routine travel and possible commuting; casual patterns are compatible with more varied trip purposes. Neither motivation is verified.

**Marketing opportunity:** Test creative and campaign timing during periods of higher casual activity.

**Denominator warning:** These percentages describe the distribution **within each segment**. They are not shares of all rides, rider counts, or absolute hourly volumes.

## Finding 4 — Casual rides are concentrated on weekends

**Tableau visual:** Weekly ride counts. `K` = approximately one thousand rides.

| Day | Casual rides | Member rides |
|---|---:|---:|
| Monday | ~166K | ~388K |
| Tuesday | ~162K | ~440K |
| Wednesday | ~162K | ~437K |
| Thursday | ~174K | ~422K |
| Friday | ~223K | ~392K |
| Saturday | **~299K** | ~327K |
| Sunday | ~229K | ~279K |

### Three evidence-based observations

1. **Saturday is the busiest casual day**, with approximately **299K rides**.
2. **Saturday casual volume is ~85% higher than Tuesday or Wednesday**, both at approximately **162K**.
3. **The membership mix narrows on Saturday:** casual rides account for roughly **48%** of Saturday rides, versus roughly **27%** on Tuesday. Member trips peak on Tuesday (~440K) and Wednesday (~437K).

**Business interpretation:** The weekly pattern supports different marketing schedules for the two segments, without proving whether weekend trips are recreational.

**Marketing opportunity:** Pilot weekend membership promotions and measure incremental conversion against a comparable holdout group.

## Finding 5 — Summer creates a clear seasonal opportunity

**Tableau visual:** Monthly ride trends. Counts below are rounded chart labels.

| Month | Casual rides | Member rides |
|---|---:|---:|
| January | ~17K | ~81K |
| February | ~30K | ~118K |
| March | ~60K | ~161K |
| April | ~87K | ~215K |
| May | ~159K | ~277K |
| June | ~200K | ~310K |
| July | **~227K** | ~338K |
| August | ~220K | **~341K** |
| September | ~188K | ~319K |
| October | ~144K | ~274K |
| November | ~64K | ~171K |
| December | ~19K | ~77K |

### Three evidence-based observations

1. **Casual rides peak in July (~227K)**; member rides peak in **August (~341K)**.
2. **Casual July volume is approximately 13.4 times January volume**, based on rounded labels (~227K vs ~17K).
3. **Members record more rides every month**, despite the seasonal increase in casual activity.

**Business interpretation:** Both segments are seasonal, with particularly large summer-versus-winter variation in casual volume. The dataset does not isolate the influence of weather, tourism, events, or pricing.

**Marketing opportunity:** Launch and evaluate membership education during the spring-to-summer ramp-up rather than waiting until peak summer demand.

**Period clarification:** The chart orders months January–December for readability. In the intended study window, **October–December refer to 2025** and **January–September to 2026**. Actual timestamp boundaries were not independently validated.

## Finding 6 — Electric bikes account for most rides in both segments

**Tableau visual:** Bike type by membership.

| Bike type | Casual rides | Member rides |
|---|---:|---:|
| Classic bike | ~544K | ~1,235K |
| Electric bike | **~870K** | **~1,449K** |

| Share within segment | Casual | Member |
|---|---:|---:|
| Electric | **~61.5%** | **~54.0%** |
| Classic | ~38.5% | ~46.0% |

### Three evidence-based observations

1. **Electric bikes are the majority of rides in both groups**, exceeding classic-bike trips in each segment.
2. **Electric-bike share is ~7.5 percentage points higher for casual rides** than for member rides (61.5% vs 54.0%).
3. **Members record more rides on both bike types** in absolute terms.

**Business interpretation:** Electric-bike usage is especially prominent in the *mix of casual rides*. This is not a survey of personal preference, nor does it reveal whether a particular casual customer rides frequently.

**Marketing opportunity:** Explain the actual annual-membership terms for electric bikes, including any extra charges. Test whether this information improves membership conversion.

---

## Cross-chart insight: Different riding patterns call for different marketing tests

| Dimension | Casual pattern | Member pattern | Testable implication |
|---|---|---|---|
| Ride share | ~34.5% | ~65.5% | Build a dedicated casual-to-member campaign |
| Mean duration | 20.11 min | 12.29 min | Explain value for different ride lengths |
| Peak weekday | Saturday (~299K) | Tuesday (~440K) | Tailor timing by segment |
| 8 AM share | ~3.6% | ~7.4% | Avoid assuming identical daily routines |
| Peak month | July (~227K) | August (~341K) | Test spring/summer outreach |
| Electric-bike share | ~61.5% | ~54.0% | Test electric-bike-specific messaging |

**Central conclusion:** Casual and member ride records show meaningful differences across several dimensions. These differences justify **hypothesis-driven marketing experiments**, not a claim that the trip data itself proves which customers will purchase annual membership.

## Three priority recommendations

### 1. Target weekend and spring/summer casual activity

- **Evidence:** Saturday is the casual peak (~299K); July is the casual monthly peak (~227K).
- **Action:** Test weekend and spring/summer campaigns with transparent membership terms and clear value explanations.
- **Measurement:** Incremental annual memberships, conversion rate, customer acquisition cost, and later retention.

### 2. Communicate electric-bike membership value

- **Evidence:** Electric bikes make up ~61.5% of casual trips.
- **Action:** Compare electric-bike-specific messaging with general membership messaging, using accurate prices, benefits, and fee conditions.
- **Measurement:** Controlled conversion lift and retained annual memberships.

### 3. Personalise conversion efforts where data permissions allow

- **Evidence:** Casual rides make up roughly one-third of recorded trips, with distinctive duration and timing patterns.
- **Action:** If Cyclistic has separate, authorised customer-level data, identify eligible repeat casual users and test tailored offers.
- **Measurement:** Incremental sign-ups versus holdout, acquisition cost, and retention.
- **Boundary:** The present trip-level data **cannot identify repeat customers or measure membership conversion**.

## Data quality and analytical limitations

| Issue | Why it matters |
|---|---|
| **2,073,763 records removed for missing station data** | Approximately **33.60%** of raw records were excluded; segment or bike-type comparisons may be affected by selection bias |
| **20-ride difference across Tableau views** | Annual-volume chart totals **4,097,983**, whereas the notebook and duration summary total **4,098,003**; worksheet filters and null handling need review |
| **Ride IDs are not customer IDs** | Unique users, repeat riders, and conversions are not observable |
| **No observed trip purpose** | Commuting and leisure interpretations are plausible but unverified |
| **No pricing or marketing outcomes** | Savings, ROI, acquisition costs, and campaign effectiveness cannot be estimated from this dataset |
| **Rounded Tableau labels** | Weekly/monthly/bike-type counts are approximate; some chart `$` labels are formatting errors, not monetary values |
| **No executed duplicate removal** | The notebook should be reviewed for duplicate ride IDs before treating every record as a unique valid ride |
| **No independent CSV rerun** | Counts are taken from notebook outputs and Tableau charts; the cleaned export exceeds 760 MB and is not hosted |

## Portfolio takeaway

> **Cyclistic's casual riders account for a meaningful share of ride activity and exhibit different duration, timing, seasonality, and bike-type patterns from members. The most defensible next step is to test targeted membership campaigns and measure actual conversion outcomes using appropriate customer and marketing data.**

## Supporting project files

- [Exploratory Data Analysis](Exploratory_Data_Analysis.md) — full seven-chart analysis and interpretation.
- [Data Sources and Methodology](Data_Sources_and_Methodology.md) — data provenance, analytical scope, and reproducibility.
- [Data Cleaning and Transformation](Data_Cleaning_and_Transformation.md) — executed Python cleaning steps and row-count audit.
- [Jupyter notebook](../notebooks/all_trips_v2.ipynb) — original Python workflow (when added to the repository).
- Tableau workbook and chart screenshots — add to `tableau/` and `visualizations/` respectively.

**Source attribution:** Cyclistic is a fictional case-study company; the underlying trip records come from the public [Divvy bike-share dataset](https://divvy-tripdata.s3.amazonaws.com/index.html).
