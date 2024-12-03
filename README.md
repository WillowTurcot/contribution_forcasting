# Forecasting Political Contributions

## Objective and Use Cases

I have taken on the challenge of forecasting contributions to the 4 major political parties in Canada using Elections Canada data from 1993 to 2023(excluding 2024, as it is not complete at the time of publishing). This project is a foundational step in understanding campaign contributions for a number of different use cases, including estimating campaign budgets for parties and estimating opponents' budgets. The contribution amount can also be seen as a proxy for public support of each party using yearly, publically available data as a supplement to more expensive data.  

## The Data
[Elections Canada](https://www.elections.ca/content.aspx?section=fin&dir=oda&document=index&lang=e) 

Elections Canada provides 5 .csv files containing contributions towards parties and candidates; I imported these data, cleaned and combined them into one dataset with a sorted date time index. 

## Data Exploration

Initial exploration looked at the distribution of contribution data, finding that there is an extreme variance in the value of contributions from many small, less than $100, to a few contributions in the million-dollar range. Breaking the data down by party and plotting it over time revealed certain patterns in the data.

1. Election years have a higher number of contributions leading to more total contributions
2. The mean value of contributions dropped off in 2004 when legislation reducing contributions from organizations took effect.

## Modeling

First I added two additional columns to take into acount the above patterns by adding an election year column and a pre-2004, both being binaries. The first model I created was the simple mean baseline model to be compared to later modeling attempts. Linear regression with autregression lags and the same while scaling the y variable was my next modeling attempt with some promising initial results. In all cases except for the conservative party and the scaled NDP model, they beat the baseline in root mean squared error and mean absolute error while forecasting 2017-2023. 

