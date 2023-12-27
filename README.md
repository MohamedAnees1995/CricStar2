# Mobile Price Range Prediction (Classification)


## Objective
The main objective of this project is to build a predictive model, which predicts whether the price range of mobile phones available in the market on the basis of various mobile featrures.
Mobile price ranges are as 0(low cost), 1(medium cost), 2(high cost) and 3(very high cost). Therefore this is a multiclass classification problem.

## Dataset used
 The dataset provides the information about following features of mobile phones.



```
- Data Description -

- Battery_power : Total energy a battery can store in one time measured in mAh
- Blue : Has bluetooth or not
- Clock_speed : speed at which microprocessor executes instructions
- Dual_sim : Has dual sim support or not
- Fc : Front Camera mega pixels
- Four_g : Has 4G or not
- Int_memory : Internal Memory in Gigabytes
- M_dep : Mobile Depth in cm
- Mobile_wt : Weight of mobile phone
- N_cores : Number of cores of processor
- Pc : Primary Camera mega pixels
- Px_height : Pixel Resolution Height
- Px_width : Pixel Resolution Width
- Ram : Random Access Memory in Mega Bytes
- Sc_h : Screen Height of mobile in cm
- Sc_w : Screen Width of mobile in cm
- Talk_time : longest time that a single battery charge will last when you are
- Three_g : Has 3G or not
- Touch_screen : Has touch screen or not
- Wifi : Has wifi or not
- Price_range : This is the target variable with value of 0(low cost), 1(medium cost), 2(high cost) and 3(very high cost). (DEPENDENT VARIABLE)

```

- Total number of rows in data : 2000
- Total number of columns : 21
## Data Cleaning and Feature Engineering

### (1) Removing Duplicate rows
- No duplicate rows were present in dataset.

### (2) Handling null values
- No Null values were found in dataset.

### (3) Removing invalid values
- Found some values of `px_height` and `sc_w	` to be 0. Replaced them with median value of respective column.

### (4) Handling skewness
- Used logarithmic transformation to reduce skewness of `clock_speed`,`fc`,`px_height`,`sc_w`.

### (5) Handling outliers
- No outliers were found.

### (6) Rescaling of features
- Used `StandardScaler` for rescaling of features.This step scales data into a uniform format that would utilize the data in a better way while performing fitting and applying different algorithms to it. 

## Exploratory Data Analysis

Visualization of data were mainly performed using Matplotlib and Seaborn libraries and the following graph and plots had been used:
  - Bar Plot.
  - Histogram.
  - Scatter Plot.
  - Line Plot.
  - Heatmap.
  - Box Plot
             


- Dataset found to be balanced.
- Phones with higher RAM has higher prices.
- Except for `RAM` none of the independent features were correlated to `price_range`.


### Feature Selection

Feature Selection is crucial step before model training as it improves the performance of model and also to reduce multicollinearity in dataset.


```

         Feature selection increases the predictive power of machine learning algorithms by selecting the most important variables 
         and eliminating redundant and irrelevant features. For selecting features I have used `correlation heatmap`.         
                      
                 
          (a) Correlation heatmap :
          
                 (i) `sc_w` found to be correlated with `sc_h`.
                      
                      New feature `sc_area` is created and `sc_w` and `sc_h` are dropped.
                      `sc_area` = `(sc_h * sc_w)/2`
                      
                 (ii) `px_width` and `px_height` found to be correlated.
                 
                       New feature px_area` is created and `px_width` and `px_height` are dropped.
                      `px_area` = `(px_height * px_width)/2`
                      
                 (iii) `fc` and `pc` found to be correlated.
                 
                       New feature avg_cam` is created and `fc` and `pc` are dropped.
                      `avg_cam` = `(fc + pc)/2`
                      
            
```

### Features for model building

Input independent features used for model building are as follows:


```
- Battery_power 
- Blue
- Clock_speed
- Dual_sim
- avg_cam 
- Four_g
- Int_memory
- M_dep 
- Mobile_wt 
- N_cores 
- Px_area 
- Ram 
- Sc_area
- Talk_time 
- Three_g
- Touch_screen 
- Wifi : Has 

```



## Model Building


Since we have to predict the mobile price range where ranges are: 0(low cost), 1(medium cost), 2(high cost) and 3(very high cost).So this is a multiclass classification problem. Based on the problem statement I decided to develop predictive models using following algorithms and have compared there performance.
```
- Logistic Regression
- SVM Classifier
- Random Forest Classifier
- Gradient Boosting Classifier
- KNN Classifier



Following necessary steps have been employed for better model performance.
                (i)   train test split for model evaluation.
                (ii)  Hyperparameter tuning for best learning parameters that developed a better model. Hyperparameter tuning was done with the help
                      of RandomizedSearchCV.
                (iii) Since, we have to build multiclass classifier models, in logistic regression `multi_class='multinomial'` has to be specified.
                      
                      
                  
```


### Evaluation metrics

To evaluate the models I have used  `F1-score`.


## Conclusion

```
                 (i) Gradient boosting was most accurate as compared to other model.
                          f1- score                     = 0.91
                 (ii) Performing hyperparamter tuning by RandomSearchCV improved f1-score in SVM model
                         f1-score before tuning         = 0.88
                         f1-score after tuning          = 0.91
                 (iii) Of all models KNN performed worst.
                         f1-score                       = 0.52
           

```

