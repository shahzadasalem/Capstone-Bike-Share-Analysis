# Data Sources and Methodology

**Project:** Cyclistic Bike-Share Case Study  
**Business question:** How do casual riders and annual members use bike-share differently, and how can these differences inform membership-conversion marketing?  
**Study period:** October 2025–September 2026 (as specified by the 12 source filenames)  
**Tools:** Python 3.12.13 / pandas in JupyterLab Desktop, Tableau Desktop, PowerPoint  
**Primary evidence:** [`all_trips_v2.ipynb`](../notebooks/all_trips_v2.ipynb), its saved outputs, and the project's Tableau charts.

> **Evidence standard:** Counts and transformations below are documented in the uploaded notebook's saved execution outputs. The 12 original monthly CSVs and 760+ MB cleaned CSV were not independently rerun or inspected here. Results should be reproduced from the source files before treating them as independently verified.

## 1. Business context and analytical objective

Cyclistic is the fictional company in the Google Data Analytics Capstone scenario. The underlying data is from Divvy, Chicago's real bike-share system. The marketing objective is to understand **how recorded rides differ between casual and member segments** and propose testable ways to encourage annual membership.

**Unit of analysis:** a ride, not a person. Ride counts are not counts of distinct customers, and trip records alone cannot establish commuting purpose, customer intent, or actual membership conversion.

## 2. Data provenance and files

The notebook explicitly reads these 12 monthly input files:

| Period | Input CSV |
|---|---|
| Oct–Dec 2025 | `202510-divvy-tripdata.csv`, `202511-divvy-tripdata.csv`, `202512-divvy-tripdata.csv` |
| Jan–Mar 2026 | `202601-divvy-tripdata.csv`, `202602-divvy-tripdata.csv`, `202603-divvy-tripdata.csv` |
| Apr–Jun 2026 | `202604-divvy-tripdata.csv`, `202605-divvy-tripdata.csv`, `202606-divvy-tripdata.csv` |
| Jul–Sep 2026 | `202607-divvy-tripdata.csv`, `202608-divvy-tripdata.csv`, `202609-divvy-tripdata.csv` |

- **Public source:** [Divvy System Data](https://divvybikes.com/system-data) and [historical trip-data directory](https://divvy-tripdata.s3.amazonaws.com/index.html). These are source-access references; the individual archived files have not been independently checked here.
- **Python notebook:** `notebooks/all_trips_v2.ipynb`, containing the import, transformation, filters, and saved outputs.
- **Final analytical export:** `oct_sep_summary.csv`, produced by the notebook and referenced by the Tableau workbook. The export is not distributed because it is over 760 MB.
- **Tableau workbook:** `tableau/Oct-2025_to_Sep-2026-Tableau.twb`, with 12 worksheets, including alternative views of the same measures.
- **Visual evidence:** Tableau screenshots and presentation charts.

The filenames identify the intended 12-month window; the actual minimum and maximum timestamps were **not** separately validated in the notebook.

## 3. Dataset schema

After combining the files and removing coordinate columns, the notebook reports nine base fields:

| Field | Description |
|---|---|
| `ride_id` | Ride identifier; not a rider identifier |
| `rideable_type` | Bike type/category in the current data |
| `started_at`, `ended_at` | Ride timestamps |
| `start_station_name`, `start_station_id` | Start station metadata |
| `end_station_name`, `end_station_id` | End station metadata |
| `member_casual` | Recorded membership segment |

The notebook then adds `date`, `month`, `day`, `year`, `ride_length_minutes`, and `day_of_week`, yielding **15 columns** in the final DataFrame. It does **not** create a Python `hour` column; the hour-based Tableau analysis requires a Tableau timestamp calculation or another documented derivation.

## 4. Executed methodology

### Step 1 — Import and standardise

The notebook uses `pd.read_csv()` for each monthly file, compares columns, applies a legacy-to-current column-name mapping, casts `ride_id` and `rideable_type` to string, and combines the 12 DataFrames with `pd.concat(..., ignore_index=True)`.

**Caution:** The legacy mapping includes `bikeid` → `rideable_type`. A bike identifier is not automatically a bike category; the mapping should be checked before reusing the notebook with legacy data. No claim is made that this mapping altered the current 2025–2026 files.

### Step 2 — Inspect and reduce columns

The notebook checks column names, `.info()`, `.shape`, `.describe()`, and membership counts. It drops `start_lat`, `start_lng`, `end_lat`, and `end_lng` with `errors='ignore'`.

### Step 3 — Exclude missing station metadata

Records missing **any** of `start_station_name`, `start_station_id`, `end_station_name`, or `end_station_id` are removed with `dropna(subset=...)`.

### Step 4 — Create time and duration variables

`started_at` and `ended_at` are converted using `pd.to_datetime()`. The notebook derives calendar date, month, day, year, weekday name, and:

```python
all_trips['ride_length_minutes'] = (
    (all_trips['ended_at'] - all_trips['started_at']).dt.total_seconds() / 60
).round(2)
```

### Step 5 — Filter quality-control and negative-duration rides

The final DataFrame is created using:

```python
all_trips_v2 = all_trips[
    (all_trips['start_station_name'] != 'HQ QR') &
    (all_trips['ride_length_minutes'] >= 0)
].copy()
```

Zero-minute rides remain eligible. The notebook does **not** execute a `drop_duplicates()` operation, and it does **not** replace `Subscriber`/`Customer` labels: the saved counts already show `member` and `casual`.

### Step 6 — Export for Tableau

```python
all_trips_v2.to_csv('oct_sep_summary.csv', index=1)
```

`index=1` includes the DataFrame index in the CSV. This can introduce an extra, non-analytical index column in Tableau.

## 5. Cleaning audit from saved notebook outputs

| Stage | Ride records | Change |
|---|---:|---:|
| Twelve monthly CSVs concatenated | **6,171,785** | — |
| Removed due to missing station metadata | — | **−2,073,763** |
| After missing-station filter | **4,098,022** | — |
| After `HQ QR` / negative-duration filter | **4,098,003** | **−19** |
| **Total excluded** | — | **2,073,782** |

The missing-station filter removes **33.60%** of the initial records; total exclusions are about **33.60%**. The final dataset retains approximately **66.40%** of the original rides. The notebook does not separate the 19 final exclusions into quality-control versus negative-duration counts.

**Selection-bias warning:** Missing station metadata does not necessarily make a ride invalid. The substantial exclusion may affect member/casual comparisons, especially if missingness varies by bike type or membership.

## 6. Tableau analysis and measures

The project uses seven main analytical views: membership ride volume, duration summary, hourly ride patterns, weekly ride patterns, monthly ride trends, average ride duration, and bike-type usage. The workbook contains 12 worksheets because some analyses have alternative visual formats.

| Measure | Definition |
|---|---|
| Ride count | Number of records in a category |
| Membership share | Segment rides ÷ all analysed rides × 100 |
| Mean duration | Average `ride_length_minutes` for a segment |
| Median / quartiles | 50th / 25th / 75th percentiles of ride duration |
| Hourly segment share | Segment rides at an hour ÷ total rides for that segment × 100 |
| Bike-type segment share | Segment rides on a bike type ÷ total rides for that segment × 100 |

**Observed Tableau results** (chart-derived, not independently recomputed from the CSV):

- Duration summary: **2,683,396 member** and **1,414,607 casual** rides, totaling **4,098,003**, consistent with the notebook's final row count.
- Annual volume chart: **2,683,384 member** and **1,414,599 casual** rides, totaling **4,097,983** — **20 fewer rides** than the notebook.
- Average duration: **20.11 minutes casual** versus **12.29 minutes member**.
- Casual Saturday rides: approximately **299K**; casual July rides: approximately **227K**.
- Electric bikes: approximately **61.5% of casual rides** and **54.0% of member rides**.

**Unresolved reconciliation:** The 20-ride difference between the annual volume chart and final notebook count needs investigation (worksheet filters, null handling, and aggregation settings). Do not silently substitute one count for the other.

## 7. Analytical limitations and interpretation

1. **Large missing-station exclusion:** 2,073,763 records were removed. This is the main data-quality limitation and may introduce selection bias.
2. **No customer identity:** `ride_id` identifies trips, not people. Repeat riders and actual conversion rates cannot be derived from these records alone.
3. **No observed trip purpose:** Weekday and hourly patterns can be *consistent with* commuting, but do not prove it.
4. **No pricing or revenue:** Potential savings, profitability, and marketing ROI require separate commercial data.
5. **Time coverage not independently audited:** Monthly filenames identify the intended window; actual timestamp bounds and timezone treatment need verification.
6. **No duplicate removal in executed code:** The notebook's descriptive output indicates fewer unique ride IDs than rows, but there is no executed duplicate-resolution step.
7. **Rounding and display formatting:** Some Tableau charts show rounded thousands or currency-style labels for counts/minutes; these are not currency measures.

## 8. Business recommendations as hypotheses

- **Seasonal/weekend campaigns:** Test membership messaging during high-casual-activity periods.
- **Electric-bike value communication:** Test clear, accurate membership-versus-casual electric-bike pricing explanations.
- **Targeted conversion tests:** If appropriately authorised customer-level data becomes available, test offers for repeat casual users and evaluate incremental membership conversions.

Success measures should include conversion rate, incremental annual memberships, customer acquisition cost, and retention. These outcomes are **not** measurable from the current trip dataset alone.

## 9. Reproducing the project

1. Download the twelve named monthly CSVs from the public Divvy source.
2. Place them alongside the notebook or update its input paths.
3. Install Python and pandas; the saved environment reports Python **3.12.13**, but the pandas version is not recorded.
4. Run `notebooks/all_trips_v2.ipynb` in order and compare counts with the audit table.
5. Verify date bounds, missingness by segment, duplicate IDs, and the 20-ride Tableau discrepancy.
6. Generate `oct_sep_summary.csv` locally; do not upload the 760+ MB export to standard GitHub.
7. Reconnect the Tableau workbook to the regenerated file and inspect worksheet filters.

## 10. Suggested repository layout

```text
cyclistic-bike-share-analysis/
├── README.md
├── notebooks/
│   └── all_trips_v2.ipynb
├── reports/
│   ├── Business_Problem_and_Objectives.md
│   ├── Data_Sources_and_Methodology.md
│   └── Data_Cleaning_and_Transformation.md
├── tableau/
│   └── Oct-2025_to_Sep-2026-Tableau.twb
├── visualizations/
└── presentation/
```

**Availability note:** The cleaned `oct_sep_summary.csv` (over 760 MB) is intentionally excluded from the repository. The public source links and notebook provide the documented reconstruction path, subject to the validation notes above.
