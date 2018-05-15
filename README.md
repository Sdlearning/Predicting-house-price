# Predicting-house-price
To preduict housing price using Linear regression model
We'll work with housing data for the city of Ames, Iowa, United States from 2006 to 2010. You can read more about why the data was collected here. You can also read about the different columns in the data here.
Let's start by setting up a pipeline of functions that will let us quickly iterate on different models.
Train ->Transform_features()->select_features()->train_and_test()->rmse values -> avg rmse
Import pandas, matplotlib, and numpy into the environment. Import the classes you need from scikit-learn as well.
Read AmesHousing.tsv into a pandas data frame.
Create a function named transform_features() that, for now, just returns the train data frame.
Create a function named select_features() that, for now, just returns the Gr Liv Area and SalePrice columns from the train data frame.
Create a function named train_and_test() that, for now:
Select the first 1460 rows from from data and assign to train.
Select the remaining rows from data and assign to test.
Trains a model using all numerical columns except the SalePrice column (the target column) from the data frame returned from select_features()
Test the model on the test set and returns the RMSE value.

Transform_features()
Let's now start to removing features with many missing values, diving deeper into potential categorical features, and transforming text and numerical columns. Update transform_features() so that any column from the data frame with more than 25% (or another cutoff value) missing values is dropped. We also need to remove any columns that leak information about the sale (e.g. like the year the sale happened). In general, the goal of this function is to:
remove features that we don't want to use in the model, just based on the number of missing values or data leakage
transform features into the proper format (numerical to categorical, scaling numerical, filling in missing values, etc)
create new features by combining other features
Next, we need to get more familiar with the remaining columns by reading the data documentation for each column, determining what transformations are necessary (if any), and more. Libraries like scikit-learn has made it quick and easy to simply try and tweak many different models, but cleaning, selecting, and transforming features is still more of an art that requires a bit of human ingenuity.

Select_features()
Now that we have cleaned and transformed a lot of the features in the data set, it's time to move on to feature selection for numerical features.
Generate a correlation heatmap matrix of the numerical features in the training data set. 
Which features correlate strongly with our target column, SalePrice?
Calculate the correlation coefficients for the columns that seem to correlate well with SalePrice. Because we have a pipeline in place, it's easy to try different features and see which features result in a better cross validation score.
Which columns in the data frame should be converted to the categorical data type? All of the columns marked as nominal from the documentation are candidates for being converted to categorical. Here are some other things you should think about:
If a categorical column has hundreds of unique values (or categories), should we keep it? When you dummy code this column, hundreds of columns will need to be added back to the data frame.
Which categorical columns have a few unique values but more than 95% of the values in the column belong to a specific category? This would be similar to a low variance numerical feature (no variability in the data for the model to capture).
Which columns are currently numerical but need to be encoded as categorical instead (because the numbers don't have any semantic meaning)?
What are some ways we can explore which categorical columns "correlate" well with SalePrice?
Read this post for some potential strategies.
Update the logic for the select_features() function. This function should take in the new, modified train and test data frames that were returned from transform_features().

Train_test()
Now for the final part of the pipeline, training and testing. When iterating on different features, using simple validation is a good idea. Let's add a parameter named k that controls the type of cross validation that occurs.

The optional k parameter should accept integer values, with a default value of 0.
When k equals 0, perform holdout validation (what we already implemented):
Select the first 1460 rows and assign to train.
Select the remaining rows and assign to test.
Train on train and test on test.
Compute the RMSE and return.
When k equals 1, perform simple cross validation:
Shuffle the ordering of the rows in the data frame.
Select the first 1460 rows and assign to fold_one.
Select the remaining rows and assign to fold_two.
Train on fold_one and test on fold_two.
Train on fold_two and test on fold_one.
Compute the average RMSE and return.
When k is greater than 1, implement k-fold cross validation using k folds:
Perform k-fold cross validation using k folds.
Calculate the average RMSE value and return this value.




