# MovieFy Recommendation System


## Introduction

We'll be working to create a movie recommendation system on behalf of Moviefy, a new streaming video competitor. A solution to boredom and ovrwhelming choice, this new platform will be entirely based on our recommender system, eliminating the abaility to search for titles at all.

We will rely on data from [MovieLens](https://grouplens.org/datasets/movielens/latest/). We will use RMSE to determine our best fit model. Models will be created using python's surprise library and ALS spark.

## Data

* Ratings data columns: userId, movieId, rating, timestamp
* Movies data columns: movieId, title, genres

Using this data, we developed a recommendation system based on the inputs of 610 existing users across 9724 unique movies. The average user had already rated  roughly 165 movies.

Most movies were rated between 3 and 4 stars.

<img src='https://github.com/miriamsemmar/dsc-mod-4-project-v2-1-onl01-dtsc-pt-070620/blob/master/ratings_distribution.png'>


Most movies in this dataset are comedies, dramas, action movies or thrillers.

<img src='https://github.com/miriamsemmar/dsc-mod-4-project-v2-1-onl01-dtsc-pt-070620/blob/master/moviespergenre.png'>



## Modelling

We began the modelling process by leveraging [python's surprise library](https://surprise.readthedocs.io/en/stable/prediction_algorithms_package.html). Every prediction algorithm available was tested and the RMSE scores were recorded. A summary of the results below:

<img src='https://github.com/miriamsemmar/dsc-mod-4-project-v2-1-onl01-dtsc-pt-070620/blob/master/Vanilla%20Models.png'>

We then took the top 3 models (based on lowest RMSE) and used GridsearchCV to find the best parameters for each model. All models were improved by Gridsearch, however, the results all translate to predictions within +/-1 star. SVDpp remains the strongest performing model, now refined with Gridsearch. RMSE scores below for reference.

<img src='https://github.com/miriamsemmar/dsc-mod-4-project-v2-1-onl01-dtsc-pt-070620/blob/master/Gridsearch_models.png'>

Given the long processing time of the SVDpp model, we opted to develop an ALS spark model. This RMSE was 0.852285, in line with the RMSEs of our Gridsearch models. Because of it's efficent runtime, we moved forward using the ALS model to build our recommendation system.


## Recommendation System

Our recommendation system works by first determining if someone is a new or existing user by prompting the user for an ID. If this is an existing user, the system generates 5 recommendations based on their viewing and rating history.

If this is a new user, the system asks the user to rate 5 movies. Based on these reposnses, the new user received 5 movies recommendations. 


## Conclusions and Next Steps

The final ALS model is the best model for our purposes, given the low RMSE (<0.9) and quick processing time.

The recommendation system has some room for improvement. A few ideas below:

- Ask new users to rate some of the most popular movies, to avoid drawing out the initial survey. The initial survey is necessary to resolve the cold start problem.

- Create a more sophisticated model that can generate recommendations based on genres or even age group (children only, for example).

- Our dataset has a high number of comedy, fantasy and thriller movies. It's possible that our recommendations won't be as strong for movies that fall into less popular genres. We could consider a larger dataset.

- We should be updating the dataset as new movies become available on our platform.
