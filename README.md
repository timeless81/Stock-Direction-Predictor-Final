# Stock-Direction-Predictor
### Notebook link - https://github.com/timeless81/Stock-Direction-Predictor/blob/main/Stocks.ipynb

### *"This product uses the FRED® API but is not endorsed or certified by the Federal Reserve Bank of St. Louis."



## Overview
The intent of this project is to predict the direction of movement of the stock price based on several different factors like momentum, lag, technical indicators etc. 
Based ont the stock movement direction the user of this ML system can take automatic bets if the ratio of success/failure is somewhat skewed. A 60:40 ratio would be a great winner.


## Key Features
### 1. Price based features
OHLC - Open, High, Low, Close.  
Prive 20 day moving average.  
Price 50 day moving average.  
Price 2000 day moving average.   

### 2. Volume based features
Volume spike.  
Volume moving average.  

### 3. Indices movement - reflects broader market movements
NASDAQ & S&P movement

### 4. Technical indicators
a. RSI - Relative Strength Index  
b. Bollinger Band - They consist of three lines plotted on a stock chart:   
    Middle band → a moving average (usually 20-day).   
    Upper band → middle band + volatility (standard deviation).  
    Lower band → middle band − volatility.  
Momentum.  

### 5. Lag features 
Past 1 day return.   
Past 2 day return.  

### 5. Seasonality
Day of the week.    
Month of the year. 

### 6. Market sentiments
Twitter analysis.  
Reddit analysis.  
News analysis.  

### 7. Macroeconomics
Interest rate.   
Gold price.  
Bitcoin price.  
Fed decisions.  

### EDA (Exploratory Data Analysis)

#### Boolinger Band 
![My Image](bollinger.png)

### Price vs moving averages
Plotted with moving average of 20, 50 and 200 days. 
![My Image](price_vs_ma.png)
### Price vs momentum indicators
The growing spike amplitudes on the momentum indiactos is a good reflection of upwards trending closing price

![My Image](price_vs_momentum.png)
### The setup 
The main setup is that when you start from this date and by this date how much money will you have or by how much will the stocks up or down.

## EDA Observations:

### 1. Correlation heat map - suggests closing price is highly correlated with sp500, nasdaq and dowjones
So we can drop those features
![My Image](corr_heatmap.png)


### 2. The stock direction:
![My Image](stock_direction.png)

From the above plot it is apparent that stock moves up about 53% of time and down for 47% of the time. Which is close to a 50:50 split and therefore the prediction of the stock direction(Target) is not going to be simple modeling.


### 3. Lag features do not correlate well with the target. Here is the correlation plot
![My Image](lag_feature_corr_with_target.png)

This happens because the linear correlation between those features is missing.

However, doing a rolling mean average of the target resulted in a good correlation.

![My Image](corr_lag_vs_target_rmean.png)
### Explaination - Why target lags correlation with Target is small

## Feature Engineering -
Added the following features to the data to enrich the trends in the data.
1. Added lag features.
2. Added stock returns.
3. Added momentum features - ROC, Bollinger bands, MACD, RSI etc.
4. Added seaonality features like, day, week and quarter in the data.

## Base Model -
Logistical regression was used as the base model for this due to its efficiency in binary classification problems. It becomes a model to compare other models.

### Evaluation Metric -
Stock data is sensitive to the false prediction either false positive or false negative. 
Precistion suggests that when the model says “stock will go up", how often is it correct
Recall suggests that Out of all actual sotck up days, how many did the model catch?
Since both the precision and recall have to be balanced so F1 score is chosen as the evaluation metric, requiring both of them to be high

F1 = 2 * (precision*recall)/(precision+recall)

Why accuracy is not the main evaluation metric -
It is because the accuracy suggest the overall correctness. In stock prediction, precision reflects the quality of buy signals, while recall captures the ability to identify profitable opportunities.





