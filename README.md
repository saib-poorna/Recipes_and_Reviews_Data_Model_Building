# Recipes_and_Reviews_Data_Model_Building
This project is by Aishwarya Ramesh and Sai Poornasree Balamurugan. In this project we predicted the average ratings of recipes in the Recipes and Reviews Dataset. 

## Problem Identification 
- metric we choose and why we choose it over other metrics (need to do)

### Introduction
Given the various recipes in the Recipes and Reviews dataset, it would be nice to be able to predict the rating for a new recipe. Hence, for our prediction problem we choose to predict the average rating of a recipe given the columns in the Recipes and Reviews Dataset. 

In order to predict the average rating of a recipe, our goal was to develop a prediction model that could potentially give us an accurate average rating for a recipe using regression analysis. 

### Data Cleaning
However, before we could get into creating our baseline model we first cleaned our data. Our cleaned dataset came from our Recipes_Reviews_Data_Analysis (project 3). We additonally wanted to add `calories`, `n_tags`, and `less_or_more_tags` columns to our datatset. We added these columns to be able to use them in our model as exploratory variables. Our response variable is the `avg_rating` because we want to predict the average rating for a recipe. At the time of prediction, the information we would know is `recipe_id`, `name`, `n_ingredients`, `avg_rating`, `n_steps`, `minutes`, `calories`, and `n_tags`. We will only be using a few of these columns to train our model. 

In our final dataset, to be used for predictive modeling, we dropped the NaN values in the entire dataset. This is because the NaN values don't have much predictive value for the final average rating. Thus, it makes sense to delete these values from the dataset before performing any predictive modeling. 

## Baseline Model 
- Describe your model and state the features in your model
    - including how many are quantitative, ordinal, and nominal, and how you performed any necessary encodings
- Report the performance of your model and whether or not you believe your current model is “good” and why.

In the baseline model, our exploratory dataset, X, has columns `recipe_id`, `n_ingrdients`, `n_steps`, `minutes`, `calories`, and `n_tags`. We then created our train and test datasets using train_test_split() from sklearn.model_selection. 

The next step, was to create a preprocessor using ColumnTranformer(), where we used StandardScaler() on `n_ingredients` and `n_steps` to standardize the column values. The column `n_ingredients` and `n_steps` were the quantitative features of our model. Then we made a linear regression model and created a pipeline to fit our training dataset. 

The RMSE of our training dataset was 0.640, which indicates the average magnitude of the errors between the predicted average ratings and actual average ratings. The r2 score on our training datasets were 0.0015. Given that this value is pretty low, our model is not performing too well. Next, we created preditions for our test dataset and got an RMSE value of 0.642. Our r2 score was 0.0012. 

In conlclusion, the r2 score of 0.0015 for our training data and the r2 score of 0.0012 for our test data are quite similar. Hence our model is doing approximately the same on the train and test data. 

## Final Model 


## Fairness Analysis 
