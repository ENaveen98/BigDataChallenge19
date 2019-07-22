# BigDataChallenge19
The Winning Solutin for Big Data Challenge powered by HSBC under Shaastra 2019.

Problem Statement:
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
events and future stock price for 30 seconds time-horizons. 
