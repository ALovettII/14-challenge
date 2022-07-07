# 14-challenge
 Creating an algorithmic trading bot that learns and adapts to new data and evolving markets.


## Technologies
Using the Conda package manager: [My GitHub Project](https://github.com/ALovettII/14-challenge.git)

To use this project, you will need the following libraries:
* import pandas as pd
* import numpy as np
* from pathlib import Path
* import hvplot.pandas
* import matplotlib.pyplot as plt
* from sklearn import svm
* from sklearn.preprocessing import StandardScaler
* from pandas.tseries.offsets import DateOffset
* from sklearn.metrics import classification_report
* from sklearn.ensemble import RandomForestClassifier


## Usage
The goal of this project is to create an algorithmic trading bot that learns and adapts to new data and evolving markets.

Procedural Steps Followed:
1. Establish a Baseline Performance
2. Tune the Baseline Trading Algorithm
3. Evaluate a New Machine Learning Classifier
4. Create an Evaluation Report

To modify this code for your own use:
* Change the import variable `ohlcv_df` to upload your data
* Ensure that the columns are renamed to match the Notebook


## Evaluation Report

#### Tuning the Algorithm by Adjusting the Size of the Training Dataset
*"Answer the following question: What impact resulted from increasing or decreasing the training window?"* 

To seek optimal strategy results, I tested both shortened and extended training windows. Shortening the training window had no positive effect in return or acccuracy. However, by increasing the training window one month at a time, I was able to see positive results.

At `DateOffset`= 7 months, there was a 1% increase to precision, recall, and F1 score, most of which applied to the `-1` minority class. This increased total accuracy by 1%. Although the 1% increase is small, it is still a productive increase, yielding better results. Furthermore, the final cumulative product was 1.850; significantly greater (14.4% increase comparitively) than the 1.617 for the baseline strategy, and 1.518 for the `Actual Returns` cumulative return. 

By increasing the DateOffset above 7 months, the results were decreasingly productive, showing reduced accuracy and return.

#### Tuning the Algorithm by Adjusting the SMA Input Features
*Answer the following question: What impact resulted from increasing or decreasing either or both of the SMA windows?*

After resetting the `DateOffset` = 3, I tested various `long-window` (LW) and `short-window` (SW) combinations.

First, I attempted to increase and decresase both the LW and the SW independently, holding the other constant:
* By modifying the SW by increments of 1 day, I found an increase in return (r=1.633) at `SW` = 3; while all other changes yielded reduced return.
* By modifying the LW by increments of of 1 day, I found an increase in return (r=1.644) at `LW`=101; further increases and reductions yielded no better results

However after testing the `LW` and `SW` combinations together, the only postive yield came at `LW`=101 with `SW`=4. This changed had no change to the model accuracy (A=.55).
 
#### Choose the Set of Parameters That Best Improved the Trading Algorithm Returns
Following the same methodology applied to the tuning of the trading algorithm's SMA and training datatset, I tested various combinations of `DateOffset`, `long-window`, and `short-window`.

This experimentation led to my final version of the tuned trading algorithm with the following parameters:
```python
DateOffset = 7
long-window = 3
short-window = 79
```
Yielding the following results:
* Cumulative Return = 1.856
* Accuracy = .56

These were much better results than the baseline trading algorithm. The tuned algrithm was 14.8% greater than the baseline return of 1.617, and increase of 23.9% overall. The overall accuracy of the model increased by 1% to 56% which is relatively small but still positive.

![Baseline Classification Report](https://github.com/ALovettII/14-challenge/blob/main/Resources/Images/Baseline_Report.png)
![Tuned Classification Report](https://github.com/ALovettII/14-challenge/blob/main/Resources/Images/Tune_Report.png)
![Baseline Cumulative Return Plot](https://github.com/ALovettII/14-challenge/blob/main/Resources/Images/Baseline_Plot.png)
![Tuned Cumulative Return Plot](https://github.com/ALovettII/14-challenge/blob/main/Resources/Images/Tuned_Plot.png)


#### Backtest the new model to evaluate its performance
*Answer the following questions: Did this new model pelrorm better or worse than the provided baseline model? Did this new model perform better or worse than your tuned trading algorithm?*

The Logistic regression model performed worse with respect to both the baseline model and the tuned trading algrithm. While the return was the same (r=1.617), the accuracy decreased significantly (A=.52) compared to the baseline (A=.55). Subsequently, it's accuracy was 4% below the tuned trading algorithm.

However, a notable postive of the new model was it's balanced prediction of each class. Where the SVM predicted the `1` class significantly more accurately, the Logistic Regression model predicted both classes with a closer balance between the two, as seen in the report below.

![Logistic Regression Report](https://github.com/ALovettII/14-challenge/blob/main/Resources/Images/LR-Report.png)
![Logistic Regression Cumulative Return Plot](https://github.com/ALovettII/14-challenge/blob/main/Resources/Images/LR-Plot.png)

#### Summary of Model Performance
| Model Name | Accuracy | Cumulative Return |
| ---------- | -------- | ----------------- |
| Baseline SVM | 0.55 | 1.617 | 
| Training Tuned SVM | 0.56 | 1.850 | 
| SMA Tuned SVM | .55 | 1.644 | 
| Optimal Tuned SVM | .56 | 1.856 | 
| Logistic Regression | .52 | 1.617 | 


## Contributors
Created by Arthur Lovett