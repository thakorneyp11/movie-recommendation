# movie-recommendation
Movie recommendation based on rating scores

## Project Overview
This project consists of 2 parts
1. SVD recommendation modeling
2. Interactive movie recommendation pipeline: user can rate more movies and the pipeline will recommend more movies based on the model prediction values and user's rating scores on each specific movie

## Dataset Overview
source: https://www.kaggle.com/CooperUnion/anime-recommendations-database

### Context
This data set contains information on user preference data from 73,516 users on 12,294 anime. Each user is able to add anime to their completed list and give it a rating and this data set is a compilation of those ratings.

### Content
**Anime.csv**
- `anime_id` - myanimelist.net's unique id identifying an anime.
- `name` - full name of anime.
- `genre` - comma separated list of genres for this anime.
- `type` - movie, TV, OVA, etc.
- `episodes` - how many episodes in this show. (1 if movie).
- `rating` - average rating out of 10 for this anime.
- `members` - number of community members that are in this anime's "group".

**Rating.csv**
- `user_id` - non identifiable randomly generated user id.
- `anime_id` - the anime that this user has rated.
- `rating` - rating out of 10 this user has assigned (-1 if the user watched it but didn't assign a rating).

## How to Run
1. Prepare environment using virtualenv or docker, then install all dependencies listed in `requirements.txt`
2. Download dataset from [kaggle dataset](https://www.kaggle.com/CooperUnion/anime-recommendations-database) to `dataset/anime.csv` and `dataset/rating.csv`
3. SVD model training: run the `model_training.py` script
4. Test model prediction: run the `model_prediction.py` script
5. Run the interactive movie recommendation pipeline: run the `movie_recommendation.py` script

## Interactive Movie Recommendation's System Diagram
![Movie Recommendation Pipeline](https://user-images.githubusercontent.com/58812639/160230960-690bb8cf-c7d9-44d8-8d95-b7a8bcd69f59.jpeg)

## Interactive Movie Recommendation's Output Example
The pipeline will ask the user to select the `user_id` to play as this person, then it will perform SVD model prediction to predict the estimated rating score on all unseen movies and suggest a initial movie set to the user
![image_1](https://user-images.githubusercontent.com/58812639/160231130-ebebec88-ee97-44ba-807b-9ca9d0d017b1.png)
The pipeline will ask whether the user want to continue watching the movie and rate the selected movie. In this case, I choose movie_id `28977` which include `Comedy` genre and rate it with 9. The pipeline will adjust the genre-weights for each genre-type included in movie_id `28977` and suggest to the user again.
![image_2](https://user-images.githubusercontent.com/58812639/160231133-bb4efacc-bd67-4027-972f-2b89d0c5af9c.png)
I continue choosing movie_id `9863` which include `Comedy` genre and rate it with 8. The pipeline will adjust the genre-weights for each genre-type included in movie_id `9863` and suggest to the user again.
![image_3](https://user-images.githubusercontent.com/58812639/160231134-7da7215d-7650-4ea9-a0ec-317a14bdf567.png)
I continue choosing movie_id `5114` which include `Action` genre and rate it with 3. The pipeline will adjust the genre-weights for each genre-type included in movie_id `5114` and suggest to the user again.
![image_4](https://user-images.githubusercontent.com/58812639/160231135-9aa1371b-5c4d-4e2a-944e-201a49890eb2.png)
After selecting and rating movies continuously with the goal of giving `Comedy` genre movies good rating scores and `Action` genre movies bad rating scores, the pipeline have continuously adjust the genre-weights and suggest a movie set that mostly include `Comedy` genre and neglecting `Action` genre to the user.
![image_5](https://user-images.githubusercontent.com/58812639/160231137-ac21a940-3b0c-4d46-8e7a-138cfe9e8fed.png)
