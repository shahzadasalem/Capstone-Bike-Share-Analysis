# Data Cleaning and Transformation

**Project:** Cyclistic Bike-Share Case Study  
**Period:** October 2025–September 2026 (source file naming)  
**Notebook:** [`all_trips_v2.ipynb`](../notebooks/all_trips_v2.ipynb)  
**Tools:** Python 3.12.13, pandas, JupyterLab Desktop  
**Final local export:** `oct_sep_summary.csv` (over 760 MB; not uploaded)

> **Source of truth:** This document is based on the uploaded notebook's **executed code and saved outputs**. The original monthly CSVs and final large export were not rerun or independently inspected. Commentary in code cells is not treated as evidence that a transformation executed.

## 1. Cleaning objective

Combine twelve monthly Divvy ride datasets, standardise the columns, derive analytical variables, filter selected records, and export a ride-level file for Tableau. This document also records limitations and possible improvements without presenting those improvements as completed work.

## 2. Source files and import

The notebook uses `pd.read_csv()` to load the following 12 files:

```text
202510-divvy-tripdata.csv   202511-divvy-tripdata.csv
202512-divvy-tripdata.csv   202601-divvy-tripdata.csv
202602-divvy-tripdata.csv   202603-divvy-tripdata.csv
202604-divvy-tripdata.csv   202605-divvy-tripdata.csv
202606-divvy-tripdata.csv   202607-divvy-tripdata.csv
202608-divvy-tripdata.csv   202609-divvy-tripdata.csv
```

It checks columns and data types for each file and concatenates them in chronological order:

```python
all_trips = pd.concat(
    [oct, nov, dec, jan, feb, mar, apr, may, jun, jul, aug, sep],
    ignore_index=True
)
```

**Initial combined shape:** **6,171,785 rows × 13 columns**, as reported by the notebook.

## 3. Standardise field names and types

The notebook calls `.rename(columns={...})` for each month, with the following legacy-name mapping:

| Input name | Standardised name |
|---|---|
| `trip_id` | `ride_id` |
| `bikeid` | `rideable_type` |
| `start_time` | `started_at` |
| `end_time` | `ended_at` |
| `from_station_name` | `start_station_name` |
| `from_station_id` | `start_station_id` |
| `to_station_name` | `end_station_name` |
| `to_station_id` | `end_station_id` |
| `usertype` | `member_casual` |

It converts `ride_id` and `rideable_type` to string in all twelve DataFrames before concatenation.

**Caution:** `bikeid` usually denotes an identifier, whereas `rideable_type` denotes a category. Their equivalence must not be assumed if the code is reused with historical schemas. The notebook does not demonstrate that this rename was needed for the current files.

## 4. Inspect the raw combined data

The notebook uses `.info()`, `.head()`, `.describe()`, `.shape`, `.columns`, and `.value_counts()`.

| Pre-filter observation | Saved result |
|---|---:|
| All rides | **6,171,785** |
| `member` | **3,982,761** |
| `casual` | **2,189,024** |
| Unique `ride_id` values shown in `.describe()` | **6,171,750** |

The displayed distinct-ID count is **35 fewer than the number of rows**. This suggests potential repeated IDs, but the notebook does **not** execute duplicate detection/removal with `duplicated()` or `drop_duplicates()`. The precise cause of the difference has not been investigated.

Comments mention changing `Subscriber` to `member` and `Customer` to `casual`. **No executed replacement code appears**, and the displayed data already contains only `member` and `casual`.

## 5. Drop coordinate fields

The executed code is:

```python
all_trips = all_trips.drop(
    columns=['start_lat', 'start_lng', 'end_lat', 'end_lng'],
    errors='ignore'
)
```

The notebook reports **9 remaining base columns**. Although a comment also refers to birth year and gender, those columns are not in the executed `drop()` call.

## 6. Audit and filter missing station data

The notebook checks missing values in four fields:

| Field | Missing values before filtering |
|---|---:|
| `start_station_name` | 1,289,486 |
| `start_station_id` | 1,289,486 |
| `end_station_name` | 1,355,487 |
| `end_station_id` | 1,355,487 |

These counts **overlap**; do not add them together.

The notebook creates `delete_trips` to inspect records missing at least one station field, then runs:

```python
all_trips = all_trips.dropna(
    subset=[
        'start_station_name', 'start_station_id',
        'end_station_name', 'end_station_id'
    ]
)
```

| Outcome | Rows |
|---|---:|
| Before filter | **6,171,785** |
| Removed with at least one missing station field | **2,073,763** |
| After filter | **4,098,022** |

**33.60% of the original rides were excluded at this stage.** This is a major limitation: missing station metadata does not prove a trip was invalid, and the exclusion could affect bike-type or membership comparisons. The notebook does not quantify whether excluded rides disproportionately belong to a particular group.

## 7. Parse timestamps and create analytical columns

Executed conversion:

```python
all_trips['started_at'] = pd.to_datetime(all_trips['started_at'])
all_trips['ended_at'] = pd.to_datetime(all_trips['ended_at'])
```

Executed derived fields:

```python
all_trips['date'] = all_trips['started_at'].dt.date
all_trips['month'] = all_trips['started_at'].dt.month
all_trips['day'] = all_trips['started_at'].dt.day
all_trips['year'] = all_trips['started_at'].dt.year
all_trips['ride_length_minutes'] = (
    (all_trips['ended_at'] - all_trips['started_at'])
    .dt.total_seconds() / 60
).round(2)
all_trips['day_of_week'] = all_trips['started_at'].dt.day_name()
```

| Added field | Meaning |
|---|---|
| `date` | Ride-start calendar date |
| `month` | Ride-start month (1–12) |
| `day` | Ride-start day of month |
| `year` | Ride-start year |
| `ride_length_minutes` | Duration in minutes, rounded to 2 decimal places |
| `day_of_week` | Ride-start weekday name |

**Not performed in Python:** Creation of a dedicated `hour` column. The hourly Tableau visuals may extract hour from `started_at`; verify the workbook calculation when reproducing the analysis.

**Not verified:** Minimum/maximum actual timestamps, timezone treatment, and unusually long positive rides.

## 8. Filter quality-control and negative-duration rides

The executed filter is:

```python
all_trips_v2 = all_trips[
    (all_trips['start_station_name'] != 'HQ QR') &
    (all_trips['ride_length_minutes'] >= 0)
].copy()
```

This excludes rides that either start at `HQ QR` or have a **negative** duration. Rides of **zero minutes are retained**. The notebook does not report separate counts for the two exclusion conditions.

The saved output shows:

| Stage | Rows |
|---|---:|
| After missing-station filter | 4,098,022 |
| After final quality/duration filter | **4,098,003** |
| Additional exclusions | **19** |

## 9. Final row-count reconciliation

| Checkpoint | Rows | Removed at checkpoint |
|---|---:|---:|
| Combined raw data | **6,171,785** | — |
| Missing-station filter | **4,098,022** | **2,073,763** |
| `HQ QR` / negative-duration filter | **4,098,003** | **19** |
| **Total excluded** | — | **2,073,782** |

The final dataset retains approximately **66.40%** of initial records. The notebook's final `.info()` reports **4,098,003 rows and 15 columns**.

This matches the Tableau duration-summary count (2,683,396 member + 1,414,607 casual = 4,098,003), but **not** the separate annual ride-volume chart (2,683,384 + 1,414,599 = 4,097,983). The **20-ride discrepancy remains unresolved**; worksheet filters or null handling should be investigated rather than assuming a cause.

## 10. Export and GitHub distribution

The notebook executes:

```python
all_trips_v2.to_csv('oct_sep_summary.csv', index=1)
```

Because `index=1` is truthy, the DataFrame index is **included** in the CSV. It may appear as an additional unnamed field when opened in Tableau. For a cleaner future export, `index=False` would normally be preferable, but **that is a recommendation, not the code that was executed**.

The cleaned CSV exceeds **760 MB** and is **not included in the GitHub repository**. Instead, publish the notebook, public-source links, data dictionary, and instructions to regenerate the file locally.

**Do not upload** a large CSV by splitting it into arbitrary parts solely to bypass GitHub limits. Exclude it using `.gitignore`, for example:

```gitignore
oct_sep_summary.csv
all_trips_v2.csv
*.zip
.ipynb_checkpoints/
```

## 11. Known limitations and recommended follow-up checks

The following are **future validation tasks, not completed cleaning steps**:

1. Check duplicate `ride_id` values and decide whether/how to resolve them.
2. Profile missing station fields by `member_casual`, `rideable_type`, and month.
3. Test sensitivity of findings to the 33.60% station-data exclusion.
4. Confirm actual timestamp bounds and timezone assumptions.
5. Investigate zero-minute and unusually long positive rides.
6. Separate the 19 final exclusions by reason.
7. Reconcile the 20-ride difference between Tableau worksheets.
8. Verify bike-type values and the legacy `bikeid` rename before reuse.
9. Export without the DataFrame index in a future reproducibility update.

## 12. Reproduction instructions

1. Obtain the twelve monthly CSVs named above from [Divvy's public historical trip data](https://divvy-tripdata.s3.amazonaws.com/index.html).
2. Put the files in the notebook's working directory or update the `pd.read_csv()` paths.
3. Open `notebooks/all_trips_v2.ipynb` in JupyterLab with Python and pandas installed.
4. Run cells in order; confirm the row counts at each checkpoint.
5. Recreate `oct_sep_summary.csv` locally and reconnect the Tableau workbook.
6. Review the known limitations before interpreting or publishing results.

**Portfolio note:** The documentation describes the actual notebook, including its limitations. It does not claim that duplicate removal, membership-label replacement, customer-level tracking, or causal conversion analysis was performed.
