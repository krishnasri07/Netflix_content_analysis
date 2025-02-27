# Netflix Movies & Shows Analysis

## Project Overview
This project analyzes the **Netflix Movies and TV Shows dataset** using **Python, Pandas, Seaborn, and Matplotlib**. The goal is to uncover insights about:
- Movie genres, top-rated content, and trends 
- Most common actors 
- Average duration of movies 
- Country-wise distribution 
- Comparison with Amazon Prime & Disney+ data 

## 🔧 Tech Stack
- **Python** 
- **Pandas** (Data manipulation)
- **Matplotlib & Seaborn** (Visualization)
- **Google Colab** (Execution)

## 📂 Dataset
The dataset is sourced from **Kaggle**: [Netflix Movies & TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows)

##  Steps to Run the Project
### 1️. Install Dependencies
```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

### 2️. Load the Dataset
```python
df = pd.read_csv("netflix_titles.csv")
df.head()
```

### 3️. Data Cleaning & Preprocessing
```python
# Handling missing values
df["rating"].fillna(df["rating"].mode()[0], inplace=True)
df["duration"].fillna("0 min", inplace=True)
df.dropna(subset=["country"], inplace=True)

# Convert 'date_added' to datetime
df["date_added"] = pd.to_datetime(df["date_added"], errors='coerce')
```

### 4️. Extract Movie Duration (Handling Seasons Issue)
```python
# Extract numeric duration for movies
df["movie_duration"] = df["duration"].str.extract(r'(\d+)')
df["movie_duration"] = pd.to_numeric(df["movie_duration"], errors='coerce')
```

### 5️. Data Analysis
#### 🔹 Most Common Genres
```python
plt.figure(figsize=(10,5))
sns.countplot(y=df['listed_in'].value_counts().index[:10], order=df['listed_in'].value_counts().index[:10])
plt.title("Top 10 Most Common Genres")
plt.show()
```

#### 🔹 Top 10 Countries with Most Content
```python
plt.figure(figsize=(12,6))
df['country'].value_counts()[:10].plot(kind='bar', color='skyblue')
plt.title("Top 10 Countries with Most Netflix Content")
plt.show()
```

#### 🔹 Yearly Trend of Content Added on Netflix
```python
plt.figure(figsize=(12, 6))
df["year_added"] = df["date_added"].dt.year
sns.countplot(x=df["year_added"], palette="Set2")
plt.xticks(rotation=45)
plt.title("Yearly Trend of Content Added on Netflix")
plt.xlabel("Year")
plt.ylabel("Count")
plt.show()

```

#### 🔹 Top 10 Most Frequent Actors on Netflix
```python
plt.figure(figsize=(12, 6))
sns.barplot(data=actor_df.head(10), x="Actor", y="Count", palette="coolwarm")
plt.xticks(rotation=45)
plt.title("Top 10 Most Common Actors on Netflix")
plt.show()
```

#### 🔹 Average Movie Duration
```python
avg_duration = df[df["type"] == "Movie"]["movie_duration"].mean()
print("Average duration of movies:", avg_duration, "minutes")
```

#### 🔹  Compare Netflix with Amazon Prime & Disney+
```python
df_compare = pd.read_csv("/content/MoviesOnStreamingPlatforms.csv")
platform_counts = df_compare[["Netflix", "Prime Video", "Disney+"]].sum()
plt.figure(figsize=(8, 6))
sns.barplot(x=platform_counts.index, y=platform_counts.values, palette="Set1")
plt.title("Number of Movies on Netflix vs Prime Video vs Disney+")
plt.xlabel("Streaming Platform")
plt.ylabel("Count")
plt.show()
```

##  Insights & Observations
1. **Most common genres** include International mMvies, Dramas and Comedies.
2. **Top producing countries**: USA, India, UK, and Japan.
3. **Average movie duration** on Netflix is around **100.46 minutes**.
4. **TV Shows & Movies have different data structures**, requiring separate handling.
5. **By comapring different movie streaming platforms**, we can see Amazon Prime Video has more no.of movies than netfix.

## Future Enhancements
- Analyze **viewer trends** over time.
- Explore **user ratings & reviews**.

## Conclusion
This project provides valuable insights into Netflix’s content trends and helps understand the platform’s entertainment landscape. 

## References
- [Netflix Dataset - Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)
- [MoviesOnStreamingPlatforms Dataset - Kaggle](https://www.kaggle.com/datasets/ruchi798/movies-on-netflix-prime-video-hulu-and-disney)
- [Pandas Documentation](https://pandas.pydata.org/)
- [Seaborn Documentation](https://seaborn.pydata.org/)
