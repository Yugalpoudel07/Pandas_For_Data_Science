# Pandas for Data Science

My complete, runnable notes on Python's **pandas** library — from `pd.Series` all the
way to cleaning a real 8,800-row dataset.

Every notebook is written as **notes + code**: a short markdown explanation of the
topic, then the code that demonstrates it, then a *Key takeaways* table at the end.
All notebooks run top to bottom without errors and are committed **with their
outputs**, so you can read them straight on GitHub without installing anything.

```
13 notebooks · 485 code cells · 244 explanation cells · 4 datasets
```

---

## Repository layout

```
Pandas_For_Data_Science/
├── Notebook/                          # notebooks 1–12, one topic each
├── Netflix_125_questions_workbook/    # notebook 13, the capstone workbook
├── data/                              # all CSV files used by the notebooks
├── requirements.txt
├── .gitignore
└── README.md
```

Notebooks read their data with a relative path — `pd.read_csv("../data/file.csv")`.
Both notebook folders sit **one level below the repository root**, so that same
`../data/...` path works from either of them — nothing to change after cloning.

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
| 13 | [`netflix_125_question_workbook.ipynb`](Netflix_125_questions_workbook/netflix_125_question_workbook.ipynb) | **125-question practice workbook** | everything above, applied end to end on the Netflix catalogue |

---

## The Netflix workbook

`Netflix_125_questions_workbook/netflix_125_question_workbook.ipynb` is the capstone:
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
git clone https://github.com/<your-username>/Pandas_For_Data_Science.git
cd Pandas_For_Data_Science

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install -r requirements.txt
jupyter notebook
```

Then open anything in `Notebook/` — or the workbook in
`Netflix_125_questions_workbook/` — and choose **Run All**.

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

## License

MIT — free to use for learning.
