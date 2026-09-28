# Pandas for Data Science

My complete, runnable notes on Python's **pandas** library — from `pd.Series` all the
way to cleaning a real 8,800-row dataset.

The repository is made of four parts:

| Part | Folder | Notebooks | What it is |
|------|--------|:---------:|------------|
| **Core lessons** | [`Notebook/`](Notebook/) | 12 | One topic per notebook, written as notes + code, ending with a *Key takeaways* table |
| **Capstone workbook** | [`Netflix_Data_Analysis/`](Netflix_Data_Analysis/) | 1 | 125 pandas questions answered end to end on the Netflix catalogue |
| **Data Manipulation with Pandas** | [`Data Manipulation/`](Data%20Manipulation/) | 2 | A deep dive into pandas internals — objects, indexing, missing data, multi-indexing, merging, grouping, pivot tables, strings, time series, `eval()`/`query()` |
| **Coursera – Introduction to Data Science in Python** | [`Coursera_Intro_to_Data_Science/`](Coursera_Intro_to_Data_Science/) | 16 | Lecture notebooks from the University of Michigan course (Course 1 of the *Applied Data Science with Python* specialization) |

All notebooks are committed **with their outputs**, so you can read them straight on
GitHub without installing anything.

```
31 notebooks · 1,155 code cells · 452 explanation cells · 4 datasets
```

---

## Repository layout

```
Pandas_For_Data_Science/
├── Notebook/                          # notebooks 1–12, one topic each
├── Netflix_Data_Analysis/             # notebook 13, the 125-question capstone workbook
├── Data Manipulation/                 # Part I & Part II deep-dive notebooks
├── Coursera_Intro_to_Data_Science/    # 16 Coursera lecture notebooks (01–16)
├── data/                              # all CSV files used by the core + Netflix notebooks
├── requirements.txt
├── .gitignore
└── README.md
```

The core and Netflix notebooks read their data with a relative path —
`pd.read_csv("../data/file.csv")`. Every notebook folder sits **one level below the
repository root**, so that same `../data/...` path works from any of them — nothing to
change after cloning. (The *Data Manipulation* and *Coursera* notebooks use their own
external datasets — see their sections below.)

---

## Learning path

Read them in this order. Each one assumes the ones above it.

| # | Notebook | Topic | What it covers |
|---|----------|-------|----------------|
| 1 | [`Pandas Demo.ipynb`](Notebook/Pandas%20Demo.ipynb) | **First look at a dataset** | `read_csv`, `head`, `tail`, `shape`, `info`, `describe`, checking for missing values and duplicates |
| 2 | [`Series and dataframe.ipynb`](Notebook/Series%20and%20dataframe.ipynb) | **Series vs DataFrame** | 1-D Series vs 2-D DataFrame, custom index, building a table from a dict, `to_csv` / `read_csv` round trip |
| 3 | [`lociloc.ipynb`](Notebook/lociloc.ipynb) | **`.loc` vs `.iloc`** | label-based vs position-based selection, why `.loc` includes the end and `.iloc` does not, common mistakes |
| 4 | [`pandas_selection_clean.ipynb`](Notebook/pandas_selection_clean.ipynb) | **Selecting data** | `[]`, `.loc`, `.iloc`, single vs double brackets, row + column selection in one call |
| 5 | [`Indexes_How_to_Set,_Reset,_and_Use_Indexes.ipynb`](Notebook/Indexes_How_to_Set,_Reset,_and_Use_Indexes.ipynb) | **Indexes** | `set_index`, `reset_index`, `reset_index(drop=True)`, `inplace=True` vs reassigning |
| 6 | [`Condition.ipynb`](Notebook/Condition.ipynb) | **Filtering with conditions** | boolean masks, `df.loc[condition, columns]`, `&` `\|` `~`, `isin`, `between`, `str.contains` |
| 7 | [`Sorting.ipynb`](Notebook/Sorting.ipynb) | **Sorting** | `sort_values`, `sort_index`, multi-column sorts, `na_position`, `reset_index(drop=True)` after sorting |
| 8 | [`adding removing.ipynb`](Notebook/adding%20removing.ipynb) | **Adding & removing data** | adding columns and rows, updating with `.loc`, `SettingWithCopyWarning`, `drop`, `drop_duplicates`, `dropna` |
| 9 | [`pandas_count_clean_heading.ipynb`](Notebook/pandas_count_clean_heading.ipynb) | **Counting** | `len`, `count`, `value_counts`, `nunique`, counting with conditions, `groupby().count()` vs `.size()`, `pd.crosstab` |
| 10 | [`groupby.ipynb`](Notebook/groupby.ipynb) | **GroupBy** | split → apply → combine, `agg` with a list and a dict, two-column groups, `unstack`, `transform`, **25 practice questions** |
| 11 | [`pandas_joins_simple.ipynb`](Notebook/pandas_joins_simple.ipynb) | **Joins** | `pd.merge` inner / left / right / outer, `left_on` & `right_on`, `suffixes`, `indicator`, `pd.concat` |
| 12 | [`titanic_data_cleaning.ipynb`](Notebook/titanic_data_cleaning.ipynb) | **Data cleaning walkthrough** | missing values, dropping vs filling, duplicates, dtypes, outliers with the IQR rule, capping, text cleanup + 6 exercises |
| 13 | [`netflix_data_analysis_notebook.ipynb`](Netflix_Data_Analysis/netflix_data_analysis_notebook.ipynb) | **125-question practice workbook** | everything above, applied end to end on the Netflix catalogue |

---

## The Netflix workbook

[`Netflix_Data_Analysis/netflix_data_analysis_notebook.ipynb`](Netflix_Data_Analysis/netflix_data_analysis_notebook.ipynb) is the capstone:
**125 questions, all answered**, each with the pandas code and a short comment
explaining *why* that code is the right tool. It lives in its own folder because it is
a workbook rather than a topic lesson. A few answers (for example Q9 and Q12 in
Section A) are followed by a markdown cell that reads the output back in words.

| Section | Topic | Questions |
|---------|-------|-----------|
| A | First analysis of the data | Q1 – Q15 |
| B | Selection with `[]`, `.loc`, `.iloc` | Q16 – Q40 |
| C | Conditions with `.loc` | Q41 – Q60 |
| D | Sorting | Q61 – Q70 |
| E | Updating data | Q71 – Q85 |
| F | GroupBy | Q86 – Q105 |
| G | Cleaning | Q106 – Q125 |

It runs as one continuous story: Section B sets and resets the index, Section E adds
the derived columns (`age_years`, `is_movie`, `era`, `title_length`), Section F groups
by them, and Section G fixes the messy parts — `date_added` is still text until
`pd.to_datetime` turns it into a real date, `duration` mixes `"90 min"` with
`"2 Seasons"`, and three rows have a duration sitting in the `rating` column. The last
cell writes the cleaned result to `data/netflix_clean.csv`.

---

## Data Manipulation with Pandas (Part I & II)

Two long-form notebooks in [`Data Manipulation/`](Data%20Manipulation/) that go deeper
into how pandas works under the hood. They follow the structure of *Chapter 3 — Data
Manipulation with Pandas* of Jake VanderPlas's **Python Data Science Handbook**, worked
through cell by cell.

| Notebook | Size | Topics |
|----------|------|--------|
| [`Data Manipulation with Pandas Part I.ipynb`](Data%20Manipulation/Data%20Manipulation%20with%20Pandas%20Part%20I.ipynb) | 291 code cells | `Series`, `DataFrame` and `Index` objects · data indexing & selection (`loc`, `iloc`) · ufuncs and index alignment · handling missing data (`None` vs `NaN`, `isnull`, `dropna`, `fillna`) · hierarchical indexing (`MultiIndex`, `stack`/`unstack`) · `pd.concat` and `append` · `pd.merge` and join types · aggregation & `groupby` (split–apply–combine) · pivot tables · vectorized string operations · worked examples on **US birth-rate** data and a **recipe database** |
| [`Data Manipulation with Pandas part II.ipynb`](Data%20Manipulation/Data%20Manipulation%20with%20Pandas%20part%20II.ipynb) | 68 code cells | dates and times (`datetime`, `dateutil`, `datetime64`) · `Timestamp`, `Period`, `Timedelta` · indexing by time · `pd.date_range` · frequencies & offsets · resampling, shifting and rolling windows · worked example: **Seattle Fremont Bridge bicycle counts** · high-performance pandas with `pd.eval()`, `DataFrame.eval()` and `DataFrame.query()` |

> **Datasets:** these two notebooks were run against CSV/JSON files stored locally
> (`births.csv`, `state-population.csv`, `state-areas.csv`, `state-abbrevs.csv`,
> `recipeitems-latest.json`, `FremontBridge.csv`). They are not included in `data/`; the
> outputs are saved in the notebooks, so they can be read on GitHub as they are. To re-run
> them, download the files from the
> [Python Data Science Handbook repository](https://github.com/jakevdp/PythonDataScienceHandbook)
> and update the `read_csv` paths.

---

## Coursera — Introduction to Data Science in Python

The lecture notebooks from **Course 1** of the University of Michigan's
*Applied Data Science with Python* specialization on Coursera, kept in
[`Coursera_Intro_to_Data_Science/`](Coursera_Intro_to_Data_Science/) and numbered in
the order they appear in the course.

| # | Notebook | What it covers |
|---|----------|----------------|
| 01 | [`01_Series_Data_Structure.ipynb`](Coursera_Intro_to_Data_Science/01_Series_Data_Structure.ipynb) | Creating a `Series` from lists and dicts, `None` vs `NaN`, index labels |
| 02 | [`02_Querying_a_Series.ipynb`](Coursera_Intro_to_Data_Science/02_Querying_a_Series.ipynb) | `iloc` / `loc`, vectorized operations vs loops (timed with `%timeit`), broadcasting, appending Series |
| 03 | [`03_DataFrame_Data_Structure.ipynb`](Coursera_Intro_to_Data_Science/03_DataFrame_Data_Structure.ipynb) | Building DataFrames, selecting rows/columns, chaining, dropping and adding columns |
| 04 | [`04_DataFrame_Indexing_and_Loading.ipynb`](Coursera_Intro_to_Data_Science/04_DataFrame_Indexing_and_Loading.ipynb) | Loading CSVs with `read_csv`, `index_col`, renaming and cleaning column names |
| 05 | [`05_Querying_a_DataFrame.ipynb`](Coursera_Intro_to_Data_Science/05_Querying_a_DataFrame.ipynb) | Boolean masking, `where`, `dropna`, combining conditions with `&` and `\|` |
| 06 | [`06_Indexing_DataFrames.ipynb`](Coursera_Intro_to_Data_Science/06_Indexing_DataFrames.ipynb) | `set_index`, `reset_index`, multi-level (hierarchical) indexes on census data |
| 07 | [`07_Missing_Values.ipynb`](Coursera_Intro_to_Data_Science/07_Missing_Values.ipynb) | Detecting missing data with `isnull`, `dropna`, `fillna` with `ffill` / `bfill`, `replace` with regex |
| 08 | [`08_Example_Manipulating_DataFrame.ipynb`](Coursera_Intro_to_Data_Science/08_Example_Manipulating_DataFrame.ipynb) | Cleaning a list of US presidents: `str.split`, `str.extract`, `apply` with custom functions, dates |
| 09 | [`09_Merging_DataFrames.ipynb`](Coursera_Intro_to_Data_Science/09_Merging_DataFrames.ipynb) | Relational theory, inner/outer/left/right joins with `pd.merge`, `pd.concat` on College Scorecard data |
| 10 | [`10_Pandas_Idioms.ipynb`](Coursera_Intro_to_Data_Science/10_Pandas_Idioms.ipynb) | Writing "pandorable" code: method chaining, `apply` vs vectorization, timing with `timeit` |
| 11 | [`11_DataFrame_Manipulation_Practice.ipynb`](Coursera_Intro_to_Data_Science/11_DataFrame_Manipulation_Practice.ipynb) | Practice notebook: scraping tables with `pd.read_html` and re-running the idioms examples |
| 12 | [`12_Group_By.ipynb`](Coursera_Intro_to_Data_Science/12_Group_By.ipynb) | Split–apply–combine: aggregation, transformation, filtering and `apply` on census and Airbnb listings data |
| 13 | [`13_Scales.ipynb`](Coursera_Intro_to_Data_Science/13_Scales.ipynb) | Ratio / interval / ordinal / nominal scales, ordered `category` dtype, `pd.cut` for binning |
| 14 | [`14_Pivot_Tables.ipynb`](Coursera_Intro_to_Data_Science/14_Pivot_Tables.ipynb) | `pivot_table` with several aggregations and margins on world university rankings data |
| 15 | [`15_Date_Functionality.ipynb`](Coursera_Intro_to_Data_Science/15_Date_Functionality.ipynb) | `Timestamp`, `Period`, `DatetimeIndex`, `PeriodIndex`, `to_datetime`, `Timedelta`, offsets, dates in a DataFrame |
| 16 | [`16_Basic_Statistical_Testing.ipynb`](Coursera_Intro_to_Data_Science/16_Basic_Statistical_Testing.ipynb) | Hypothesis testing, p-values and Student's t-test with `scipy.stats.ttest_ind` |

> **Datasets:** the lectures read from a `datasets/` folder provided inside the Coursera
> Jupyter environment (`census.csv`, `Admission_Predict.csv`, `presidents.csv`,
> `cwurData.csv`, `listings.csv`, `grades.csv`, College Scorecard files, …). Those files
> are not redistributed here — the notebooks are kept with their outputs for reading and
> revision. To re-run a notebook, place the matching dataset in a `datasets/` folder next
> to it.

---

## Datasets

| File | Rows | Used by | Source |
|------|------|---------|--------|
| `data/titanic_dataset.csv` | 1,309 | notebooks 1, 6, 9, 12 | classic Titanic passenger list |
| `data/data.csv` | 50 | notebook 2 | generated inside notebook 2 |
| `data/nepali_data.csv` | 1,000 | notebooks 1, 6, 7 | generated inside notebook 2 (seeded, so it is reproducible) |
| `data/netflix_titles.csv` | 8,807 | notebook 13 | Kaggle — ["Netflix Movies and TV Shows"](https://www.kaggle.com/datasets/shivamb/netflix-shows) by Shivam Bansal |
| `data/netflix_clean.csv` | 8,797 | — | written by the last cell of notebook 13 |

### About the Netflix files

Both Netflix CSVs are **committed to the repository** (~3 MB each), so notebook 13
runs straight after a clone — no Kaggle download needed. `netflix_clean.csv` is the
cleaned output of the workbook and is kept in the repo so the result of the cleaning
can be inspected without re-running all 125 cells.

`data/titanic_clean.csv` is still git-ignored, because running notebook 12
regenerates it.

---

## Running the notebooks

```bash
git clone https://github.com/Yugalpoudel07/Pandas_For_Data_Science.git
cd Pandas_For_Data_Science

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install -r requirements.txt
jupyter notebook
```

Then open anything in `Notebook/` — or the workbook in
`Netflix_Data_Analysis/` — and choose **Run All**.

The *Data Manipulation* and *Coursera* notebooks also use `scipy`, `seaborn`, `lxml`
(for `pd.read_html`) and `numexpr` (for `pd.eval`) — all listed in `requirements.txt`.

Tested with **Python 3.11** and **pandas 2.3**.

---

## Quick reference

A cheat sheet of everything covered, so you don't have to hunt through the notebooks.

### Loading and first look

| Goal | Code |
|------|------|
| Load a CSV | `pd.read_csv("../data/file.csv")` |
| First / last rows | `df.head(n)` · `df.tail(n)` |
| Size | `df.shape` |
| Types + missing counts | `df.info()` |
| Numeric summary | `df.describe()` |
| Text summary | `df.describe(include="object")` |
| Missing per column | `df.isna().sum()` |
| Worst columns first | `df.isna().sum().sort_values(ascending=False)` |
| Real memory usage | `df.info(memory_usage="deep")` |
| Duplicated rows | `df.duplicated().sum()` |

### Selecting

| Goal | Code |
|------|------|
| One column as a Series | `df["col"]` |
| One column as a DataFrame | `df[["col"]]` |
| Several columns | `df[["a", "b"]]` |
| By label | `df.loc[label]` — end **included** |
| By position | `df.iloc[pos]` — end **excluded** |
| Rows + columns | `df.loc[condition, ["a", "b"]]` |

### Filtering

| Goal | Code |
|------|------|
| One condition | `df.loc[df["Age"] > 30]` |
| AND / OR / NOT | `&` · `\|` · `~` (each condition in its own brackets) |
| One of several values | `df.loc[df["col"].isin([...])]` |
| Range | `df.loc[df["col"].between(lo, hi)]` |
| Text match | `df.loc[df["col"].str.contains("x", na=False)]` |
| Missing / not missing | `df["col"].isna()` · `df["col"].notna()` |

### Changing data

| Goal | Code |
|------|------|
| Add / update safely | `df.loc[condition, "col"] = value` |
| New calculated column | `df["new"] = df["a"] * 2` |
| Rename columns | `df.rename(columns={"old": "new"})` |
| Change dtype | `df["col"].astype("int32")` |
| Drop columns / rows | `df.drop(columns=[...])` · `df.drop(index=[...])` |

> **Never** write `df[condition]["col"] = value`. That is chained indexing — the value
> lands in a temporary copy and `df` is left unchanged. Use `.loc` instead.

### Grouping and joining

| Goal | Code |
|------|------|
| Rows per group | `df.groupby("col").size()` |
| One statistic | `df.groupby("col")["x"].mean()` |
| Several statistics | `.agg(["mean", "max"])` |
| Per-column function | `.agg({"Fare": "mean", "Age": "median"})` |
| Two-level group as a table | `df.groupby(["a", "b"]).size().unstack()` |
| Group value on every row | `df.groupby("a")["x"].transform("mean")` |
| Join on a key | `pd.merge(a, b, on="key", how="inner")` |
| Stack tables | `pd.concat([a, b], ignore_index=True)` |

### Cleaning

| Goal | Code |
|------|------|
| Fill missing | `df["col"].fillna(value)` |
| Fill with the most common value | `df["col"].fillna(df["col"].mode()[0])` |
| Drop rows with gaps | `df.dropna(subset=["col"])` |
| Remove repeated rows | `df.drop_duplicates()` |
| Strip whitespace | `df["col"].str.strip()` |
| Text → date | `pd.to_datetime(df["col"], format="%B %d, %Y")` |
| Parts of a date | `.dt.year` · `.dt.month_name()` |
| Pull a number out of text | `df["col"].str.extract(r"(\d+)").astype(float)` |
| Save the result | `df.to_csv("../data/clean.csv", index=False)` |

---

## Notes

- `.loc` slices **include** the end label; `.iloc` slices **exclude** the end position.
- `size()` counts rows, `count()` counts non-missing values — the gap between them is
  exactly what is missing.
- The mean of a 0/1 column is a **rate** (that is how survival rate and "% that are
  movies" are calculated).
- Most pandas methods return a **copy**. Reassign the result or pass `inplace=True`,
  otherwise nothing changes.

---

## Related repositories

Part of my data-science learning series:

| Repository | Focus |
|------------|-------|
| [Python_Fundamentals](https://github.com/Yugalpoudel07/Python_Fundamentals) | Core Python — variables to OOP, file and exception handling, regex |
| [Numpy_For_Data_Science](https://github.com/Yugalpoudel07/Numpy_For_Data_Science) | NumPy arrays, ufuncs, broadcasting, fancy indexing |
| **Pandas_For_Data_Science** | *(this repo)* |
| [Matplotlib_and_Seaborn_For_Data_Science](https://github.com/Yugalpoudel07/Matplotlib_and_Seaborn_For_Data_Science) | Data visualization with Matplotlib and Seaborn |

---

## License

MIT — free to use for learning.
