# Netflix Data Analysis

A Python-based exploratory data analysis (EDA) project on the Netflix titles dataset. This project investigates the content library across countries, genres, ratings, and release years using pandas and matplotlib.

---

## Project Overview

This notebook performs end-to-end analysis of Netflix's content catalog, including:

- Data cleaning and null value handling
- Renaming and restructuring columns
- Duplicate detection
- Visual exploration across multiple dimensions (country, genre, rating, year, duration)

---

## Dataset

**Source:** `netflix_titles.csv`

**Key Columns:**

| Column | Description |
|---|---|
| `show_id` | Unique identifier for each title |
| `type` | Movie or TV Show |
| `title` | Title of the content |
| `director` | Director name(s) |
| `cast` | Cast member(s) |
| `country` | Country of origin |
| `date_added` | Date added to Netflix |
| `release_year` | Year of release |
| `rating` | Content rating (e.g., TV-MA, PG-13) |
| `duration` | Duration in minutes (Movies) or seasons (TV Shows) |
| `listed_in` | Genre(s) — renamed to `genre` in this project |
| `description` | Short description of the title |

---

## Project Structure

```
netflix-data-analysis/
│
├── netflix_data_analysis.ipynb   # Main Jupyter Notebook
├── netflix_titles.csv            # Source dataset (not included)
├── README.md                     # Project documentation
└── Report.md                     # Analysis report with findings
```

---

## Setup & Requirements

**Python Version:** 3.7+

**Libraries:**

```
pandas
matplotlib
numpy
```

Install dependencies:

```bash
pip install pandas matplotlib numpy
```

---

## How to Run

1. Clone or download this repository.
2. Place `netflix_titles.csv` in the same directory as the notebook.
3. Open the notebook:

```bash
jupyter notebook netflix_data_analysis.ipynb
```

4. Run all cells sequentially (Kernel → Restart & Run All).

---

## Analysis Performed

### 1. Data Cleaning
- Filled missing values in `cast`, `director`, `country`, `date_added`, `rating`, and `duration` using forward-fill and backward-fill strategies.
- Renamed `listed_in` column to `genre` for clarity.
- Identified and reported duplicate rows.

### 2. Visualizations

| Chart | Description |
|---|---|
| Movies vs TV Shows by Country | Grouped bar chart for top 10 countries |
| Genre Heatmap (TV Shows) | Country vs genre matrix showing content density |
| Genre Trend by Country | Line chart — genre share (%) per country |
| Genre Trend Over Years | Line chart — content count per genre from 2000 to present |
| Top 15 Countries by Total Content | Horizontal bar chart |
| Movie Distribution by Release Year | Bar chart with peak year highlighted in gold |
| TV Show Distribution by Release Year | Bar chart with peak year highlighted in gold |
| Avg Duration by Country (Movies) | Horizontal bar — average runtime in minutes |
| Avg Seasons by Country (TV Shows) | Horizontal bar — average number of seasons |
| Rating Distribution | Grouped bar — Movies vs TV Shows per rating category |

---

## Key Findings

- The **United States** dominates Netflix's content library by a significant margin, followed by **India** and the **United Kingdom**.
- **International Movies** and **Dramas** are the most prevalent genres on the platform.
- Movie releases on Netflix peaked around **2017–2019**, after which growth slowed.
- TV Show production has seen a steady rise, especially post-2015.
- Most content is rated **TV-MA** (mature audiences), indicating Netflix's focus on adult content.
- Indian and South Korean content tends to have longer average movie runtimes compared to Western counterparts.

---

## Author

**Harsh**

---

## License

This project is for educational and analytical purposes only. The Netflix dataset is publicly available on Kaggle.
