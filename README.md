# Business Understanding
by Jessica Guzzo

This project aims to create top 5 movie recommendations for each user of the streaming service. The reason to provide movie recommendations, is to enhance the users experience. It is important to keep the users happy while using this streaming service, because there are many streaming services to choose from. 

In addition this project aims to solve the cold start problem. The cold start problem applies to new users who the company has no historical data about. This cold start problem makes it challenging for companies to personalize movie recommendations, because there is no past history to base the recommendations off of. Its important to solve the cold start problem, so new users are impressed with the streaming service, and enjoy their experience. 

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
To start exploring the data, ratings were initially investigated. The data indicates that the mean rating was close to 4 out of 5, while there as a big standard deviation around 1. The chart below indicates a heavy skew towards users liking movies, more than disliking movies. 

![Screen Shot 2024-04-06 at 3 54 12 PM](https://github.com/jguzzo522/movierec/assets/75549456/66f23286-e4b1-444c-b565-e23f91f214fa)

## Genre
The next column investigated was genres. Before exploring the data, the genre column had to undergo dummy variable conversion. This conversion changes a categorical variable into a numerical variable. This type of conversion allows for advance modeling to analyze genres importance on recommending movies. In addition to creating dummy variables, we also split the genres so there were no combination genres. Each movie only had a single genre afer this split. This created 19 different genres which were 'Action', 'Adventure',
'Animation', 'Children', 'Comedy', 'Crime', 'Documentary', 'Drama', 'Fantasy', 'Film-Noir', 'Horror', 'IMAX', 'Musical', 'Mystery',
'Romance', 'Sci-Fi', 'Thriller', 'War', 'Western

# Modeling
SVD Grid Search Modeling was conducted to produce 5 movie recommendations per user. Grid search allows for running multiple SVD models with different parameters, such as number of factors and epochs, as well as learning rate, regularization term and bias term. This specific Grid Search was performed to produce the best Root Mean Square Score (RMSE). The grid search performed many combinations of modeling and produced the best single model to provide movie recommendations for the users. After the best model was selected, this model was performed and user recommendations were created. 

![Screen Shot 2024-04-07 at 5 42 30 PM](https://github.com/jguzzo522/movierec/assets/75549456/482e8e85-dde5-4ef2-b2e5-dcf639dbc71a)

# Conclusion

## Evaluation of SVD Grid Search
Streaming services should use SVD (Singular Value Decomposition) Grid Search modeling to produce user movie recommendations. The model produced an RMSE (Root Mean Square Error) of 0.38 and a MAE (Mean Absolute Error) of 0.24, indicating that, on average, the predicted ratings deviate from the actual user ratings by a small margin. This suggests a high level of accuracy in the recommendations provided to the users.

The F1 score is close to about 0.4226, which indicates a moderate balance between precision and recall. This model had an extreme precision of 0.98, indicating that the model will identify relevant movie recommendations 98% of the time. However, its average recall of 0.34 indicates it identifies relevant movies only 34% of the time from the entire pool of movies that a user would find relevant. This suggests that while the movies recommended by the system are highly likely to be hits when they do match a user's preferences, the system fails to capture and recommend a significant proportion of movies that users would enjoy. 

Due to the skew of positive ratings in this entire dataset, most movies would be enjoyable for a user, so there are more opportunities for the model to miss movie recommendations.

## Limitations for SVD Grid Search

There are some limitations with this model. The biggest limitation is that the initial grid search could take up to several hours to produce a result. Once the grid search establishes the best fitting model for the type of evaluation requested, the model runs at a similar pace and can easily produce fast movie recommendations.

Another limitation in using this modeling, is that we are only using ratings to produce movie recommendations, there are other factors that could be further investigated, such as genres, movie tags, and additional user variables such as age, gender or occupation.

In addition this type of modeling would be ineffective at producing movie recommendations for new users. The cold start problem applies to new users who the company has no historical data on. So the SVD Grid search would be ineffective, because the grid search specifically used users ratings to suggest movies similar to the movies the user highly rated.

## KMeans Modeling for Cold Start Problem
To recommend movies to a new user, KMeans clustering can be a useful approach. In this analysis, clustering techniques are applied to group movies based on their genre features. This approach can be useful for various purposes, such as understanding movie similarities, recommending similar movies, or targeting specfic audiences.

KMeans Clustering: The KMeans algorithm is used to cluster movies into different groups based on their genre features. Initially, 10 clusters are created. The elbow method was used to determine the optimal number of clusters. A plot was generated showing the within-cluster sum of squares for different numbers of clusters. Based on the graph the optimal amount of clusters should be around 4-6.

![Screen Shot 2024-04-13 at 10 42 25 AM](https://github.com/jguzzo522/movierec/assets/75549456/43a574e3-3461-4104-8666-959160092000)

Updated Clustering: Based on the elbow method analysis, the number of clusters is updated to 5, and the clustering process is repeated.
The clustering analysis reveals distinct groups of movies based on their genre features.

![Screen Shot 2024-04-13 at 10 43 12 AM](https://github.com/jguzzo522/movierec/assets/75549456/20195c78-cde8-4a2c-ad18-3c85f0f97cbc)

Recommendations for new users can be tailored based on the identified clusters, suggesting movies similar to those already popular within each cluster. These movie clusters allow for movies to have multiple genres, for instance cluster one is maining a mixture of action, adventure, sci-fi and thriller movies. While cluster 2 is a mixture of comedy, crime and romance movies.

There are limitations to KMeans clustering, similary to the SVD grid search, it would be useful to obtain more user data to help predict what users would be interested in viewing. To start when people sign up for the streaming service, it may be useful to gather there sign up data such as age, marriage status, and family status. Knowing this information may be important because a married family with children, may want reccommendations that are family oriented, while a single young adult may not want family oriented movies. 

## Limitations and Next Steps
The SVD Grid Search method has several limitations. One such drawback is the significant time required for data analysis. The initial grid search process can be extremely time-consuming as it explores various parameter combinations to determine the optimal parameters for the SVD model. However, once the initial grid search is completed and the optimal parameters are selected, the model's performance is comparable to that of the regular SVD model.

Another issue with the SVD Grid Search, is that the only variable investigated was user rating. Although, some anaylis on genre was conducted after the SVD Grid Search model was created, the initial SVD did not include genre as a factor. 

Certain features such as 'tags' or 'decade' were not fully analyzed. Moreover, user-specific data, including demographics like age, was not considered in the analysis. Incorporating demographic information could be crucial, as user preferences may vary based on factors such as age. For instance, younger users may prefer children's movies, whereas older users without young children may perfer dramas or action movies.

Limitations for the Kmeans clustering analysis for the cold start problem include solely analyzing genre and movie rating data. Furthermore, some movies have multiple genres, and only the most relevant genre was assigned to each movie during the analysis, which could impact clustering results. Further analysis could involve combining tags and genres to provide more in-depth insights into the types of movies within each cluster. Similarly, similar to the limitations of the SVD Grid Search method, gathering information about new users such as age, marital status, children status, and occupation could enhance the clustering analysis by providing additional context for movie recommendations. 

# Repo Structure
├── gitgnore

├── README.md

├── movie rec.pdf

└── [movierec notebook](https://github.com/jguzzo522/twaterwell/blob/main/tanwaterwell.ipynb).
