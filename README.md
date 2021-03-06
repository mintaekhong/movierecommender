# Capstone Project - Movie Recommender System

## Problem Statement
It is as true today as ever: we have too many choices to make. As a consumer, one of the tools that helps us navigate through these choices is a recommender system. As we may be familiar with, recommender systems in some shape or form are now ubiquitous on many online platforms ranging from Netflix, Amazon, Google, and more.

As a business, with more of its consumers' interactions and purchases taking place in the online space, it is important to deliver a complete and tailored shopping experience to retain its customer base. Through a recommender system, businesses are able to retain customers by increasing the time spent on their respective websites. 

But how does it work behind the scenes?  I seek to explore the inner workings of recommender systems by answering the following question: Given a movie title that a user enjoyed, how can we best provide movie recommendations?

## Content
Notebooks are organized in the following order:
1. [01_Data_Gathering.ipynb](http://localhost:8888/lab/tree/dsi%2Fprojects%2Fcapstone%2FMike_Hong_LA_6%2Fnotebooks%2F01_Data_Gathering.ipynb) <br>
2. [02_Preprocessing.ipynb](http://localhost:8888/lab/tree/dsi%2Fprojects%2Fcapstone%2FMike_Hong_LA_6%2Fnotebooks%2F02_Preprocessing.ipynb) <br>
3. [03_Recommender_Engineering.ipynb](http://localhost:8888/lab/tree/dsi%2Fprojects%2Fcapstone%2FMike_Hong_LA_6%2Fnotebooks%2F03_Recommender_Engineering.ipynb) <br>

## Data Gathering
**Content-Based Recommender** <br>
For my content based movie recommender, I retrieved data from the Movie Database (TMDb) and called its API to gather the following: popularity, votes, and overview. The overview consists of approximately 3 to 5 sentences providing a brief description of the plot and main characters involved. 

**Collaborative-Based Recommender** <br>
The 20M MovieLens dataset can be found on the [GroupLens](https://grouplens.org/datasets/movielens/20m/) website. The four comma separated value files that were available are the following:

- **ratings.csv**: includes 20,000,263 ratings across 27,278 movies
- **movies.csv**: includes the title of the movie and its associated genres
- **links.csv**: includes different id's that can link with external database (i.e. imdb and tmdb)
- **tags.csv**: includes tags generated by users 

All four csv files were added to a PostgreSQL database hosted on a t2.micro AWS EC2 instance. I primarily utilized the first three csv files, namely, ratings.csv, movies.csv, and links.csv in conjunction to create my content-based recommender and collaborative-based recommender. 

## Preprocessing
**Content-Based Recommender** <br>
In order to utilize overview as vector representations for a movie, we used standard nlp practices such as tokenizing, lemmatizing, countvectorizing and tfidf to clean and turn words into machine learning-ready data. 

**Collaborative-Based Recommender** <br>
To effectively leverage user reviews as vector representations for a movie, we removed item bias by subtracting a given rating by the average rating of the movie and dividing by the standard deviation of the ratings for that movie. 


## Recommender Engineering
**Content-Based Recommender** <br>
The content-based recommender provided some questionable results. For example, when a user inserts 'Toy Story (1995)' as the input, movies such as the '40-Year-Old Virgin' and 'Child's Place 2' make it into the top 10 recommended movies. They are included because of entity nouns such as 'Andy' that are included in the movie overview, the main source of features for the movie. 

**Collaborative-Based Recommender** <br>
The collaborative-based recommender provided better recommendations. For example, when a user inputs Toy Story 2, the first few movies recommended are the following: Toy Story, A Bug's life, Monster's Inc., and Finding Nemo, which are all animated and family/adventure related movies. We are able to avoid the pitfalls of the content-based recommender because we utilize user ratings instead to vectorize the movies. 

## Conclusion and Going Forward
We explored two methods of providing movie recommendations: content-based and collaborative. With the outputs from the two said movie recommenders, I am more confident in providing movie recommendations via the collaborative method where we leverage item similarities through user reviews. With that said, the content-based recommender can be further improved by removing entity names to avoid an example such as the 'Batman and Robin (1997)' where more than half the recommended movies were Batman-related. <br>

Furthermore, we can explore the idea of engineering a hybrid recommender system where we bring together both the content and collaborative filtering recommenders into one. Some of the ways that they come together are the following: by linearly combining them or by a voting mechanism. We could also explore switching techniques that allows to switch from a recommender system to the other when a certain criteria is met. 

