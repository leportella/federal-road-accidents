# Prediction of accident victims on federal roads in Brazil

Project submmited to Udacity as final project on Nanodegree in Machine Learning Engineer.


## Project

The document of the main idea behind this project can be seen [here](https://github.com/leportella/federal-road-accidents/blob/master/PROJECT.md).
Details of implementation, techniques and other issues found during this project are 
available on the present document. 


## Cleaning up

From two initial datasets, a unique dataset was conceived with some cleaning ups. For 
instance, the dates on dataset from 2017 had a type of date pattern, while the dataset of 
2016 had a different type of pattern. 

The notebook containing the cleaning up can be seen [here](https://github.com/leportella/federal-road-accidents/blob/master/notebooks/Utils.ipynb)


## Models 

Several classificators were using in choosing the best model for the current project:

* Logistc Regression
* Random Forest Classifier
* Gaussian Naive Bayes
* SVM

Each notebook contained one type of model and one type of general strategy, such as 
undersampling or class reduction.

For many models the [GridSearchCV](http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html) 
technique to find the best model with best hyperparameters.

## Techniques

The problem chose faced the problem of having unbalanced classes. The class 2 
(accidents with fatal victims), 
for instance, represented 10% of the quantity of class 1 accidents (accidents 
with injured victims). Trying to fix some approach, the following methos were 
used:

* Class weight: adding a parameter 'balanced' to class weight parameters on model
* Undersampling: restrict the number of available samples to the same number of the 
least represented cathegory. 
* Reducing classes: reduced the smallest class to create only 2 (less unbalanced) classes


### Classification vs Regression problem

From notebooks 1 to 8 and 10, we tried treating the problem as a classification problem, 
trying to predict one out of three possible classes. However, on notebook 9 you can see 
an attempt to treat this problem as a regression problem, trying to predict the number of 
injuried people in an accident. The result was a model with an Mean Absolute Error of 0.87 and 
a Mean Squared Error of 1.88. This , however, was not better than predicting the mean 
value of the people injuried in all car accidents. Thus, this approach was not considered a good one.


## Best model

Although the main accuracry was not the higher achieved throughout all notebooks (0.57), the 
model defined on notebook 04 was, indeed, the best model considering all classes. The results were:

| Class | Precision | Recall |
|-------|-----------|--------|
| 0     | 0.54      | 0.67   |
| 1     | 0.51      | 0.44   |
| 2     | 0.64      | 0.61   |

This was achieved by undersampling the classes by the number of inputs we had on the 
smallest class (class 2). Class 2 had only 10537 cases, so we sampled the same amount 
for class 0 and 1. We had a loss of information in this case, because from 184224 
records available, we only considered 31611 for our model training. However, we had 
good results of recall for classes 0 and 2. Class 1 has a worse result, but the result throughout 
the study was considered good enough.

The model 4 considered a model with multiclass classification. If we take a dualistic representation 
of classes: accidents with no victims and accident with injuried (notebook 07), the accuracy increases to 
0.66.

If we go even further, and predict only accidents with deaths (notebook 10.2), the accuracy reaches 0.76.  



## Detailed Strategies


| Notebook |  Num of Records Considered | Num of Classes | Dummies | PCA | Model Class              | Technique                                                                           |  General Accuracy |
|----------|----------------------------|----------------|---------|-----|--------------------------|-------------------------------------------------------------------------------------|-------------------|
| 1        | 184224                     | 3              | Yes     | No  | Logistic Regression      | GridSearchCV                                                                        | 0.63              |
| 2        | 184224                     | 3              | Yes     | No  | Random Forest Classifier | GridSearchCV                                                                        | 0.62              |
| 3        | 184224                     | 3              | Yes     | No  | Gaussian NB              | None                                                                                | 0.06              |
| 4        | 31365                      | 3              | Yes     | No  | Logistic Regression      | GridSearchCV and undersampling                                                      | 0.57              |
| 5        | 184224                     | 2              | Yes     | No  | Logistic Regression      | GridSearchCV and class reducing                                                     | 0.68              |
| 6        | 31365                      | 3              | Yes     | No  | Random Forest            | GridSearchCV and undersampling                                                      | 0.56              |
| 7        | 130334                     | 2              | Yes     | No  | Logistic Regression      | GridSearchCV, class reducing and undersampling                                      | 0.66              |
| 8        | 31365                      | 3              | Yes     | No  | Logistic Regression      | GridSearchCV, undersampling and less variables                                      | 0.46              |
| 9        | 184224                     | None           | Yes     | No  | Logistic Regression      | GridSearchCV and treating as a regression problem                                   | 0.40              |
| 10       | 184224                     | 3              | Yes     | Yes | Logistic Regression      | One model for each class and a final model considering the results of each model    | 0.63              |
| 11       | 31365                      | 3              | Yes     | No  | Logistic Regression      | GridSearchCV, undersampling (more records on classes 0 and 1)                       | 0.57              |
| 12       | 128332                     | 2              | Yes     | Yes | Random Forest            | GridSearchCV, undersampling                                                         | 0.65              |


Detailed information of precision and recall:

![](https://i.imgur.com/Fcqdmv2.png)
