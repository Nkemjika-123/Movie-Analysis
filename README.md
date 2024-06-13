# Movie Data Analysis 


### Welcome to the **Movie Data Analysis project**. This repository provides insights into a dataset of movies, analyzing various aspects like runtime, ratings, votes, revenue, and more.
###

You can interact with the report [HERE](https://github.com/Nkemjika-123/Movie-Analysis/blob/main/Movie%20DataSet-Copy3.ipynb)


## Table of Contents
[Introduction](#introduction)

[Objectives](#objectives)

[Data Source](#data-source)

[Task](#task)

[Data Preparation and Transformation](#data-preparation-and-transformation)

[Data Exploration and Visualization](#data-exploration-and-visualization)

[Analysis and Findings/Insights](#analysis-and-findingsinsights)

[Recommendations](#recommendations)

[Conclusion](#conclusion)

## Introduction
The dataset contains information about movies from IMDB with the following columns:

+ **Rank**: The ranking of the movie.
+ **Title**: The title of the movie.
+ **Genre**: The genre of the movie.
+ **Description**: A brief description of the movie.
+ **Director**: The director of the movie.
+ **Actors**: The main actors in the movie.
+ **Year**: The release year of the movie.
+ **Runtime (Minutes)**: The duration of the movie in minutes.
+ **Rating**: The IMDB rating of the movie.
+ **Votes**: The number of votes received by the movie.
+ **Revenue (Millions)**: The revenue generated by the movie in millions.
+ **Metascore**: The metascore of the movie.

## Objectives
This project aims to analyze a dataset containing information about movies from IMDB. The dataset includes details such as the ranking, title, genre, description, director, actors, release year, runtime, rating, number of votes, revenue, and metascore of various movies. It aims to gain insights into the characteristics and performance of these movies to identify patterns and derive actionable insights. 

### Key Objectives
 1. **Identify High-Performing Movies:** Determine which movies have the highest ratings and revenues. 
2. **Analyze Trends Over Time:** Evaluate how movie ratings and revenues have evolved over the years.
 3. **Understand Genre Popularity:** Assess the popularity and performance of different movie genres.
 4. **Evaluate Director and Actor Influence:** Analyze the impact of directors and main actors on movie success. 
5. **Explore Runtime Effects:** Investigate how the runtime of a movie affects its ratings and revenue.
 6. **Correlate Ratings and Revenue:** Explore the relationship between movie ratings and revenue.

## Data Source
The data used for this project was from [HERE](https://www.kaggle.com/datasets/PromptCloudHQ/imdb-data)

### Analysis Questions: 
1. Titles of movies with a runtime of 180 minutes or more.
2. Average number of votes per year, sorted in descending order.
3. The year with the highest average revenue.
4. Average rating for the top 10 directors.
5. Top 10 longest movies and their runtimes.
6. Number of movies released each year.
7. Most popular movie title.
8. Top 10 highest-rated movie titles and their directors.
9. Top 10 movies that generated the highest revenue.
10. Average rating of movies each year.
11. The effect of ratings on revenue. 

## Data Preparation and Transformation
This was done using jupyter notebook Python

. Importing Libraries:
   
+	Libraries such as **pandas** for data manipulation,  **matplotlib** and **seaborn** for visualization are imported.

2. Loading the Data:

+	The IMDB dataset is loaded using **pandas.read_csv** function.

3. Data Cleaning:
   
+	check for missing values with **data.isnull().sum()**

+	Duplicate entries are removed to prevent skewed analysis using 
**dup_data = data.duplicated().any().**

## Data Exploration and Visualization
This section is vital for understanding the underlying patterns and trends in the dataset. These were the codes used:
**Title of movie having runtime >=180mins**
data[data['Runtime (Minutes)']>= 180]['Title']

**show variation btw year had the highest voting**
data.groupby('Year')['Votes'].mean().sort_values(ascending = False)


**show variation btw year had the highest average voting**
avg_votes_per_yr = data.groupby('Year')['Votes'].mean()
plt.figure(figsize = (10,6))  
plt.bar(avg_votes_per_yr.index, avg_votes_per_yr.values, color = 'red')
plt.xlabel('Year')
plt.ylabel('Average Votes')
plt.title('Average Votes by Year')
plt.grid(False) 
plt.show()


