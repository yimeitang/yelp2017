# Yelp2017
There are 156,639 business units in the business data. I focus on the restaurants in Las Vegas which has 5682 records.

In this project, I have these three questions: 
1. Could we classify ratings just by looking at the restaurants’ features?
2. Do Yelp users share some common characteristics when their given average ratings are close?
3. Could we use the ratings alone to perform collaborative filtering and matrix factorization to predict ratings?

## Step 1: Get the data
I am using three datasets(Business,Review and User) from the Yelp Data. 
You could download them here: https://www.yelp.com/dataset/challenge

## For Question 1: Classify Ratings by Restaurants' Features.
## Step 2: Preprocess the data

Each restaurant example has 15 features and among them, only the "attributes" and "review_count" features are related the the ratings.
After analyzing the "attributes" feature, I got 37 different amenities features and some of them are highly indicative of restaurant ratings. 

![corkage](https://user-images.githubusercontent.com/27776652/33225535-fc33e2c6-d13e-11e7-9893-950bd8ed481b.PNG)
![credit](https://user-images.githubusercontent.com/27776652/33225536-fc41a1c2-d13e-11e7-8ba7-615665ecced1.PNG)
![smoking](https://user-images.githubusercontent.com/27776652/33225537-fc501b08-d13e-11e7-87d1-f262c8e14474.PNG)
![tableservice](https://user-images.githubusercontent.com/27776652/33225538-fc5dc12c-d13e-11e7-831b-b7d726ec9cea.PNG)
![wifi](https://user-images.githubusercontent.com/27776652/33225539-fc6c845a-d13e-11e7-9231-c722a70b28a8.PNG)
![ambience](https://user-images.githubusercontent.com/27776652/33225540-fc7c7d9c-d13e-11e7-9ccf-16db60cd8ab3.PNG)
![attire](https://user-images.githubusercontent.com/27776652/33225541-fc8b7612-d13e-11e7-81d3-80eccdef98b0.PNG)
![bestnights](https://user-images.githubusercontent.com/27776652/33225542-fc99fd2c-d13e-11e7-911b-5f48d7d2b82e.PNG)
![byob](https://user-images.githubusercontent.com/27776652/33225544-fca9416a-d13e-11e7-9cff-c529b38063b7.PNG)


## Step 3: Build the model
I convert all dependent variables to dummy varialbes since they are categorical data, then build four models in K Nearest Neighbours,Decision Tree, Linear Discriminant Analysis and Random Forest.

## Step 4: Evaluate the model
![model_comparison](https://user-images.githubusercontent.com/27776652/33225558-4a022c60-d13f-11e7-98cb-dc6fab25619c.jpg)
The best model is Decision Tree model(entropy as criterion, the max depth is 7, the min samples split is 12, and the
min samples leaf is 1) with 13 features(dummy variables).

![dt_features](https://user-images.githubusercontent.com/27776652/33225567-7e0239ba-d13f-11e7-80e1-bc5331e60c41.PNG)

## Step 5: Conclusion
The most important feature is DRIVEThru(TRUE). Usually only fast food and coffee shops have drive through service,
therefore, it explains why this feature is important. It is a determining factor whether this is a fast food restaurant or
other types of restaurant.

Filtering out the features that are unknown, we see that Restaurants Table Service, Good For Meal(dinner) , Caters and
Business Parking lot are important features.

Given the low accuracy score of four classification models, we can’t just rely on the restaurant features alone to classify the ratings. However, these features will be helpful in future analysis.


## For Question 2: K-Means Clustering and Principal Component Analysis
## Step 2: Preprocess the data
We will only use numerical data in this analysis since KMeans clustering is for numeric data.

## Step 3: Build the model
The first time, I just use normalized data with cluster = 3.

## Step 4: Evalute the model
![first_kmeans](https://user-images.githubusercontent.com/27776652/33225656-66d24706-d141-11e7-96ce-ad84f2b54177.jpg)

## Step 5: Build the model
The second time, I use PCA and the 98% of the total variance of original 17 features could be represented by 1 principal component.

## Step 6: Evalute the model
![second_kmeans](https://user-images.githubusercontent.com/27776652/33225665-91f6b9b2-d141-11e7-862f-a0ef7a2c242b.jpg)

## Step 7: Conclusion
As we could tell from the first model, the cluster 0 seems to be of users who is relatively ”conservative” in giving high ratings. Users
from cluster 1 are the most ”generous” type of users, they give the highest ratings among these three groups. On the contrary,
users from cluster 2 are very ”picky” that they give the lowest ratings of all.

However, it is the users from cluster 0 receives the highest compliments across all categories in these three clusters. Users
from cluster 1 receives the second highest compliments among these three clusters. What is surprising is that , event though
users from cluster 2 are critical, their reviews are far less helpful or cool than other users.

If your average rating is in the middle level yelp users(in another way, you are not too critical or too
easy to satisfied), you will receive more compliments from others. People are more likely to think your reviews are helpful
or cool. However, if your average ratings are extremely low, then people are less likely to compliment your reviews.


## For Question 3: Perform Collaborative Filtering and Matrix Factorization to Predict Ratings
## Step 2: Preprocess the data
In this analysis, I only use a sample size of 8,000 ratings from the original 850,000 ratings to perform collaborative filtering with matrix factorization.

## Step 3: Build and Evalute the Model
Although I only train the model with 100 steps, the outcome is very good with an overal MAE of 1.69 for 7,389 users and 5,682 restaurants in total.

![cf_results](https://user-images.githubusercontent.com/27776652/33225687-49ab12ce-d142-11e7-92f9-32e3f6b6bf05.jpg)

## Step 4: Conclusion
Although I only use a sample size of 8,000 out of 850,000 records, the performance of the collaborative filtering model is very good with only 1.69 in MAE for 7,389 users and 5,682 restaurants.
