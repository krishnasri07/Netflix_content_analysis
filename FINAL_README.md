
# Netflix Movies & Shows Analysis

---

## Project Overview
This project explores the **Netflix Movies and TV Shows** dataset to extract insights about:
- Popular genres
- Country distribution of content
- Most frequent actors
- Average movie duration
- Comparison with other streaming platforms

Performed using **Python**, **Pandas**, **Seaborn**, and **Matplotlib**.

---

## Table of Contents
- [Tech Stack](#tech-stack)
- [Dataset](#dataset)
- [Installation & Setup](#installation--setup)
- [Data Preprocessing](#data-preprocessing)
- [Key Findings](#key-findings)
- [Insights](#insights)
- [Conclusion](#conclusion)
- [References](#references)

---

## Tech Stack
- Python 3
- Pandas
- Matplotlib & Seaborn
- Google Colab / Jupyter Notebook

---

## Dataset
- [Netflix Movies and TV Shows — Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)
- [Movies on Streaming Platforms — Kaggle](https://www.kaggle.com/datasets/ruchi798/movies-on-netflix-prime-video-hulu-and-disney)

---

## Installation & Setup
Clone the repository and install the dependencies:
```bash
git clone <repository_url>
pip install pandas matplotlib seaborn
```
Or run the notebook directly in **Google Colab**.

---

## Data Preprocessing

The following steps were performed to clean and prepare the data:

1. **Handling Missing Values:**
```python
df['rating'].fillna(df['rating'].mode()[0], inplace=True)
df['duration'].fillna('0 min', inplace=True)
df.dropna(subset=['country'], inplace=True)
```
- Filling missing ratings with the most frequent rating.
- Filling missing durations with '0 min'.
- Dropping entries with missing country values.

2. **Date Transformation:**
```python
df['date_added'] = pd.to_datetime(df['date_added'], errors='coerce')
```
- Converting `date_added` field into DateTime format for time-series analysis.

3. **Extracting Movie Duration:**
```python
df['movie_duration'] = df['duration'].str.extract(r'(\d+)').astype(float)
```
- Extracted numeric value from duration (e.g., 90 min → 90).

4. **Feature Engineering:**
```python
df['year_added'] = df['date_added'].dt.year
```
- Extracted `year_added` to analyze trends over the years.

---

## Key Findings

### 1. Distribution of Movies & TV Shows

![Distribution of Movies and TV Shows](ed0f8847-e970-43b3-a984-1856e3772f4d.png)

---

### 2. Top 10 Most Common Genres on Netflix

![Top 10 Genres](439b04a9-55d6-4051-8639-f2848b30cdfc.png)

---

### 3. Top 10 Countries Producing Netflix Content

![Top 10 Countries](7dd07338-fdc3-45d3-9ae6-4d3dc8222020.png)

---

### 4. Top 10 Most Frequent Actors on Netflix

![Top 10 Actors](ebf90e11-60f9-4860-b9eb-56d824e634c9.png)

---

### 5. Yearly Trend of New Content Added

![Yearly Trend](bd2fb32a-45bb-4bfc-ad4c-a1c2aa747e99.png)

---

### 6. Average Movie Duration

![Average Movie Duration](467aac32-498c-4302-bce6-0b672db3c759.png)

---

### 7. Netflix vs Prime Video vs Disney+

![Platform Comparison](3802c832-6d11-427d-aa1d-ff05d60f7909.png)

---

## Insights
- **Movies dominate** Netflix’s content compared to TV Shows.
- **International Movies, Dramas, and Comedies** are the most popular genres.
- The **United States, India, and the UK** lead in content production.
- **Average movie duration** is approximately **100 minutes**.
- **Amazon Prime Video** has slightly more movies than Netflix.

---

## Conclusion
The analysis reveals Netflix’s commitment to international content and a rich diversity in genres, helping maintain its global dominance.

---

## References
- [Netflix Dataset - Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)
- [Movies on Streaming Platforms - Kaggle](https://www.kaggle.com/datasets/ruchi798/movies-on-netflix-prime-video-hulu-and-disney)
- [Pandas Documentation](https://pandas.pydata.org/)
- [Seaborn Documentation](https://seaborn.pydata.org/)
