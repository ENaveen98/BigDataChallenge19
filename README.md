# BigDataChallenge19
The Winning Solution for the Finals of Big Data Challenge powered by HSBC under Shaastra 2019.

Problem Statement:
The aim of the problem is to develop a forecasting model to predict a stock's short-term price
movement. The use of such prediction models is widely prevalent in algorithmic trading. Algorithmic
trading, sometimes referred to as high-frequency trading in specific circumstances, is the use of
automated systems to identify true (money making) signals among massive amounts of data that
capture the underlying stock dynamics. These models can be leveraged to develop profitable trading
strategies (akin to hedge funds) to help investors/traders achieve better returns. Contestants are
expected and encouraged to think of empirical models/heuristics in order to better predict the price
evolution of the hypothetical stock.

Description:
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
