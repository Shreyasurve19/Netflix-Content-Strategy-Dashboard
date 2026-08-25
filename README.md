# Netflix Content Strategy Dashboard

A data analysis and Power BI dashboard project that explores Netflix Movies and TV Shows to understand the platform's content mix, content additions over time, major content-producing countries, popular genres, ratings, movie duration, and the age of content when it was added.

The project uses **Python and Pandas in Google Colab for data cleaning, calculations and exploratory data analysis (EDA)**, while **Microsoft Power BI is used for interactive data visualization and dashboard creation**.

---

## 📌 Project Overview

Netflix has a large and diverse catalog of movies and TV shows. Analyzing this catalog can help identify patterns in content type, geographic contribution, genres, ratings, and content addition trends.

This project analyzes the Netflix titles dataset and converts the raw data into a cleaned dataset and an interactive Power BI dashboard.

### Main Questions

The project focuses on the following questions:

* How is Netflix's catalog divided between Movies and TV Shows? (C1)
* How has the number of titles added to Netflix changed over the years in this dataset? (C2)
* Which countries contribute the most titles to Netflix's catalog in this dataset? (C3)
* Which genres/categories are most commonly represented in Netflix's catalog? (C4)
* Which content ratings are most common in Netflix's catalog? (C5)
* What is the typical duration of Movies in the Netflix catalog?
* How old was Netflix content, on average, when it was added to the catalog? (C6)
* Are titles added to Netflix evenly throughout the year, or are some months more active than others?
* Did the growth pattern differ between Movies and TV Shows over the years?
* Do Movies and TV Shows have different dominant genres/categories?

---

# 📊 Dataset

## Dataset Source

The project uses the **Netflix Movies and TV Shows** dataset available on Kaggle.

**Original Dataset:**
https://www.kaggle.com/shivamb/netflix-shows

The original dataset contains **8,807 rows and 12 columns** and includes information about Netflix movies and TV shows such as title, type, director, cast, country, date added, release year, rating, duration, genre/category and description.

### Original Dataset Size

* **Rows:** 8,807
* **Columns:** 12
* **Duplicate rows:** 0

### Original Columns

| Column         | Description                                 |
| -------------- | ------------------------------------------- |
| `show_id`      | Unique identifier for each title            |
| `type`         | Movie or TV Show                            |
| `title`        | Title name                                  |
| `director`     | Director of the title                       |
| `cast`         | Cast members                                |
| `country`      | Country/countries associated with the title |
| `date_added`   | Date when the title was added to Netflix    |
| `release_year` | Original release year                       |
| `rating`       | Content rating                              |
| `duration`     | Movie duration or number of TV show seasons |
| `listed_in`    | Genre/category information                  |
| `description`  | Short description of the title              |

---

# 🧹 Data Cleaning

Data cleaning and preprocessing were performed using **Python and Pandas in Google Colab**.

## Initial Data Inspection

The original dataset had:

* **8,807 rows**
* **12 columns**
* Missing values in 6 columns
* No duplicate rows

### Initial Missing Values

| Column       | Missing Values |
| ------------ | -------------: |
| `director`   |          2,634 |
| `cast`       |            825 |
| `country`    |            831 |
| `date_added` |             10 |
| `rating`     |              4 |
| `duration`   |              3 |

The remaining columns had no missing values.

## Cleaning Steps

The following preprocessing steps were performed:

1. Loaded the raw Netflix dataset into Pandas.
2. Inspected dataset shape, columns and data types.
3. Checked missing values.
4. Checked duplicate rows.
5. Handled missing values in relevant columns.
6. Converted `date_added` into proper datetime format.
7. Extracted the year from `date_added`.
8. Extracted the month from `date_added`.
9. Calculated the age of content when it was added to Netflix.
10. Separated duration into a numeric value and a duration unit.
11. Checked for invalid/negative calculated content-age values.
12. Verified the cleaned dataset for remaining missing values.
13. Verified duplicate rows again.
14. Prepared the cleaned dataset for Power BI visualization.

---

# 🔄 Feature Engineering

Five additional columns were created during preprocessing.

### `year_added`

The year in which the title was added to Netflix.

### `month_added`

The month in which the title was added to Netflix.

### `content_age_when_added`

Calculated as:

```text
Year Added - Release Year
```

This helps identify how old a movie or TV show was when it was added to Netflix.

### `duration_value`

The numerical part of the original `duration` column.

Examples:

```text
90 min → 90
2 Seasons → 2
```

### `duration_unit`

Identifies whether the duration represents:

* Minutes
* Seasons

---

# ✅ Final Dataset

After cleaning and feature engineering:

* **Final rows:** 8,790
* **Final columns:** 17
* **Missing values:** 0
* **Duplicate rows:** 0

### Final Columns

```text
show_id
type
title
director
cast
country
date_added
release_year
rating
duration
listed_in
description
year_added
month_added
content_age_when_added
duration_value
duration_unit
```

---

# 🔎 Exploratory Data Analysis

All major calculations and analytical checks were performed in **Google Colab using Python/Pandas**.

**Power BI was used only for the final dashboard visualizations and interactive analysis.**

---

## 1. Content Type Distribution — (C1)

The final dataset contains:

| Type      |     Count | Percentage |
| --------- | --------: | ---------: |
| Movie     |     6,126 |     69.69% |
| TV Show   |     2,664 |     30.31% |
| **Total** | **8,790** |   **100%** |

### Insight

Netflix's catalog in this dataset is more heavily composed of **Movies**, with nearly **70% of the titles being Movies**.

---

## 2. Content Additions by Year — (C2)

The number of titles added to Netflix changed considerably over the years.

| Year | Titles Added |
| ---- | -----------: |
| 2008 |            2 |
| 2009 |            2 |
| 2010 |            1 |
| 2011 |           13 |
| 2012 |            3 |
| 2013 |           11 |
| 2014 |           24 |
| 2015 |           82 |
| 2016 |          426 |
| 2017 |        1,185 |
| 2018 |        1,648 |
| 2019 |    **2,016** |
| 2020 |        1,879 |
| 2021 |        1,498 |

### Insight

The dataset shows **rapid growth in Netflix's catalog additions from 2016 onward**, with the **highest number of titles added in 2019**.

---

## 3. Top Countries — (C3)

Country information was separately processed because some records contain multiple countries in the same cell.

| Country        | Titles |
| -------------- | -----: |
| United States  |  3,681 |
| India          |  1,046 |
| United Kingdom |    805 |
| Canada         |    445 |
| France         |    393 |
| Japan          |    316 |
| Spain          |    232 |
| South Korea    |    231 |
| Germany        |    226 |

### Insight

The **United States** has the highest representation in the Netflix dataset, followed by **India** and the **United Kingdom**.

---

## 4. Top Genres/Categories — (C4)

The `listed_in` column contains multiple genres/categories for some titles, so the genres were separated into individual rows for analysis.

### Overall Top Categories

| Category                 | Count |
| ------------------------ | ----: |
| International Movies     | 2,752 |
| Dramas                   | 2,426 |
| Comedies                 | 1,674 |
| International TV Shows   | 1,349 |
| Documentaries            |   869 |
| Action & Adventure       |   859 |
| TV Dramas                |   762 |
| Independent Movies       |   756 |
| Children & Family Movies |   641 |
| Romantic Movies          |   616 |

### Insight

**International Movies** are the most frequently occurring category in the dataset, followed by **Dramas** and **Comedies**.

---

## 5. Content Ratings — (C5)

The most common content ratings are:

| Rating | Count |
| ------ | ----: |
| TV-MA  | 3,205 |
| TV-14  | 2,157 |
| TV-PG  |   861 |
| R      |   799 |
| PG-13  |   490 |

### Insight

**TV-MA** is the most common rating in the dataset, followed by **TV-14**.

---

## 6. Movie Duration

For Movies in the dataset:

* **Average duration:** 99.58 minutes
* **Median duration:** 98 minutes
* **Minimum duration:** 3 minutes
* **Maximum duration:** 312 minutes

### Insight

Movies in this Netflix dataset are typically **around 100 minutes long**, with both the average and median duration close to that value.

---

## 7. Content Age When Added — (C6)

The analysis found:

* **Average content age:** 4.69 years
* **Median content age:** 1 year
* **Minimum content age:** 0 years
* **Maximum content age:** 93 years

### Insight

The **median content age is only 1 year**, meaning at least half of the titles in this dataset were added to Netflix within about one year of their release year.

---

## 8. Content Additions by Month

| Month     | Titles Added |
| --------- | -----------: |
| January   |          737 |
| February  |          562 |
| March     |          741 |
| April     |          763 |
| May       |          632 |
| June      |          728 |
| July      |      **827** |
| August    |          754 |
| September |          769 |
| October   |          760 |
| November  |          705 |
| December  |      **812** |

### Insight

Titles are **not added evenly throughout the year**.

**July** has the highest number of recorded content additions in the dataset, followed by **December**, while **February** has the lowest.

---

## 9. Movies vs TV Shows Over the Years

The analysis compared the number of Movies and TV Shows added each year.

| Year |    Movies | TV Shows |
| ---- | --------: | -------: |
| 2008 |         1 |        1 |
| 2009 |         2 |        — |
| 2010 |         1 |        — |
| 2011 |        13 |        — |
| 2012 |         3 |        — |
| 2013 |         6 |        5 |
| 2014 |        19 |        5 |
| 2015 |        56 |       26 |
| 2016 |       251 |      175 |
| 2017 |       836 |      349 |
| 2018 |     1,237 |      411 |
| 2019 | **1,424** |      592 |
| 2020 |     1,284 |  **595** |
| 2021 |       993 |      505 |

### Insight

**Movies remained the larger share of Netflix's catalog additions** throughout the major growth period, while **TV Shows also increased substantially**.

The highest number of Movies added in a single year was **2019 (1,424)**, while the highest number of TV Shows added was **2020 (595)**.

---

## 10. Movies vs TV Shows — Dominant Genres/Categories

The genre/category distribution was also analyzed separately for Movies and TV Shows.

### Top 5 Movie Categories

| Category             | Count |
| -------------------- | ----: |
| International Movies | 2,752 |
| Dramas               | 2,426 |
| Comedies             | 1,674 |
| Documentaries        |   869 |
| Action & Adventure   |   859 |

### Top 5 TV Show Categories

| Category               | Count |
| ---------------------- | ----: |
| International TV Shows | 1,349 |
| TV Dramas              |   762 |
| TV Comedies            |   573 |
| Crime TV Shows         |   469 |
| Kids' TV               |   448 |

### Insight

Movies and TV Shows have **different dominant content categories**, but **international content is the largest category for both**.

For Movies, **International Movies** is the leading category, while **International TV Shows** is the leading category for TV Shows.


# 📊 Power BI Dashboard

The final dashboard was created using **Microsoft Power BI**.

Python/Colab was used for:

* Data cleaning
* Feature engineering
* Calculations
* EDA
* Analytical insights

Power BI was used for:

* Interactive visualizations
* KPI cards
* Charts
* Dashboard layout
* Filters/slicers

---

# 📌 Dashboard KPIs

The dashboard contains four main KPI cards.

### 1. Total Titles

**8,790**

### 2. Total Movies

**6,126**

### 3. Total TV Shows

**2,664**

### 4. Average Movie Duration

**99.58 minutes**

---

# 📈 Dashboard Visualizations

The dashboard contains six major visualizations.

### 1. Content Mix: Movies vs TV Shows

**Visual:** Donut chart

Shows the percentage distribution of Movies and TV Shows.

**Key result:**

* Movies — 69.69%
* TV Shows — 30.31%

---

### 2. Content Additions Over the Years

**Visual:** Line chart

Shows how the number of titles added changed from 2008 to 2021.

**Key result:**

2019 recorded the highest number of additions with **2,016 titles**.

---

### 3. Top 10 Countries by Titles

**Visual:** Horizontal bar chart

Shows the countries contributing the highest number of titles.

The United States ranks first, followed by India and the United Kingdom.

---

### 4. Top 10 Genres/Categories

**Visual:** Horizontal bar chart

Shows the most frequently occurring genres/categories after separating multi-valued genre entries.

---

### 5. Content Ratings Distribution

**Visual:** Column chart

Shows the distribution of content ratings.

**Key result:**

TV-MA is the most common rating.

---

### 6. Content Age When Added

**Visual:** Column chart

Shows the distribution of the number of years between a title's release year and its Netflix addition year.

---

# 🎛️ Dashboard Interactivity

The dashboard also includes filters/slicers for:

* **Type**

  * Movie
  * TV Show

* **Year Added**

These allow users to interactively explore the Netflix catalog.

---

# 💡 Key Findings

Based on the complete analysis:

1. **Netflix's catalog is more heavily composed of Movies**, with Movies representing **69.69%** of all titles in the dataset.
2. The dataset shows **rapid growth in catalog additions from 2016 onward**, with the **highest number of titles added in 2019 (2,016 titles)**.
3. The **United States** has the highest representation in the dataset, followed by **India** and the **United Kingdom**.
4. **International Movies** are the most frequently occurring category, followed by **Dramas** and **Comedies**.
5. **TV-MA** is the most common content rating, followed by **TV-14**.
6. Movies in the dataset are typically **around 100 minutes long**, with an average duration of **99.58 minutes** and a median of **98 minutes**.
7. The **median content age is 1 year**, meaning at least half of the titles were added to Netflix within about one year of their release year.
8. Content additions are **not evenly distributed throughout the year**. **July** has the highest number of recorded additions, followed by **December**, while **February** has the lowest.
9. **Movies remained the larger share of catalog additions** throughout the major growth period, although TV Show additions also increased substantially.
10. Movies and TV Shows have **different dominant categories**, but **international content is the largest category for both**.


---

# 🛠️ Technologies Used

* **Python**
* **Pandas**
* **Google Colab**
* **Microsoft Power BI**
* **Microsoft Excel**
* **Data Cleaning**
* **Exploratory Data Analysis**
* **Data Visualization**

---


# 🚀 How to Use This Project

### 1. Run the analysis

Open:

'Netflix_Content_Strategy_Analysis.ipynb'

The notebook contains the data loading, cleaning, feature engineering, calculations and EDA.

### 2. Open the dashboard

Open:

`PowerBI/Netflix_Content_Strategy_Dashboard.pbix`

using Microsoft Power BI Desktop.

### 3. Explore the dashboard

Use the available filters to explore Netflix content by type and year added.

---
# Author
Shreya Surve


---

