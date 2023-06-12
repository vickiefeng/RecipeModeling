# Recipe Modeling
by Vickie Feng

## Framing the Problem
The aim of this project is to **predict average ratings of recipes**. For this prediction problem, the response variable will be the recipe's average rating because it measures how positively evaluated a recipe is by users or reviewers. The chosen metric to evaluate the model is RMSE (root mean squared error). Predictions will tend to five because more than 70% of ratings are five stars, which means that outliers will heavily influence the average rating. RMSE captures these variations by measuring the average magnitude of the differences between the predicted and actual values. Other metrics like F1-score and accuracy are more suitable for classification problems involving discrete values, which we will not be dealing with since average rating is a continuous variable. 

Moreover, the features we want to use in this regression problem is information that is available prior to a given rating. This refers to variables such as number of ingredients, number of steps, preparation time, and number of calories. We want to exclude features like user reviews, as they are usually given after a user has rated a recipe. 

