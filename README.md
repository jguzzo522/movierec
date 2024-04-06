# Business Understanding
by Jessica Guzzo

This project aims to create top 5 movie recommendations for each user of the streaming service. The reason to provide movie recommendations, is to enhace the users experience. It is important to keep the users happy while using this streaming service, because there are many streaming services to choose from. 

In addtion this project aims to solve the cold start problem. The cold start problem applies to new users who the company has no historical data about. This cold start problem makes it challenging for companies to personalize movie reccomendations, because there is no past history to base the reccomendations off of. Its important to solve the cold start problem, so new users are impressed with the streaming service, and enjoy their experience. 
![glenn-carstens-peters-EOQhsfFBhRk-unsplash](https://github.com/jguzzo522/movierec/assets/75549456/e8a7fc92-b038-4486-a172-91bf87695783)

# Data Understanding

This dataset come from https://grouplens.org/datasets/movielens/latest/ . In this dataset the following columns are present: 
![Screen Shot 2024-04-06 at 3 36 13 PM](https://github.com/jguzzo522/movierec/assets/75549456/418f1490-5720-43b7-b5e5-6accedf85e66)

## Data Preparation

Packages such as Pandas, Numpy, Matplotlib, Surprise, Scikit-learn, and Scipy were used to create models and evaluate performance for both movie recommendations and the cold start problem.

Once the packages were loaded, the four datasets were imported, and an empty dictionary was created to store all four DataFrames. Exploration of the datasets began by reviewing the number of rows and columns, as well as printing out the first 5 data points from each dataset.

The four datasets were merged o 'movieId', so the data could be fully explored. There were a total number of 9,742 movies, from a total number of 233,213 users.  Ratings of movies ranged from 0.5 to 5. In the  genres column there were many types of genres, and most movies had overlapping genres. 

The year column was condensed into a decade column. This made the visualization of movie trends easier to interpret. 

Missing values were removed from the data set including around 52k missing userid_y, tag, and timestamp_y values. Prior to these rows being removed the dataset had 285,762 values, after removal of the missing data there were 233,213 rows.


# Exploratory Data Analysis

## Rating
To start exploring the data, ratings were initially investigated. The data indicates that the mean rating was close to 4 out of 5, while there as a big standard deviation around 1. The chart below indicates a heavy skew towards users liking movies, more than dislking movies. 
![Screen Shot 2024-04-06 at 3 54 12 PM](https://github.com/jguzzo522/movierec/assets/75549456/66f23286-e4b1-444c-b565-e23f91f214fa)

## Genre
The next column invesigated was genres. Before exploring the data, the genre column had to undergo dummy variable conversion. This conversion changes a categorical variable into a numerical variable. This type of conversion allows for advance modeling to analyze genres importance on reccommending movies. In addition to creating dummy variables, we also split the genres so there were no combination genres. Each movie only had a single genre afer this split. This created 19 diffrent genres which were 'Action', 'Adventure',
'Animation', 'Children', 'Comedy', 'Crime', 'Documentary', 'Drama', 'Fantasy', 'Film-Noir', 'Horror', 'IMAX', 'Musical', 'Mystery',
'Romance', 'Sci-Fi', 'Thriller', 'War', 'Western

# Modeling
SVD Grid Search Modeling was conducted to produce 5 movie reccomendations per user.
# Conclusion

## Limitations

## Reccommendations

## Next Steps
=======
# movierec
>>>>>>> 055b0e4f65ae17df9c56f428191ab5505ef2d873
