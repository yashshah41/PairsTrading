# PairsTrading

This project is a basic pairs trading algorithm that given 2 correlated stocks, cointegrates them, and shorts / longs them in reference to 
their cointegrated / predicted values. 

First, I analyzed time series data using Pandas and NumPy to form my cointegration equation in the format ticker2 = a + b * ticker1.
"a" can be found by  ticker2 / (b*ticker1) however B is a bit more tricky. I created a unit root function to help with this by tracking
the change in different and creating a least square regression line that returned a t-statistic based on this. 

The goal was to find the b value corresponding with the lowest t-statistic (most significant). I did this by using 
SciPy minimizes and price of ticker 2 / price of ticker 1 at a given day closing as our minimum value. I chose this based on "a" being 0.
I found our optimal t-statistic, b value, and a value by using this number and therefore was able to construct a new cointegration equation
based on this data. 

Using this equation, I compared it to the actual value and made signals based on it. The signals corresponded with whether to short,
long, or hold (not trade). I repeat this entire process for each day within my window. I subtract a 0.1% transaction fee for each transaction
made. 

Finally, I use Matplotlib to plot the gross and net returns.
