# Big Data Challenge 19
The Winning Solution for the Finals of Big Data Challenge powered by HSBC under Shaastra 2019.

### Problem Statement:
The aim of the problem is to develop a forecasting model to predict a stock's short-term price
movement. The use of such prediction models is widely prevalent in algorithmic trading. Algorithmic
trading, sometimes referred to as high-frequency trading in specific circumstances, is the use of
automated systems to identify true (money making) signals among massive amounts of data that
capture the underlying stock dynamics. These models can be leveraged to develop profitable trading
strategies (akin to hedge funds) to help investors/traders achieve better returns. Contestants are
expected and encouraged to think of empirical models/heuristics in order to better predict the price
evolution of the hypothetical stock.

<p align="center">
  <img src="Images/Algo%20Trading.jpg">
</p>

### Dataset Description
<p align="center">
  <img src="Images/Dataset%20Format.png">
</p>

### Built With

* [Python 3.6](https://www.python.org/) - The programming language used.
* [Jupyter Notebook](https://jupyter.org/) - Integrated Development Environment used.
* [pandas](https://pandas.pydata.org/) - Library to load training/test data as csv files.
* [matplotlib](https://matplotlib.org/) - Library to create Visualizations to analyse the data.
* [numpy](https://numpy.org/) - Library used to perform a wide range of Mathematical operations.
* [scikit-learn](https://scikit-learn.org/stable/) - Library used to build and train the framework of the overall predictive model.
* [pickle](https://docs.python.org/3/library/pickle.html) - Library used to save the trained model for reusing purposes.

### Getting Started
* Step - 1 : Features Engineering (#5th Step block in ipython notebook)
  * Merge Trade data with Quote data on Datetime.
  * Find Moving Averages over 5/10/30 previous seconds timeframes for ask price, bid price, ask size,
bid size,mid price which was finalized based on finding feature importance for different timeframes.
  * Find day of the week from datetime made of values 0-6.
  * Find the total seconds completed in a particular day from datetime and subtract 28,808 seconds
which is the value for the first data point at the beginning of the day.
  * Create labels for Classification part of the model to determine if ‘futMid’ price increases or
decreases from ‘mid’ price.
  * Delete data points with size of trade greater than 250 as they seem likely to be outsiders and will
affect the performance of the model(s).
  * Find Imbalance and Share Imbalance.

* Step - 2 : Classification model to predict the direction of mid price movement (#5th Step block in ipython
notebook)
  * Split ‘IN’ data with features Engineered as above into features(26) and labels(1) for classification.
  * Choosing model based on various performance metrics such as precision, recall, classification
accuracy, etc.
  * Fit the ‘IN’ data using Bagging Classifier with Random Forest Classifier as its base estimator.
  * Print classification inference to verify the model.
  * Pickle out this classification model as it takes ample time to train.
  
* Step - 3 : Regression model to predict the mid price change and hence the predicted future mid price (#5th
Step block in ipython notebook)
  * Split ‘IN’ data into labels which is the difference b/w ‘futMidPrice’ and ‘midprice’ and into
features,only this time including the predicted direction of mid price movement found from the
classification model above as a separate feature.
  * Again, based on various performance measures such as absolute loss, mse, etc. fit the ‘IN’ data
with Bagging Regressor with Extra Tree Regressor as its base estimator.
  * Find the predicted Future mid price by adding the above models prediction with the corresponding
mid price.
  * The model is then pickled.
  
* Step - 4 : Fine tuning (#5th Step block in ipython notebook)
  * We find that the overall method to find mid price prediction performs well on majority of the data but
is unstable at certain regions.
  * Finding the pattern by plotting predictions against total seconds completed in that day for ‘IN’ data
as calculated in features engineering and removing any prediction made for those specific small
intervals.

* Step - 5 : Testing Prediction for OUT data (#6th Step block in ipython notebook)
  * Calculating all similar features as used in the above models.
  * Predict the direction of mid price movement from the Classification model first.
  * Then predict the required Future mid price using the Regression model.
  * Finally, find the RMS error and number of valid predictions using the function that is provided
already.
  * Note: If need to predict using new data it should be in the same format as the data that was given
initially. ( i.e. quote_out, trade_out csv files)

* Results and further Scope
  * The classification part of the overall prediction is the most difficult part to predict and we achieved a
really significant change in classification accuracy from the one provided earlier through our robust
model.
  * We carried out the process of fine tuning the model using the ‘IN’ data to help retain only the better
predictions and dump the unstable ones.
  * This was clearly evident when we tested it out with the ‘OUT’ data achieving a RMS error of 1.306
with over 20,000 predictions.
  * Considering the factor that 5,000 predictions are required for submission we did further analysis of
the variation of prediction for each day in ‘IN’ data and finalized a time frame to remove resulting in
over 7,000 predictions with a better RMS error now.
  * We can still hope to achieve a smaller RMSE by dumping predictions from even more unstable
regions, but because of the limited number of days of ‘IN’ data available it may turn out to be a case
of overfitting or a bad practice even though it might reduce RMS error.
  * So we decided to finish our entire prediction model here.
  
### Relevant Files
[Model - Jupyter Notebook](Model.ipynb)

[Final Round Presentation Slides](Big%20Data%20Challenge%202019%20Presentation.pdf)

### Description:
An order driven market is a financial market where all buyers and sellers display the prices at
which they wish to buy or sell a particular security, as well as the amounts of the security desired
to be bought or sold. In these markets, participants may submit limit orders or market orders.

In a limit order, you specify how much of the asset you want to buy or sell, and the price you
want. If there are matching orders on the book (e.g. someone who wants to sell at the same
price, or lower, as the price at which you want to buy), your order will be filled immediately. If not,
your order will stay on the book until matching orders arrive (which could be never). It is also
possible for a limit order to be only partially filled, if the counterparty wants to trade a smaller
amount than you did. In that case the rest of the order remains on the book.

In a market order, you only specify how much of the asset you want to trade. Your order is then
filled immediately at the best price currently available on the market. For instance, if you place a
market buy order, you will be matched with the current lowest-priced sell order on the book. If
that order is not large enough to completely fill yours, the next-lowest sell order will be used to fill
some more of yours, and so on. (You are encouraged to go through the 1st suggested reading
for a pictorial understanding of order book and price dynamics)

In this competition, we use tick data. Tick data refers to any market data which shows the price
and volume of every print. Additionally, changes to the state of the order book occur in the form
of trades and quotes. A quote event occurs whenever the best bid or the ask price is updated. A
trade event takes place when shares are bought or sold.

The aim of this competition is to determine the relationship between recent past order book
events and future stock price for 30 seconds time-horizons. Few factors that are explored in the
literature to predict price movements:
• Order arrival rate
• Bid-ask spread
• Order book imbalance
• Trade volume @ Bid price vs Trade volume @ Ask price
Certain factors, such as current order book imbalance, tend to have good predictive power for
very short-time time-horizons (under 10-20 seconds), however other factors might be important
for time-horizons of more than a minute.
Equity markets are very fast and it is important to understand that multiple high-frequency events
can occur in the same milliseconds. Analysing and understanding the data is critical before
applying machine learning models.
