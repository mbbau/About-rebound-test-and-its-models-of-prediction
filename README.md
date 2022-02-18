# Can the accuracy of the Rebound Method for testing concrete Strenght be improved?

## Introduction

In this work, I use machine learning to try to improve the concrete strength prediction made by using the rebound method with the Schmidt Hammer.
Given the fact that the rebound hammer provides a quick and inexpensive mean of checking the uniformity of concrete, it's limitations make this non destructive test unreliable
to predict the concrete strength. But, do the limitations come only from the device and the method itself? 
Is there a way to include some of the known parameters that affect the test in the calibration procedure in order to reduce uncertanty?
Is there a better model to calibrate it? 

I will try to answer all this questions with this work.

## The current model of prediction

The current model of prediction is a linear regresion about the correlation between the rebound and the strenght of the concrete. 
In the nxt figure can be seen that such a relationship really exists.

![Regresión lineal](https://user-images.githubusercontent.com/61053776/154716078-36f8e7f3-883d-4939-a4b1-6d6b14508f22.png)

Usually in the calibration stage, there are no control over the sample size in order to verify if the model is performing well, assigning to the method values of R2 above 0,9
that are not compared to a test set, and if we make a graph of the evolution of R2 against the sample size for the calibration, we can clearly see, that the meassure for the
model performance has a roof and converge between the train set and the test set as can be seing in the next figure.

![Learning curve - Linear regression](https://user-images.githubusercontent.com/61053776/154716819-716189f7-dc3d-4c88-a773-183604cb8fd7.png)

If we compute the residuals for this method and make a histogram of it, it shows why the results rebound hammer are not very trusted in the field of non destructive methods. 
It can be seeing from the histogram that the values can vary from -10 to +10 MPa in the prediction for the concrete strenght.

![Residuals for linear regression model](https://user-images.githubusercontent.com/61053776/154717401-e2bb67b1-64af-4f0c-83cd-46acecb8605b.png)



