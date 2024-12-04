# Forecasting Political Contributions

## Objective and Use Cases

I have taken on the challenge of forecasting contributions to the 4 major political parties in Canada using Elections Canada data from 1993 to 2023(excluding 2024, as it is not complete at the time of publishing). This project is a foundational step in understanding campaign contributions for a number of different use cases, including estimating campaign budgets for parties and estimating opponents' budgets. The contribution amount can also be seen as a proxy for the public support of each party using publically available data as a supplement to more expensive data.  

## The Data
[Elections Canada](https://www.elections.ca/content.aspx?section=fin&dir=oda&document=index&lang=e) 

Elections Canada provides 5 .csv files containing contributions towards parties and candidates; I imported these data, cleaned and combined them into six datasets less than 50MB designed to be combined into one with a sorted date time index. Note: to run 01_cleaning.ipynb you must first download the appropriate files from Elections Canada. 

## Data Exploration

Initial exploration looked at the distribution of contribution data, finding that there is an extreme variance in the value of contributions from many small, less than $100, to a few contributions in the million-dollar range. Breaking the data down by party and plotting it over time revealed certain findings in the data.

1. Election years have a higher number of contributions leading to more total contributions
2. The mean value of contributions dropped off in 2004 when legislation reducing contributions from organizations took effect.
3. No seasonality was detected in the data  

## Modeling Conclusions

First, I added two additional columns to take into account the above patterns by adding an election year column and a pre-2004, both being binaries. The first model I created was the simple mean baseline model to be compared to later modeling. Two other models were used Linear Regression and ARIMAX. Both models were used to predict total contributions from 2019-2023 for each party and then have those results compared to the actual values from those years, using root mean squared error(RMSE) and mean absolute error(MAE). linear regression modeling was used with some success, scaling the y variable during fit did not produce results. Most models performed better than the baseline, but the Bloc Québécois's model performed worse across the board. The highest-performing models were the Liberal and NDP with $45.9 and $2.9 million RMSE, respectively, while their baseline models performed $10 million for the Liberals and $4.9 million for the NDP. Even with this significant improvement, I am only confident that they can provide generally accurate forecasting. The Conservative predictions, while better than the baseline, do not indicate reliable forecasting into the future. 

## For the Future

Political life has a complexity to it that my modeling is not fully capturing. Going forward, I would like to add more supporting X variables, which could help improve predictions. Ideas include.

1. Current proportion of seats in Parliament
2. Opinion Polling on the parties
3. By-election results
4. level of contestation in leadership elections

Further, I have only tried a limited number of models, but using logistic regression and polynomial regression could provide useful results. I could also try modeling the number of contributions and mean contribution for that year before combining them into a total contribution metric. This would allow for the isolation of more particular patterns in the data. There is also the need to investigate the reason for Conservatives' contributions spiking and diving so intensely, which is the primary cause of poor prediction.  

# Data Files

1. Data Folder: contains the 6 cleaned canada_contributions_data files hosted on GitHub. Note: the raw data available at this address [Elections Canada](https://www.elections.ca/content.aspx?section=fin&dir=oda&document=index&lang=e)

   Data Dictionary for the above files

   1. fiscal/election_date(DateTime): The index and the year of the contribution in Pandas DateTime format
   2. year(int): a derivative of the index with only the year
   3. political_party_of-recipient(string): which of the 4 major political parties are being contributed too
   4. monetary_amount(float): amount in dollars provided to the party of party member
   5. non_monetary_amount(float: equivalent value of contribution in dollars
   6. total_contribution(float): the sum of monetary and non_monetary amounts for that entry
   
3. Code: Separated into 4 .ipynb files and a functions.ipynb which contains the functions used in the other notebooks.  
4. yml Folder: Contains the .yml files which can be used to create conda environments to run the code files. base_env runs 01-03 and sktime_env runs 04.
5. Visuals Folder: contains the pdf of presentation slides and the plots used in those slides.
6. .gitignore: Will ignore the raw Elections Canada data if a commmit is initiated as those files are too large for GitHub. 



