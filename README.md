# UM FinTech Bootcamp Project 1

## [Write a Description]

_The quality of a README desccription often differentiates a good project from a bad project. A good one takes advantage of the opportunity to explain and showcase:_

_What your application does,
Why you used the technologies you used,
Some of the challenges you faced and features you hope to implement in the future._

## [Add a Table of Contents (Optional)]

## Technologies We Installed

In the course of this project we used several technologies:

- Git and Github for Version Control
- Python
- Pandas
- Numpy
- Matplotlib
- yfinance Library
- pycoingecko
- Quandl

## Data Sources Used

### Treasury Markets and the US Dollar Index

In order to perform the data analysis for the 30 Year US Treasury Bond, 10 Year US Treasury Note, and the US Dollar Index, we pulled the data from Yahoo Finance. However, since the Yahoo Finance API was decommissioned in 2017, we installed and imported yfinance.

**yfinance** is a popular open source library built to gain access to financial data from Yahoo Finance. yfinance was built when the Yahoo Finance API was decommissioned.

We accessed data for approximately one year because we analyzed the June Futures Contract of the 30 Year US Treasury Bond (ticker symbol on Yahoo Finance is 'ZBM21.CBT') and the 10 Year US Treasury Note (ticker symbol on Yahoo Finance is 'ZNM21.CBT'). So all three assets where analyzed for the same time period.

## What is the RSI?

### The Relative Strength Index or RSI

A quick summary of the RSI:

- created in in 1978 as a momentum indicator with an optimal look-back period of 14 bars, by J. Welles Wilder.
- the goal is to find areas or zones where the asset is overbought or oversold.
- this method was created to give fundamental analysts a quick way to assess overvalued or undervalued assets.

### RSI Divergence

One way to look at RSI divergence is the RSI can show a change in price momentum, before you see a change in price action. You can think of it as an early warning signal.

> **RSI Divergenc**e occurs when the Relative Strength Index indicator starts reversing before price does. A **bearish divergenc**e consists of an overbought RSI reading, followed by lower high on RSI. At the same time, price must make a higher high on the second peak, where the RSI is lower. In a **bullish divergence** situation, there must be an oversold condition on the RSI, followed by a higher low on the RSI graph. Simultaneously, price must form a lower low on the second peak.

### Application of the RSI for our Project

J. Welles Wilder's original RSI used a smoothed moving average, we instead used the exponential weighted moving average, since it is what is used in most trading packages.

So we:

- took the spread of each time period; essentially the close of the current candle to the close of the previous candle.
- segregated each up and down period to a positive or negative difference, with all things equal to zero.
- calculated an exponential weighted moving average with a period of 14 days of the up and down periods.
- calculated the relative strength (RS) by the ratio of up and down averages.
- used the RSI formula to marmalize the values between 0-100.

## Bonds vs. US Dollar Index Concept

From anecdotal evidence, a pattern was noted in the movement of the Treasury Markets and the US Dollar Index. As money was flowing into the bonds market, the US Dollar Index was experiencing bearish trends. The same was seen vice versa. This led to an understanding that investors move money when they view the US Dollar as weak into the bonds market.

Our hypothesis held _there is a direct inverse relationship between the Bonds market and the US Dollar Index_. Essentially, when the 30 Year T-bond and the 10 Year T-Note would rally, we should see the US Dollar Index move bearish. Similarly, when the US Dollar rallie, we should see the 30 Year T-Bond and 10 Year T-Note move bearish. The inverse of these relationships would be seen, as well.

## [Gold and BitCoin as Safe Haven Assets]

## Research Questions We look to Answer

- What relationships are seen between the three assets (30-year T-Bond, 10-year T-Note, and the US Dollar Index (USDX)?
- How can we apply our findings to currency pair movements?

## [Analysis]

## [References]

- https://www.investopedia.com/terms/r/rsi.asp
- https://kaabar-sofien.medium.com/back-testing-the-rsi-divergence-strategy-on-fx-in-python-c3680e7e2960
- https://www.tradingheroes.com/rsi-divergence-explained/#:~:text=RSI%20Divergence%20occurs%20when%20the,where%20the%20RSI%20is%20lower
- https://medium.com/dev-genius/overlaying-the-relative-strength-index-rsi-on-multiple-stocks-crypto-in-python-64a46f9837a1
- https://www.guggenheiminvestments.com/mutual-funds/resources/interactive-tools/asset-class-correlation-map
- https://www.babypips.com/learn/forex/the-411-on-bonds

## Contributors

- Jonathan Eidam
- William Tate Jones
- Sheldon Palm

## License

    Copyright 2021 Jonathan Eidam, William Tate Jones, and Sheldon Palm.
    This Project is subject to the GNU GPLv3 license.
