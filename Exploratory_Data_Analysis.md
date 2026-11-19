# Exploratory Data Analysis (EDA)

**Project:** Cyclistic Bike-Share Case Study  
**Business question:** How do casual riders and annual members use bike-share differently, and what marketing opportunities could encourage casual riders to become annual members?  
**Intended study period:** October 2025–September 2026 (based on the 12 monthly CSV filenames)  
**Analysis tools:** Python / pandas / JupyterLab for preparation; Tableau Desktop for visual analysis  
**Evidence:** [`all_trips_v2.ipynb`](../notebooks/all_trips_v2.ipynb), Tableau workbook and screenshots, and the project presentation.

> **Interpretation guide:** This is a descriptive analysis of **rides**, not unique people. Approximate chart labels are marked `~`. The reported Tableau values have not been recomputed from the 760+ MB cleaned CSV, which is not included in this repository. Patterns may be consistent with commuting or recreation, but trip purpose and actual membership conversion are not observed.

## 1. Executive summary

The cleaned dataset contains **4,098,003 ride records**, according to the saved Python notebook output. The Tableau duration summary agrees with this total, reporting **2,683,396 member rides (65.48%)** and **1,414,607 casual rides (34.52%)**. A separate annual-volume chart reports 20 fewer rides; that discrepancy is documented below.

Across the seven principal Tableau analyses, five themes emerge:

1. **Members generate most recorded trips**, while casual riders still account for roughly one-third of activity.
2. **Casual rides last longer:** 20.11 minutes on average, versus 12.29 minutes for members.
3. **Timing differs:** member activity is relatively concentrated on weekdays and around morning/evening peaks; casual activity increases on weekends and during afternoon hours.
4. **Seasonality matters:** both segments rise in warmer months, but casual riding varies more sharply across the year.
5. **Electric bikes are prominent in both segments**, especially among casual rides by percentage share.

These findings support **testing** targeted marketing, not claiming that any campaign has already increased membership.

## 2. Data preparation context and coverage

The notebook combines 12 monthly Divvy CSV files, from `202510-divvy-tripdata.csv` through `202609-divvy-tripdata.csv`, and exports `oct_sep_summary.csv` for Tableau.

| Processing checkpoint | Records |
|---|---:|
| Combined raw ride records | 6,171,785 |
| Excluded for missing start/end station name or ID | 2,073,763 |
| Remaining after station-data filter | 4,098,022 |
| Further excluded by `HQ QR` / negative-duration filter | 19 |
| **Final cleaned records** | **4,098,003** |

**Major caveat:** Excluding **33.60%** of raw rides for missing station metadata may bias comparisons, especially if missingness differs by membership or bike type. The notebook does not establish that every excluded ride was invalid. It also does not execute duplicate removal or a dedicated customer-level analysis. See [Data Cleaning and Transformation](Data_Cleaning_and_Transformation.md) for the exact workflow.

### Measures and denominators

- **Ride count:** number of ride records, not unique riders.
- **Membership share:** rides in a membership group divided by total analysed rides.
- **Hourly share:** percentage of *that group's* rides occurring in a particular hour; member and casual percentages have separate denominators.
- **Bike-type share:** percentage of *that group's* rides using a given bike type.
- **Duration:** `ride_length_minutes`, calculated from end minus start timestamps and rounded to two decimal places in Python.
- **Monthly/weekly counts:** values read from Tableau labels, generally rounded to the nearest thousand; sums of rounded values need not match exact annual totals.

## 3. EDA 1 — Annual ride distribution by membership

**Chart:** Total annual rides, casual versus member (Tableau presentation slide 9).

| Segment | Tableau annual-volume chart | Share |
|---|---:|---:|
| Member | 2,683,384 | 65.48% |
| Casual | 1,414,599 | 34.52% |
| **Total** | **4,097,983** | **100%** |

**Three key findings**

1. **Members account for almost two-thirds of rides.** Their 65.48% share exceeds the casual share by approximately 31 percentage points.
2. **Member volume is about 1.90 times casual volume.** The chart shows **1,268,785** more member than casual rides.
3. **Casual activity is substantial.** Approximately **1.41 million** casual trips represent a meaningful audience for testing membership marketing, although the number of distinct casual customers is unknown.

**Business interpretation:** Annual members are the larger source of observed ride volume, while casual rides offer a sizeable pool of activity that could be targeted with relevant value propositions.

**Marketing implication:** Test membership education and conversion messages aimed at casual users, and evaluate actual sign-ups using a separate campaign/customer dataset.

**Reconciliation note:** The notebook and Tableau duration summary total **4,098,003** (member **2,683,396**, casual **1,414,607**). The annual-volume chart is **20 rides lower**. The cause has not been established; inspect Tableau worksheet filters and null-handling before final publication.

## 4. EDA 2 — Ride-duration statistical distribution

**Chart:** Duration statistical summary (Tableau presentation slide 10).

| Statistic | Casual rides | Member rides |
|---|---:|---:|
| Rides in duration summary | 1,414,607 | 2,683,396 |
| Mean duration, rounded | 20 min | 12 min |
| Standard deviation | 42 min | 25 min |
| First quartile (Q1) | 7 min | 5 min |
| Median | 12 min | 9 min |
| Third quartile (Q3) | 22 min | 15 min |
| Interquartile range (IQR) | 15 min | 10 min |

**Three key findings**

1. **Casual rides are longer on average.** Rounded means differ by about eight minutes.
2. **Casual rides are more variable.** Standard deviation is **42 minutes**, compared with **25 minutes** for members; the casual IQR is also wider (**15 versus 10 minutes**).
3. **The typical casual ride is longer.** Median duration is **12 minutes** for casual rides and **9 minutes** for member rides. The middle half of casual rides spans **7–22 minutes**, versus **5–15 minutes** for members.

**Business interpretation:** Different duration profiles suggest the segments may value different aspects of the service. The higher mean than median in each group is consistent with some longer trips influencing the average, but a distribution plot would be needed to characterise skew precisely.

**Marketing implication:** Test membership messaging for people who take longer casual rides, using actual pricing and usage rules rather than assuming that longer trips always yield savings.

## 5. EDA 3 — Hourly riding patterns

**Chart:** Percentage of each membership segment's rides by starting hour (Tableau presentation slide 11).

| Hour | Member share of member rides | Casual share of casual rides |
|---|---:|---:|
| 8 AM | ~7.4% | ~3.6% |
| 2 PM | ~5.2% | ~7.0% |
| 5 PM | ~10.9% | ~9.5% |
| Midnight | ~0.8% | ~2.0% |

**Three key findings**

1. **The morning peak is more pronounced for members.** At **8 AM**, the within-member share is approximately **7.4%**, compared with **3.6%** for casual rides.
2. **5 PM is a strong period for both groups.** Approximately **10.9%** of member rides and **9.5%** of casual rides occur at this hour.
3. **Casual rides have higher relative midday and late-night shares.** At **2 PM**, casual share is approximately **7.0%** versus **5.2%** for members; at midnight, about **2.0%** versus **0.8%**.

**Business interpretation:** Member timing is consistent with routine travel and potential commuting; casual rides are spread more broadly into afternoon and night. **Trip purpose cannot be proven** from timestamps alone.

**Marketing implication:** Compare campaign response by time of day, particularly during periods when casual riders are active. **Do not interpret these percentages as absolute hourly ride counts** or as the percentage of all riders at an hour.

## 6. EDA 4 — Weekly ride patterns

**Chart:** Ride counts by weekday and membership segment (Tableau presentation slide 12). All counts below are **approximate thousands of rides (K)**, not currency.

| Day | Casual rides | Member rides |
|---|---:|---:|
| Monday | ~166K | ~388K |
| Tuesday | ~162K | ~440K |
| Wednesday | ~162K | ~437K |
| Thursday | ~174K | ~422K |
| Friday | ~223K | ~392K |
| Saturday | ~299K | ~327K |
| Sunday | ~229K | ~279K |

**Three key findings**

1. **Members are busiest midweek.** Tuesday (**~440K**) and Wednesday (**~437K**) are the strongest member days.
2. **Saturday is the highest casual day.** At **~299K**, casual Saturday activity is approximately **85% higher** than Tuesday or Wednesday (**~162K** each).
3. **The segment gap narrows on weekends.** Casual rides represent approximately **48% of Saturday rides** (299K of 626K), compared with approximately **27% on Tuesday** (162K of 602K).

**Business interpretation:** Weekly rhythms differ, with members showing stronger midweek activity and casual users concentrating more activity on weekends. This pattern is compatible with different routine and discretionary travel needs but does not confirm trip purpose.

**Marketing implication:** Pilot weekend-specific annual-membership messages, ideally with a holdout group and tracked conversions.

**Chart-quality note:** Tableau screenshots use `$`-style formatting on some count labels. These values are **ride counts**, not dollars.

## 7. EDA 5 — Monthly ride trends and seasonality

**Chart:** Monthly ride counts by membership segment (Tableau presentation slide 13). Values are **approximate thousands (K)**, not currency.

| Calendar month | Casual rides | Member rides |
|---|---:|---:|
| January | ~17K | ~81K |
| February | ~30K | ~118K |
| March | ~60K | ~161K |
| April | ~87K | ~215K |
| May | ~159K | ~277K |
| June | ~200K | ~310K |
| July | ~227K | ~338K |
| August | ~220K | ~341K |
| September | ~188K | ~319K |
| October | ~144K | ~274K |
| November | ~64K | ~171K |
| December | ~19K | ~77K |

**Three key findings**

1. **Both groups peak in summer.** Casual rides peak in **July (~227K)**, while member rides peak in **August (~341K)**.
2. **Casual riding is highly seasonal.** July casual volume is approximately **13.4 times** January casual volume (~17K), based on rounded labels.
3. **Members outnumber casual rides every month.** The member segment remains larger even when both groups experience winter lows.

**Business interpretation:** Seasonality strongly affects the timing of potential membership campaigns. The data support testing spring/summer outreach, but weather, tourism, and pricing effects were not modelled.

**Marketing implication:** Test campaigns as casual activity increases in spring and evaluate conversion through summer, rather than relying on a single year-round message.

**Period note:** The chart is arranged January–December, but the underlying intended observation window is **October 2025–September 2026**. October–December belong to 2025, while January–September belong to 2026. Actual timestamp bounds still require validation.

## 8. EDA 6 — Average ride duration

**Chart:** Average ride duration by membership type (Tableau presentation slide 14).

| Segment | Mean ride duration |
|---|---:|
| Casual | **20.11 minutes** |
| Member | **12.29 minutes** |
| **Difference** | **7.82 minutes** |

**Three key findings**

1. **Casual rides average 7.82 minutes longer** than member rides.
2. **The casual average is approximately 63.6% higher**, or **1.64 times** the member average.
3. **The precise means confirm the rounded statistical summary** (about 20 versus 12 minutes), reinforcing that the difference is not merely a chart-formatting artifact.

**Business interpretation:** The duration difference, together with weekend and summer patterns, suggests that a single generic marketing message may not suit both segments. The data do **not** prove leisure use or predict willingness to buy membership.

**Marketing implication:** Compare marketing creative that highlights value for regular longer rides against broader membership-benefit messaging.

**Presentation note:** This view repeats the mean comparison from EDA 2. Keep it as a simple visual headline and use EDA 2 for the distribution detail. Some Tableau labels incorrectly show `$`; the unit is **minutes**.

## 9. EDA 7 — Bike-type usage

**Chart:** Ride counts by bike type and membership segment (Tableau presentation slide 15). Counts are approximate and rounded.

| Bike type | Casual rides | Member rides |
|---|---:|---:|
| Classic bike | ~544K | ~1,235K |
| Electric bike | ~870K | ~1,449K |

| Share within each membership segment | Casual | Member |
|---|---:|---:|
| Electric-bike rides | **~61.5%** | **~54.0%** |
| Classic-bike rides | ~38.5% | ~46.0% |

**Three key findings**

1. **Electric bikes account for the majority of rides in both groups.** Approximately **870K** casual and **1,449K** member trips used electric bikes.
2. **Electric bikes are more prominent in the casual ride mix.** Their share is about **61.5%** of casual rides versus **54.0%** of member rides, a difference of **7.5 percentage points**.
3. **Members have more rides in both categories.** Approximately **1,235K** member classic-bike rides and **1,449K** member electric-bike rides exceed the corresponding casual volumes.

**Business interpretation:** Electric-bike usage is an important feature of casual activity. This is a comparison of **ride mix**, not a direct survey of rider preferences or an estimate of distinct electric-bike customers.

**Marketing implication:** Test clear explanations of annual membership's actual electric-bike terms, fees and benefits. Verify pricing before making any savings claims.

## 10. Cross-chart synthesis

| Dimension | Observed casual pattern | Observed member pattern | Possible marketing test |
|---|---|---|---|
| Ride share | ~34.5% of rides | ~65.5% of rides | Membership education for casual users |
| Duration | Longer; 20.11-min mean | Shorter; 12.29-min mean | Value messaging for repeat longer trips |
| Day of week | Saturday peak | Tuesday/Wednesday peaks | Weekend campaign timing |
| Hour | Higher relative midday/night share | Stronger 8 AM share | Time-of-day creative testing |
| Season | Sharper summer peak | More activity year-round | Spring-to-summer outreach |
| Bike type | 61.5% electric share | 54.0% electric share | Electric-bike membership messaging |

**Central insight:** The two segments differ along multiple dimensions—volume, duration, time, season and bike type—so **segmented marketing experiments** are more defensible than one generic membership campaign.

## 11. Three data-informed recommendations

### Recommendation 1 — Target weekend and spring/summer casual activity

**Evidence:** Casual rides peak on Saturday (~299K) and in July (~227K).  
**Action:** Test seasonal and weekend membership promotions with accurate pricing and clear terms.  
**Success metrics:** Incremental memberships, conversion rate, cost per acquisition and retention.  
**Caveat:** A high number of rides does not reveal how many eligible casual customers can be contacted.

### Recommendation 2 — Explain electric-bike membership value

**Evidence:** Approximately 61.5% of casual rides use electric bikes.  
**Action:** Test electric-bike-specific messaging that explains verified membership benefits and any extra usage charges.  
**Success metrics:** Campaign response, incremental sign-ups and retained members.  
**Caveat:** Ride-level electric-bike share does not establish a customer's long-term preference or whether membership is financially advantageous.

### Recommendation 3 — Test personalised conversion messaging where permitted

**Evidence:** Casual riders generate approximately one-third of recorded rides, and casual activity differs by timing and duration.  
**Action:** If separate, permissioned customer-level information becomes available, identify eligible repeat casual users and run controlled membership-offer experiments.  
**Success metrics:** Lift versus holdout, conversion cost, new annual memberships and retention.  
**Caveat:** The current anonymised trip dataset cannot identify repeat customers or directly measure conversion.

## 12. Limitations and validation checklist

- **Selection bias:** 2,073,763 records (33.60% of raw data) were removed for missing station metadata. Check whether exclusions differ by membership, bike type or month.
- **Unresolved 20-ride discrepancy:** The annual-volume worksheet totals 4,097,983, while the notebook and duration summary total 4,098,003.
- **No unique-rider identifiers:** Trip counts cannot establish customer counts, repeat behaviour or membership conversion.
- **No trip-purpose labels:** Commuting and recreation are interpretations, not observed facts.
- **No commercial inputs:** Pricing, customer acquisition cost, membership profitability and ROI are not contained in the trip data.
- **Rounded visual labels:** Weekly, monthly and bike-type counts are approximate; do not treat them as exact totals.
- **Potential duplicate ride IDs:** The notebook did not execute duplicate removal; verify before rerunning or publishing exact aggregates.
- **Duration outliers:** The executed filter removes negative durations but retains zero and long positive rides. Consider sensitivity analysis.
- **Date/time checks:** Validate actual minimum/maximum timestamps, timezone handling and hour extraction in Tableau.
- **Formatting:** `$` signs in some charts represent formatting errors, not money.

## 13. Reproducibility and project navigation

1. Download the twelve source files from [Divvy's historical trip-data directory](https://divvy-tripdata.s3.amazonaws.com/index.html).
2. Follow the executed workflow in [`all_trips_v2.ipynb`](../notebooks/all_trips_v2.ipynb).
3. Compare row counts with [Data Cleaning and Transformation](Data_Cleaning_and_Transformation.md).
4. Generate `oct_sep_summary.csv` locally; it is not hosted in GitHub because it exceeds 760 MB.
5. Reconnect the Tableau workbook and verify worksheet filters, percentage denominators and date calculations.
6. Review the original chart screenshots in `visualizations/` and the presentation in `presentation/` when those assets have been uploaded.

**Source context:** Cyclistic is the fictional Google Data Analytics Capstone scenario; the ride records originate from public Divvy trip data. The analysis describes patterns in the processed dataset and proposes marketing experiments; it does not claim causal effects or observed membership growth.
