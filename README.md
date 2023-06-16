# Recipe Modeling
by Vickie Feng (vfeng@ucsd.edu)

My exploratory data analysis on this dataset can be found [here](https://vickiefeng.github.io/RecipeInsights/).

## Framing the Problem
The aim of this project is to **predict average ratings of recipes**. For this prediction problem, the response variable will be the recipe's average rating because it measures how positively evaluated a recipe is by users or reviewers. The chosen metric to evaluate the model is RMSE (root mean squared error). Predictions will tend to five because more than 70% of ratings are five stars, which means that outliers will heavily influence the average rating. RMSE captures these variations by measuring the average magnitude of the differences between the predicted and actual values. RMSE provides a more comprehensive assessment of the model's performance and is preferable to other metrics like MSE (mean squared error), which gives lower weight to outliers. 

Moreover, the features we want to use in this regression problem is information that is available prior to a given rating. This refers to variables such as number of ingredients, preparation time, and number of calories. We want to exclude features like user reviews, as they are usually given after a user has rated a recipe. 

