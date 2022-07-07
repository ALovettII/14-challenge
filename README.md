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

#### Tuning the SMA: Tuning the Algorithm by Adjusting the SMA Input Features
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

| Model Name | Accuracy | Cumulative Return |
| ---------- | -------- | ----------------- |
| Baseline SVM | 0.55 | 1.617 | 
| Training Tuned SVM | 0.56 | 1.850 | 
| SMA Tuned SVM | .55 | 1.644 | 
| Optimal Tuned SVM | 
| RandomForest | 


## Contributors
Created by Arthur Lovett