# SGD-Regressor-for-Multivariate-Linear-Regression

## AIM:
To write a program to predict the price of the house and number of occupants in the house with SGD regressor.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Jupyter notebook

## Algorithm
Step 1: Start


Step 2: Load California housing data, select features and targets, and split into training and testing sets.



Step 3: Scale both X (features) and Y (targets) using StandardScaler.



Step 4: Use SGDRegressor wrapped in MultiOutputRegressor to train on the scaled training data.



Step 5: Predict on test data, inverse transform the results, and calculate the mean squared error.



Step 6: End

#### Developed by: Malar Mariam S
#### Register Number: 212223230118

## Program:
```python
  import numpy as np
  from sklearn.datasets import fetch_california_housing
  from sklearn.linear_model import SGDRegressor
  from sklearn.multioutput import MultiOutputRegressor
  from sklearn.model_selection import train_test_split
  from sklearn.metrics import mean_squared_error
  from sklearn.preprocessing import StandardScaler
  #load the california housing dataset
  data = fetch_california_housing()
  #use the first 3 features as inputs
  X= data.data[:, :3] #features: 'Medinc','housage','averooms'
  Y=np.column_stack((data.target,data.data[:, 6]))
  x_train,x_test,y_train,y_test = train_test_split(X,Y,test_size=0.2,random_state=42)
  #scale the features and target variables
  scaler_x = StandardScaler()
  scaler_y = StandardScaler()
  x_train = scaler_x.fit_transform(x_train)
  x_test = scaler_x.transform(x_test)
  y_train = scaler_y.fit_transform(y_train)
  y_test = scaler_y.transform(y_test)
  #initialize the SGDRegressor
  sgd = SGDRegressor(max_iter = 1000,tol = 1e-3)
  #Use Multioutputregressor to handle multiple output varibles
  multi_output_sgd = MultiOutputRegressor(sgd)
  #train the model
  multi_output_sgd.fit(x_train,y_train)
  #predict on the test data
  y_pred = multi_output_sgd.predict(x_test)
  #inverse transform the prediction to get them back to the original scale
  y_pred = scaler_y.inverse_transform(y_pred)
  y_test = scaler_y.inverse_transform(y_test)
  #evaluate the model using mean squared error
  mse = mean_squared_error(y_test,y_pred)
  print("Mean Squared Error:",mse)
  #optionally print some predictions
  print("\npredictions:\n",y_pred[:5])

```

## Output:
![image](https://github.com/user-attachments/assets/e73d7abf-037f-448d-b75c-6f14e99949dd)


## Result:
Thus the program to implement the multivariate linear regression model for predicting the price of the house and number of occupants in the house with SGD regressor is written and verified using python programming.
