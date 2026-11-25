# 🎬 What Makes a Hindi Film Score Well on IMDb?

A data analysis project that explores which factors (genre, runtime, release month, sequels, and director track record) are linked to higher IMDb ratings for Hindi-language Indian feature films. The workflow combines **Python (pandas)** for data preparation with **SQL (SQLite)** for analysis, and **matplotlib/seaborn** for visualization.

---

## 📌 Project Overview

- **Goal:** Identify data-backed recommendations a production house could use to make better-rated Hindi films.
- **Scope:** 3,173 matched Hindi feature films from India → 156 unrated films dropped → **3,017 rated films** analysed.
- **Target metric:** IMDb rating.

---

## 📂 Data Sources

| Dataset | Description |
|---|---|
| `TMDB_movie_dataset_v11.csv` | TMDB movie dataset (~1.5M rows, 24 columns). Filtered to Hindi (`hi`) films produced in India → 6,257 records |
| `hindi_films_imdb_1980-2023.csv` | IMDb details for Hindi films (1980–2023): rating, genre, actors, director, etc. |
| `READY_hindi_films_with_month_runtime_genre.csv` | Prepared features: release month, runtime in minutes, primary genre, main director, sequel flag |

The three datasets are joined on `imdb_id`.

> ⚠️ Raw CSV files are not included in this repo due to size. Download them from their original sources and update the file paths in the notebook.

---

## 🛠️ Tech Stack

- **Python 3.13**
- **pandas** – data loading, filtering, cleaning
- **SQLite + SQLAlchemy + ipython-sql** – storage and SQL analysis
- **matplotlib / seaborn** – visualizations
- **Jupyter Notebook**

---

## 🔄 Workflow

1. **Load & explore** the TMDB dataset (shape, columns, null checks).
2. **Filter** to Hindi-language films produced in India.
3. **Load into SQLite** (`movies.db`) and load the two IMDb datasets as additional tables.
4. **Join** all three tables on `imdb_id` and export to `hindi_movies_final_joined.csv`.
5. **Clean:** create a `rated_films` view that removes films with missing/invalid ratings.
6. **Analyse with SQL:**
   - Average rating by primary genre
   - Average rating by release month
   - Average rating by runtime band
   - Sequels vs. originals
   - Director track record (using window functions)
7. **Visualize** the key results.

---

## 🔍 Key Findings & Recommendations

### 1. Prioritize high-performing genres
- **Biography** leads with an average rating of **6.86** (46 films), followed by **Crime** (**6.19**, 173 films) and **Drama** (**6.11**, 788 films).
- **Horror** (**4.76**) and pure **Musicals** (**4.86**) underperform.

### 2. Target optimal runtimes (130–160 min)
- Films in the 130–160 min and 160+ min bands score higher on average than films under 100 minutes.

### 3. Back directors with proven track records
- Using SQL window functions, directors with a prior average rating of **7.0+** tend to produce higher-rated subsequent films than first-time or low-scoring directors.

---

## ⚠️ Limitations

1. **Ratings ≠ box office.** IMDb scores reflect audience/critic sentiment, not commercial success.
2. **Missing runtime data** for some older or obscure films, so runtime analysis uses a subset.
3. **Heuristic sequel tagging.** `sequel_guess` relies on title keywords (e.g. `2`, `3`, `Returns`, `Again`) and may miss sequels with unrelated titles.

---

## 🚀 How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. Install dependencies
pip install pandas sqlalchemy ipython-sql prettytable==3.11.0 matplotlib seaborn jupyter

# 3. Place the datasets in a local folder and update the file paths in the notebook

# 4. Launch the notebook
jupyter notebook IMDB2.ipynb
```

---

## 📁 Repository Structure

```
├── IMDB_Analysis.ipynb              # Main analysis notebook
├── README.md                        # Project documentation
└── data/                            # (optional) place datasets here
```

---

## 👤 Author

**Niranjan Kumar**
[GitHub](https://github.com/Niranjansah91) · [LinkedIn](https://www.linkedin.com/in/niranjansah121)
