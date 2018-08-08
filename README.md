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


## Best model

I got a model with accuracy of 0.617, which seems pretty good for a real case with 
no indications if there could be a model that predicts the accidents. The best 
model was the Random Forest Classifier with class weigth balanced. The model can be 
seen in Notebook 02. 
