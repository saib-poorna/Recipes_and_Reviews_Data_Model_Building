# Recipes_and_Reviews_Data_Model_Building
This project is by Aishwarya Ramesh and Sai Poornasree Balamurugan. In this project we predicted the average ratings of recipes in the Recipes and Reviews Dataset. 

## Problem Identification 
Given the various recipes in the Recipes and Reviews dataset, it would be nice to be able to predict the rating for a new recipe. Hence, for our prediction problem we choose to predict the average rating of a recipe given the columns in the Recipes and Reviews Dataset. 

In order to predict the average rating of a recipe, our goal was to develop a prediction model that could potentially give us an accurate average rating for a recipe using regression analysis. The metric we chose to evaluate our model was the R^2 value of the model on the test set. We used this metric because our model is linear regression, not classification and R^2 is a measure of how well the independent variables predict the response variable.

### Data Cleaning
However, before we could get into creating our baseline model we first cleaned our data. Our cleaned dataset came from our Recipes_Reviews_Data_Analysis (project 3). We additonally wanted to add `calories`, `n_tags`, and `less_or_more_tags` columns to our datatset. We added these columns to be able to use them in our model as exploratory variables. Our response variable is the `avg_rating` because we want to predict the average rating for a recipe. At the time of prediction, the information we would know is `recipe_id`, `name`, `n_ingredients`, `avg_rating`, `n_steps`, `minutes`, `calories`, and `n_tags`. We will only be using a few of these columns to train our model. 

In our final dataset, to be used for predictive modeling, we dropped the NaN values in the entire dataset. This is because the NaN values don't have much predictive value for the final average rating. Thus, it makes sense to delete these values from the dataset before performing any predictive modeling. Below, are the first couple of rows from our final dataset, unique_recipes. 

|   recipe_id | name                                  |   n_ingredients |   avg_rating |   n_steps |   minutes |   calories |   n_tags |
|------------:|:--------------------------------------|----------------:|-------------:|----------:|----------:|-----------:|---------:|
|      275022 | impossible macaroni and cheese pie    |               7 |            3 |        11 |        50 |      386.1 |       15 |
|      275024 | impossible rhubarb pie                |               8 |            3 |         6 |        55 |      377.1 |        9 |
|      275026 | impossible seafood pie                |               9 |            3 |         7 |        45 |      326.6 |       17 |
|      275030 | paula deen s caramel apple cheesecake |               9 |            5 |        11 |        45 |      577.7 |       10 |
|      275032 | midori poached pears                  |               9 |            5 |         8 |        25 |      386.9 |       24 |


## Baseline Model 
In the baseline model, our exploratory dataset, X, has columns `recipe_id`, `n_ingredients`, `n_steps`, `minutes`, `calories`, and `n_tags`. We then created our train and test datasets using train_test_split() from sklearn.model_selection. 

The next step, was to create a preprocessor using ColumnTranformer(), where we used StandardScaler() on `n_ingredients` and `n_steps` to standardize the column values. The column `n_ingredients` and `n_steps` were the quantitative features of our model. Then we made a linear regression model and created a pipeline to fit our training dataset. 

The RMSE of our training dataset was 0.640, which indicates the average magnitude of the errors between the predicted average ratings and actual average ratings. The r2 score on our training datasets were 0.0015. Given that this value is pretty low, our model is not performing too well. Next, we created preditions for our test dataset and got an RMSE value of 0.642. Our r2 score was 0.0012. 

In conlcusion, the r2 score of 0.0015 for our training data and the r2 score of 0.0012 for our test data are quite similar. Hence our model is performing approximately the same on the train and test data. As we can see from the low r^2 value, our model is not doing a good job of predicting the response variable. This means that the independent and dependent variables are not highly correlated in our model. 

## Final Model 
In order to improve the quality of our model beyond what it is now, it seems that we must go beyond linear regression and model potential nonlinear relationships between features of our data and our response variable, `avg_rating`.

For this purpose, a random forest regressor provides us with the necessary flexibility.

Our grid for potential parameters include n_estimators, max_depth, and min_samples_split to search for ideal hyperparameters. In our ColumnTranformer() we standardized `n_ingredients` and `n_steps`, quantile transfomed `minutes` and `calories`, and binarized `n_tags`. We added `minutes`, `n_tags`, and `calories`, as our features in addition to `n_ingredients` and `n_steps` because we believe that they would be predictive of the `avg_rating`. Recipes that take longer may be likely to have lower average ratings. Recipes with more tags, may be likely to be seen by more people and thus be rated a greater number of times. Finally, recipes with higher calories may be likely to taste better due to containing higher calorie ingredients like butter or sugar. Due to these potential trends, we decided to include these features in our final model. 

After creating a GridSearchCV and fitting our model, the best parameters we got were regressor__max_depth: 10, regressor__min_samples_split: 10, and regressor__n_estimators: 10. The best model we got was RandomForestRegressor with a  max_depth of 10 and a min_samples_split of 10.  

The rmse of our traning data was 0.623 and the r^2  of traning data set was 0.0555. Given the r^2 value the model is approximately performing the same on the train and test dataset. After creating the predictions for the test dataset, the rmse for the test dataset was 0.64 and the r^2 is 0.0014. 

Our final model's performance is an imporvement from our baseline's model because our training dataset rmse for baseline model of 0.6404 was greater than the training dataset rmse for our final model of 0.62. Furthermore, our training dataset r^2 for baseline model is 0.0016 which is less than the training dataset r^2 for final model of 0.055. 

Additionally, the testing dataset rmse for baseline model was 0.63976 which is slightly greater than then testing dataset rmse for the final model, 0.6394. Finally the testing dataset r^2 for baseline model was 0.000339 which is less than the testing dataset r^2 for final model, 0.00143. 

Thus these values prove that our final model is an imporvement from our baseline model. 


## Fairness Analysis 
The groups we will be considering for fairness analysis are recipes that have more tags vs less tags.

Null Hypothesis: Our model is fair. Its R^2 is the same recipes with more or less tags.

Alternative Hypothesis: Our model is unfair. Its R^2 is higher for recipes with more or less tags.

We started by defining a dataframe of recipes with less tags and recipes with more tags. A few rows of the data frame are shown below.

|   recipe_id | name                                  |   n_ingredients |   avg_rating |   n_steps |   minutes |   calories |   n_tags | less_or_more_tags   |
|------------:|:--------------------------------------|----------------:|-------------:|----------:|----------:|-----------:|---------:|:--------------------|
|      275022 | impossible macaroni and cheese pie    |               7 |            3 |        11 |        50 |      386.1 |       15 | less                |
|      275024 | impossible rhubarb pie                |               8 |            3 |         6 |        55 |      377.1 |        9 | less                |
|      275026 | impossible seafood pie                |               9 |            3 |         7 |        45 |      326.6 |       17 | more                |
|      275030 | paula deen s caramel apple cheesecake |               9 |            5 |        11 |        45 |      577.7 |       10 | less                |
|      275032 | midori poached pears                  |               9 |            5 |         8 |        25 |      386.9 |       24 | more                |

The a defined a dataframe called less_tags with only recipes with less tags and a datafram called more_tags with only recipes with more tags. These sub dataframes were created by finding the median number of tags in the entire dataset, which was 16. Then recipes with a number of tags less than 16 were categorized as less and recipes with 16 or greater number of tags were categorized as more. 

Then we created new testing data for the less_tags and more_tags dataframe respectively. The r^2 for less_tags was 0.047 and the r^2 for more_tags was 0.041. We decided to do the absolute difference between the r^2 of less_tags and the r^2 of more_tags as our observed test statistic, which was 0.0065. 

We created the permutation test by getting the less tags vs the more tags data frames. Then we set up the data to feed into our model, calculated the r^2 for the two different groups, and finally appended the absolute difference between r^2 for less and more tags to our test stats list. 

After completing the permutation test our p-value was 0.007. Since this value is less than the threshold p-value of 0.05, we reject the null hypothesis that our model performs differently between recipes with more tags and less tags





