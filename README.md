# Recipes_and_Reviews_Data_Model_Building
This project is by Aishwarya Ramesh and Sai Poornasree Balamurugan. In this project we predicted the average ratings of recipes in the Recipes and Reviews Dataset. 

## Problem Identification 
- state prediction problem and type(classification or regression) 
- report response variable and why we choose it 
- metric we choose and why we choose it over other metrics
- justify what information you would know at the time of prediction and onle train your model using those features


Given the various recipes in the Recipes and Reviews dataset, it would be nice to be able to predict the rating for a new recipe. Hence, for our prediction problem we choose to predict the average rating of a recipe given the columns in the Recipes and Reviews Dataset. 

In order to predict the average rating of a recipe, our goal was to develop a prediction model that could potentially give us an accurate average rating for a recipe using regression analysis. 

However, before we could get into creating our baseline model we wanted to add `calories`, `n_tags`, and `less_or_more_tags` columns to our datatset. We added these columns to be able to use them in our model as exploratory variables. Our response variable is the `avg_rating` because we want to predict the average rating for a recipe. At the time of prediction, the information we would know is `recipe_id`, `name`, `n_ingredients`, `avg_rating`, `n_steps`, `minutes`, `calories`, and `n_tags`. In our final dataset, to be used for predictive modeling, we dropped the NaN values in the entire dataset. This is because the NaN values don't have much predictive value for the final average rating. Thus, it makes sense to delete these values from the dataset before performing any predictive modeling. 

## Baseline Model 
In the baseline model, our exploratory dataset, X, had all of the columns except for `avg_rating` and `name`. We then created our train and test datasets using train_test_split() from sklearn.model_selection. 

The next step, was to create a preprocessor using ColumnTranformer(), where we used StandardScaler() on `n_ingredients` and `n_steps`. Then we made a linear regression model and creates a pipeline to fit our traning dataset. 



## Final Model 


## Fairness Analysis 
