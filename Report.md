# Netflix Data Analysis — Report

**Project:** Netflix Titles EDA
**Tool:** Python (pandas, matplotlib, numpy)
**Dataset:** netflix_titles.csv
**Notebook:** netflix_data_analysis.ipynb

---

## 1. Introduction

This report documents the exploratory data analysis conducted on the Netflix titles dataset. The objective was to uncover patterns in Netflix's global content library — understanding how content is distributed across countries, genres, content types, ratings, and years. The analysis also examines duration trends and genre preferences at a country level.

---

## 2. Dataset Overview

The dataset contains metadata for thousands of Netflix titles, including both Movies and TV Shows. Key fields include country of origin, genre (listed_in), content rating, release year, duration, cast, and director.

The dataset was loaded using pandas and explored through `.head()`, `.tail()`, `.dtypes`, and `.isnull().sum()` to understand its shape and quality.

---

## 3. Data Cleaning

Several data quality issues were addressed before analysis:

**Missing Values**

The following columns had null entries and were filled using appropriate strategies:

| Column | Strategy Used |
|---|---|
| `cast` | Backward fill (bfill) |
| `director` | Forward fill (ffill) |
| `country` | Forward fill (ffill) |
| `date_added` | Forward fill (ffill) |
| `rating` | Forward fill (ffill) |
| `duration` | Forward fill (ffill) |

Forward fill propagates the last known value forward, while backward fill uses the next known value. These strategies were applied as reasonable approximations given the nature of the data.

**Column Renaming**

The column `listed_in` was renamed to `genre` for improved readability across all subsequent analyses.

**Duplicate Detection**

A check for fully duplicated rows was performed. Any detected duplicates were printed for review, ensuring the integrity of all downstream visualizations and counts.

---

## 4. Exploratory Analysis & Visualizations

### 4.1 Movies vs TV Shows by Country (Top 10)

**Method:** Grouped bar chart using `groupby(['country', 'type']).size().unstack()`

**Findings:**
- The United States leads with the highest combined count of Movies and TV Shows by a significant margin.
- India ranks second, driven primarily by Movies.
- The United Kingdom, Canada, and Japan round out the top five.
- Most countries have a noticeably higher proportion of Movies compared to TV Shows, reflecting Netflix's content acquisition strategy.

**Chart Colors:** Red (`#E50914`) for Movies, Dark (`#221F1F`) for TV Shows — aligned with Netflix's brand palette.

---

### 4.2 Genre Preference by Country — TV Shows (Heatmap)

**Method:** Pivot table of country vs genre for TV Shows, displayed as an `imshow` heatmap using the `Blues` colormap.

**Scope:** Top 10 countries and Top 10 genres.

**Findings:**
- The United States dominates across nearly all genre categories for TV Shows.
- "International TV Shows" appears strongly for countries like South Korea, Japan, and India — indicating that Netflix categorizes non-English content under this genre.
- TV Dramas and Crime TV Shows are concentrated predominantly in the US and UK.
- Kids' TV content is prominent in the US and Canada.

---

### 4.3 Genre Trend Across Countries — TV Shows (Line Chart)

**Method:** Percentage-normalized line chart (`pivot_pct`) plotting each genre's share of a country's TV Show library.

**Scope:** Top 10 countries, Top 10 genres.

**Findings:**
- "International TV Shows" dominates in India, South Korea, and Japan, often representing over 50% of their TV content on Netflix.
- In the United States and United Kingdom, Dramas and Crime TV Shows hold relatively higher shares.
- Comedies and Kids' TV have a more uniform distribution across countries.
- This chart reveals that genre preferences vary significantly by region, suggesting Netflix curates country-specific content libraries.

---

### 4.4 Genre Trend Over the Years (2000 – Present)

**Method:** Multi-line chart tracking yearly content count per genre from 2000 onwards.

**Findings:**
- Content volume across all genres remained low and relatively flat from 2000 through approximately 2012.
- A sharp and consistent rise began around 2015, coinciding with Netflix's global expansion and its shift toward original content production.
- "International Movies" and "Dramas" show the steepest growth curves.
- "Documentaries" and "Action & Adventure" also increased significantly post-2015.
- There is a visible plateau or slight decline in counts for recent years (2020–2021), likely due to production slowdowns and the dataset's capture date.

---

### 4.5 Top 15 Countries by Total Content

**Method:** Horizontal bar chart (`barh`) sorted by total content count.

**Findings:**
- The **United States** is the single largest contributor, with a count far exceeding all others.
- **India** ranks second, reflecting Netflix's major investment in Indian original and licensed content.
- **United Kingdom**, **Canada**, and **France** follow.
- Countries such as **South Korea**, **Japan**, and **Spain** are notable for their growing footprints, particularly in TV Show content.

---

### 4.6 Movie Distribution by Release Year

**Method:** Vertical bar chart, peak year highlighted in gold.

**Findings:**
- Movie releases on Netflix grew steadily from 2000, accelerating sharply from 2015.
- The peak year for movie releases sits in the **2017–2019** range (exact year determined dynamically by the notebook).
- The peak bar is highlighted in gold for visual emphasis.
- Post-peak, there is a visible decline, which may reflect shifts in Netflix's strategy from licensing existing movies toward producing originals.

---

### 4.7 TV Show Distribution by Release Year

**Method:** Vertical bar chart with dark fill and gold peak year highlight.

**Findings:**
- TV Show releases show a consistent upward trajectory from 2000 onward.
- The peak year for TV Show releases is more recent than for movies, suggesting Netflix is increasingly investing in serialized content.
- The growth is particularly pronounced post-2015, consistent with the genre trend analysis in Section 4.4.

---

### 4.8 Average Content Duration by Country

**Method:** Two side-by-side horizontal bar charts.
- Left: Average movie duration in minutes (top 10 countries by movie count)
- Right: Average TV Show seasons (top 10 countries by TV Show count)

**Findings:**

**Movies:**
- India and certain Asian markets tend to produce longer movies (often 120+ minutes on average) compared to Western countries.
- The United States and United Kingdom cluster around the 90–105 minute average, which is the Hollywood industry standard.

**TV Shows:**
- The United States leads in average number of seasons, reflecting long-running series common in American television.
- Countries like South Korea and Japan tend to have fewer seasons per show (often 1–2), consistent with their anthology or single-season drama format (e.g., K-dramas).

---

### 4.9 Rating Distribution — Movies vs TV Shows

**Method:** Grouped bar chart for top 8 ratings, split by content type.

**Findings:**
- **TV-MA** (Mature Audiences) is the most common rating across both Movies and TV Shows, indicating that Netflix's library skews toward adult content.
- **TV-14** is the second most prevalent rating.
- **TV-PG** and **PG-13** are present but less dominant.
- Movies tend to have a broader spread of ratings (G, PG, PG-13, R) compared to TV Shows, which are more concentrated in the TV-MA/TV-14 range.
- Very few titles carry a **G** or **TV-G** rating, reflecting limited family/children content relative to the total catalog.

---

## 5. Summary of Key Findings

| Dimension | Finding |
|---|---|
| Content Leader | United States dominates in both Movies and TV Shows |
| Fastest Growing Market | India (Movies), South Korea (TV Shows) |
| Most Popular Genre | International Movies, Dramas |
| Peak Movie Year | 2017–2019 |
| Peak TV Show Year | 2019–2020 |
| Dominant Rating | TV-MA |
| Longest Movies (Avg) | India |
| Fewest Seasons (Avg) | South Korea, Japan |
| Genre Most Tied to a Country | International TV Shows → India, Japan, South Korea |

---

## 6. Limitations

- Missing values were filled using forward/backward fill, which may introduce slight inaccuracies in country and director attribution.
- The dataset is a static snapshot; it does not reflect Netflix's current catalog.
- Genre analysis is based on the primary genre string, which can include multiple genres per title — the explode approach was used to address this.
- Duration data for TV Shows (measured in seasons) does not capture within-season episode counts, which could be relevant for viewership analysis.

---

## 7. Tools & Libraries

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, grouping, pivoting |
| `matplotlib` | All visualizations (bar charts, heatmaps, line charts) |
| `numpy` | Array operations for chart positioning |

---

## 8. Conclusion

This analysis reveals that Netflix's content library is heavily skewed toward American productions, adult-rated content, and dramatic genres. However, the platform's international growth — particularly in India, South Korea, and Japan — is clearly reflected in the data, with these markets showing strong genre preferences and growing content volume. The period from 2015 to 2020 represents Netflix's golden era of content growth, with a noticeable shift in focus from movies to serialized TV content in recent years. These insights can inform content acquisition decisions, regional marketing strategies, and genre investment priorities.
