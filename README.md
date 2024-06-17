# Movie Data Analysis 


### Welcome to the **Movie Data Analysis project**. This repository provides insights into a dataset of movies, analyzing various aspects like runtime, ratings, votes, revenue, and more.
###

You can interact with the report [HERE](https://github.com/Nkemjika-123/Movie-Analysis/blob/main/Movie%20DataSet-Copy3.ipynb)


## Table of Contents
[Introduction](#introduction)

[Objectives](#objectives)

[Data Source](#data-source)

[Task](#task)

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

![1 (1)](https://github.com/Nkemjika-123/Movie-Analysis/assets/152037119/c331b851-c2b5-441e-90e6-8d739c2fdb2f)


**which year had the highest average revenue** 
data.groupby('Year')['Revenue (Millions)'].mean().sort_values(ascending = False)

avg_revenue_per_yr = data.groupby('Year')['Revenue (Millions)'].mean()
plt.figure(figsize = (10,6))  
plt.barh(avg_revenue_per_yr.index, avg_revenue_per_yr.values, color = 'darkblue')
plt.xlabel('Average Revenue (Millions)')
plt.ylabel('Year')
plt.title('Average Revenue (Millions) by Year')
plt.grid(False)
plt.show()

![2](https://github.com/Nkemjika-123/Movie-Analysis/assets/152037119/eaeb788d-bf2f-488a-8537-2f054c1081c2)

**average rating for top 10 directors**
mean_rating_per_director = data.groupby('Director')['Rating'].mean()
top_10_directors = mean_rating_per_director.sort_values(ascending=False).head(10)
print(top_10_directors)

plt.figure(figsize = (10,6))  
top_10_directors.plot(kind = 'bar')
plt.xlabel('Director')
plt.ylabel('Average Rating')
plt.title('Top 10 Directors by Average Rating')
plt.xticks(rotation=45, ha = 'right')
plt.grid(False)
plt.show()

![3](https://github.com/Nkemjika-123/Movie-Analysis/assets/152037119/c715f178-51ac-4e97-aad1-be3cc7fa0c91)

**top 10 lengthy movies and runtime**
Top10_len=data.nlargest(10,'Runtime (Minutes)' )[['Title', 'Runtime (Minutes)']].set_index('Title')
Top10_len

sns.barplot(x='Runtime (Minutes)', y=Top10_len.index, data=Top10_len)
plt.title('Top 10 Movies by Runtime(Minutes)')
plt.show()

![4](https://github.com/Nkemjika-123/Movie-Analysis/assets/152037119/922efd37-f415-4c37-bb76-4b43edaa283e)

**how many movies were watched in each year**
data['Year'].value_counts()

sns.countplot(x='Year', data=data, color = 'darkblue')
plt.ylabel('Number of Movies Released')
plt.title('Number of Movies Per Year')
plt.show()

![5](https://github.com/Nkemjika-123/Movie-Analysis/assets/152037119/0554b981-8be9-4c76-bae3-b5079db1627b)

**top 10 highest rated movie titles and its directors**
Top10_len=data.nlargest(10,'Rating' )[['Title', 'Rating', 'Director']].set_index('Title')
Top10_len

sns.barplot(x='Rating', y=Top10_len.index, data=Top10_len, hue='Director', dodge=False)
plt.legend(bbox_to_anchor=(1.05,1), loc=2)
plt.xlabel('Title')
plt.ylabel('Rating')
plt.title('Top Movies by Rating')
plt.xticks(rotation = 45)
plt.grid(False)
plt.show()

![6](https://github.com/Nkemjika-123/Movie-Analysis/assets/152037119/fdcd4377-a548-4698-904a-23fab8b9a97b)

**top 10 highest revenue movie titles**
Top_10=data.nlargest(10, 'Revenue (Millions)')[['Title','Revenue (Millions)']].set_index('Title')
Top_10

sns.lineplot(x='Revenue (Millions)',y=Top_10.index, data=Top_10, marker ='o', color = 'darkblue')
plt.grid(False)
plt.title('Top 10 Highest Revenue Movie Titles')
plt.show()

![7](https://github.com/Nkemjika-123/Movie-Analysis/assets/152037119/49eb2966-fb53-4fc5-8ce6-4fdfdc7a720d)

**Average rating of movies Year wise**
average_rating_by_year=data.groupby('Year')['Rating'].mean().sort_values(ascending = False)
average_rating_by_year

plt.bar(average_rating_by_year.index, average_rating_by_year.values, color='darkblue')
plt.xlabel('Year')
plt.ylabel('Average Rating')
plt.title('Average Rating of Movies Year-wise')
plt.xticks(rotation=45)
plt.show()

![8](https://github.com/Nkemjika-123/Movie-Analysis/assets/152037119/a4bc10d6-dae6-4884-8dd1-89372f0d837b)

**Does rating affect revenue**
sns.scatterplot(x='Rating',y='Revenue (Millions)', data=data)
plt.show()

![9](https://github.com/Nkemjika-123/Movie-Analysis/assets/152037119/7480bb21-6ddc-431a-a539-ee99dbc3c4b5)

You can interact with the report [HERE](https://github.com/Nkemjika-123/Movie-Analysis/blob/main/Movie%20DataSet-Copy3.ipynb)

## Analysis and Findings/Insights

+ 2012 had the highest movie engagement.	
+	The movie industry was most successful in the year 2009 because that was when they had the highest revenue.
+	Nitesh is the highest rated director, followed by Christopher.
+	Grindhouse movie stands out for its extended duration.
+	2006 had the lowest number of movies watched, it kept progressing until 2016, here the highest number of movies were watched.
+	The Force Awakens was the movie the generated the highest revenue, this was followed by Avatar.
+	Movies were rated the highest in 2006 and 2007.
+	As rating was increasing, revenue was also increasing.

## Recommendations

+ Conduct marketing campaigns and promotions during peak engagement periods to maximize audience reach.

+ Invest in and promote movies that were rated highest like directors Nitesh and Christopher. Their reputation for quality can attract larger. You can establish partnership with them for future projects. 

+ Lengthy movies such as grind house can be marketed to people that like extended storytelling and epic narratives. 

+ What are the factors that contributed to the success of movies like "The Force Awakens" and "Avatar", apply such factors to other movies.

+ Since there is a correlation between higher ratings and increased revenue, focus should be on improving movie ratings through quality content, talent, and production.

###
You can interact with the report [HERE](https://github.com/Nkemjika-123/Movie-Analysis/blob/main/Movie%20DataSet-Copy3.ipynb)




## Conclusion

These recommendations aim to leverage historical insights to improve future movie performance, audience engagement, and financial success. By understanding past trends and implementing targeted strategies, stakeholders can optimize their approach to movie production, marketing, and release scheduling. Audience feedback and critical reviews should be considered to improve movie quality and rating.
