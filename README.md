# Can the accuracy of the Rebound Method for testing concrete Strenght be improved?

## Introduction

(Note: in dark mode some of the information in the visualizations will not be watched, I will fix this in the future) 

In this work, I use machine learning to try to improve the concrete strength prediction made by using the rebound method with the Schmidt Hammer. Given the fact that the rebound hammer provides a quick and inexpensive mean of checking the uniformity of concrete, it's limitations make this non destructive test unreliable to predict the concrete strength. But, do the limitations come only from the device and the method itself? Is there a way to include some of the known parameters that affect the test in the calibration procedure in order to reduce uncertanty? Is there a better model to calibrate it? 

I will try to answer all this questions with this work.

## The current model of prediction

The current model of prediction is a linear regresion about the correlation between the rebound and the strenght of the concrete. 
In the nxt figure can be seen that such a relationship really exists.

![Regresión lineal](https://user-images.githubusercontent.com/61053776/154716078-36f8e7f3-883d-4939-a4b1-6d6b14508f22.png)

Usually in the calibration stage, there are no control over the sample size in order to verify if the model is performing well, assigning to the method values of R2 above 0,9 that are not compared to a test set, and if we make a graph of the evolution of R2 against the sample size for the calibration, we can clearly see, that the meassure for the model performance has a roof and converge between the train set and the test set as can be seing in the next figure.

![Learning curve - Linear regression](https://user-images.githubusercontent.com/61053776/154716819-716189f7-dc3d-4c88-a773-183604cb8fd7.png)

If we compute the residuals for this method and make a histogram of it, it shows why the results rebound hammer are not very trusted in the field of non destructive methods.  It can be seeing from the histogram that the values can vary from -10 to +10 MPa in the prediction for the concrete strenght.

![Residuals for linear regression model](https://user-images.githubusercontent.com/61053776/154717401-e2bb67b1-64af-4f0c-83cd-46acecb8605b.png)

From the graph we can infer that with enough samples, the error will tend to zero, but how many test are enough? and at what cost do we want to olwer the error?  Nevertheles the RSME (root square mean error) converge to 4, regardless of the nunver of test we perform, as shown in the next figure.

![Learning curve - Linear regression RMSE](https://user-images.githubusercontent.com/61053776/154720295-b8eb1a07-1412-405d-9fe4-d47a2ca838c1.png)

## Alternative model of prediction

There are lots of papers and manuals that adress the limitations of this non destructive method, and state several factors that have influence in the rebound. By analizing this bibliography, I came up with the idea of using a more complex model to try to predict the concrete's strenght by making use also of several factors of the studied elements, in order to try to lower the uncertainty and the error associated with the prediction. I have tried several methods but here will only be presented the best one so far, XGBoost (I didn't collect enough data to justify a neural network).

The new variables that were added in order to improve the prediction were:

* Concrete's age in days;
* Nominal maximum size of the mix;
* Theoretichal cement content of the mix;
* Type of cement;
* Theoretichal desired slump;
* Sepicified Strenght;
* And if the specimen was from a truck or a laboratory batch.

A copy of the data set used can be found in this repository.

With this extended data set, I calibrate the XGBoost model to obtain the following results:

![Learning curve - XGBoost R2](https://user-images.githubusercontent.com/61053776/154722613-a93f1e0d-eb34-41de-ba91-0f8eb2d8f17e.png)

![Residuals for XGBoost model](https://user-images.githubusercontent.com/61053776/154722674-678918ff-b12a-4c90-b0fd-df13794b2868.png)

As can be seen, there was an improvement not only in R2 but also in the distribution of the residuals from the test set and the train set.






