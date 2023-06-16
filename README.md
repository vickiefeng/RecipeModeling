# Recipe Modeling
by Vickie Feng (vfeng@ucsd.edu)

My exploratory data analysis on this dataset can be found [here](https://vickiefeng.github.io/RecipeInsights/).

## Framing the Problem
The aim of this project is to **predict average ratings of recipes**. For this prediction problem, the response variable will be the recipe's average rating because it measures how positively evaluated a recipe is by users or reviewers. The chosen metric to evaluate the model is RMSE (root mean squared error). Predictions will tend to five because more than 70% of ratings are five stars, which means that outliers will heavily influence the average rating. RMSE captures these variations by measuring the average magnitude of the differences between the predicted and actual values. RMSE provides a more comprehensive assessment of the model's performance and is preferable to other metrics like MSE (mean squared error), which gives lower weight to outliers. In addition, R^2 will be used to evaluate the performance of the regression model because it provides a measure of how well the model fits the observed data.

Moreover, the features we want to use in this regression problem is information that is available prior to a given rating. This refers to variables such as number of ingredients, preparation time, and number of calories. We want to exclude features like user reviews, as they are usually given after a user has rated a recipe. 

## Baseline Model
We will be utilizing four quantitative features for this problem: `minutes`, `n_ingredients`, `calories`, and `total_fat`. My chosen model is a DecisionTreeRegressor with a maximum depth of 75 and minimum number of sample split of 5 because this regression model is capable of capturing non-linear relationships between the features and the target variable. As I mentioned earlier, average ratings are skewed high in this dataset, so the relationship between recipe attributes and average rating is non-linear. No encodings were performed on these features. As they are all numeric, StandardScaler was used to ensure that all features are on a similar scale. Features like `minutes` and `calories` have extreme outliers that would dominate the model's learning process due to the values' large magnitudes. By standardizing all the values, each feature has a proportional contribution to the overall prediction. 

The results obtained after doing a train-test-split are: a training R^2 score of 0.9078868317699864, testing R^2 score of 0.15027307268157697, training RMSE of 0.15041511025342968, and testing RMSE of 0.45980209560577223. These results indicate that the baseline model explains approximately 90.78% of the variance in the training data. This indicates a high level of fit or accuracy of the model on the training set. However, the R^2 score of the test set is significantly lower than that of the training set, signifying that the model does not generalize well to unseen data. The difference in RMSE also shows that the model's predictions have a larger average error on unseen data, as it was not nearly as accurate as it was with the training set. All in all, this suggests that the model is overfitting to the training data and not generalizing well to unseen data, which is not ideal. To improve this model's performance, we will do additional feature engineering and hyperparameter tuning. 

## Final Model
In the final model, four additional transformers were used to transform the features that were previously standardized. 

QuantileTransformer on `minutes`: Applying QuantileTransformer with n_quantiles=25 allows us to transform the 'minutes' feature to follow a normal distribution. This transformation can help the model capture more complex relationships and patterns related to the duration of recipes, as it reduces the impact of outliers and extreme values.

Binarizer on `calories`: Binarizing the 'calories' feature enables us to convert it into a binary representation based on a specific cutoff point. This transformation can be useful if we want to focus on recipes that fall into two categories: above or below a certain calorie threshold---in this case, that threshold is 700 because the average meal is 500-700 calories. This simplifies the relationship between calories and average rating, allowing the model to capture potential differences between high and low-calorie recipes.

Binarizer on `n_ingredients`: Binarizing the 'n_ingredients' feature with a threshold of 10 converts it into a binary representation based on the number of ingredients being above or below the threshold. This transformation simplifies the relationship between the number of ingredients and the average rating, enabling the model to capture potential differences between recipes with a high or low number of ingredients.

Polynomial transformation on `total_fat` and `calories`: Applying a polynomial transformation on these features allows us to capture potential non-linear relationships between 'total_fat' and 'calories' and the average rating. By introducing polynomial terms, the model can better represent complex interactions and uncover higher-order patterns in the data. In experimenting with varying degrees, a degree of 8 resulted in the best results.

To determine the best hyperparameters to use, GridSearchCV was used to conduct a 5-fold cross-validation with varying values for the DecisionTreeRegressor model's maximum depth and minimum number of sample splits. The searcher returned values of None and 5, respectively.

This model returned the following results: a training R^2 score of 0.9325672188801855, testing R^2 score of 0.25185712795581877, training RMSE of 0.10837943984116992, and testing RMSE of 0.3456270812465938. There is a slight increase in model performance, as the results on the test set show. Overall, the improved R^2 scores and reduced RMSE values in the final model suggest that the additional feature engineering, transformations, and hyperparameter tuning have resulted in a more effective model. The model is better at capturing the variability in the data and generalizing to unseen examples, as evidenced by the higher test R^2 score and the lower test RMSE compared to the baseline model.

## Fairness Analysis

