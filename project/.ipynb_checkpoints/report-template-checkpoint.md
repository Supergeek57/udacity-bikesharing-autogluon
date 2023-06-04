# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Holland Henderson-Boyer

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
I realized that predictions would be rejected if some of the prediction values were less than zero, so I had to set all negative prediction values to zero.

### What was the top ranked model that performed?
According to the results from AutoGluon's fit_summary() function, the top ranked model was WeightedEnsemble_L3 for all three training runs. The top-performing training run incorporated both new features and hyperparameter optimization.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
The EDA showed that there wasn't a clear distribution of values in the datetime histogram; the distributions became much clearer when the datetime column was separated into three columns for year, month, and day. I added additional features by using Pandas' dt feature (dt.year, dt.month, and dt.day) to create three new columns from the year, month, and day pieces of the datetime column values.

### How much better did your model preform after adding additional features and why do you think that is?
My model performed significantly better after adding additional features (Kaggle score decreased from about 1.79 to 1.34). The specific features I added were month, day, and year (which replaced the initial datetime column of the dataset). I think that this addition caused the model to perform better because the model was able to optimize for the potentially different impacts of month, day, and year separately. For example, month could impact bike sharing demand because people may be less likely to bikeshare in winter weather, while day could impact bike sharing demand because people may be more likely to bikeshare during the work week. Separating these data points into different columns made it easier for the model to differentiate their impact.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
The model performed slightly better after trying different hyperparameters (Kaggle score decreased from 1.33793 to 1.32375). The hyerparameters I changed included setting the number of trials and the searcher in hyperparameter tune kwargs and setting hyperparameters to light. The fine-grained hyperparameter optimization, including using a random searcher (which might be better for this particular use case), slightly improved the performance of the model even with the same training time.
(Source: https://auto.gluon.ai/stable/api/autogluon.tabular.TabularPredictor.fit.html) 

### If you were given more time with this dataset, where do you think you would spend more time?
I would perform additional EDA to see if there were more features I could add to increase model accuracy. I would also make sure all features were optimally categorized as either numerical or categorical data.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
![model_train_score.png](img/udacity_table_2.png)

### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: Replace the image below with your own.

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO: Replace the image below with your own.

![model_test_score.png](img/model_test_score.png)

## Summary
Separating the datetime column of the dataset into month, day, and year columns and optimizing the time_limit, num_stack_levels, and num_bag_folds parameters improved the performance of an Autogluon model on the bike sharing demand dataset.
