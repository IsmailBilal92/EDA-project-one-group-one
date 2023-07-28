## COVID-19 Case Fatality Rate, Poverty Rates, and Average Income
The repository related to this topic uses the following files:
* [Analysis by State.ipynb](): data analysis performed at the State level.
* [Analysis by County.ipynb](): data analysis performed at the County level.
* [averageIncome_2021.csv](): data exported from the Analysis by State jupyter notebook to allow for manual modification of the average income custom dataset.
* [averageIncome_2021_adjusted.csv](): the result of the manually adjusted average income csv file to use in the Analysis by State and Analysis by County jupyter notebook files.
* [state_abbrevs.py](): a supporting python file containing the US State abbreviations as a dictionary which is used in both jupyter notebook files.
* [us-counties-2021.csv](): COVID-19 data from 2021 used to merge with the different datasets to use in the analysis and to calculate the case fatality rate (CFR).

### Datasets
In order to answer the question of if areas in the United States (US) of lower socioeconomic status are more likely to experience higher numbers of COVID-19 cases and deaths, three datasets were used:
* Median Income by County in the US: https://apps.bea.gov/api/_pdf/bea_web_service_api_user_guide.pdf
* US County Population: https://www.census.gov/data/tables/time-series/demo/popest/2020s-counties-total.html
* COVID-19 Data in the US: https://github.com/nytimes/covid-19-data

The reason behind going as granular with the data from US Counties instead of States is largely due to the fact that States in America have a large social gradient because there are areas within States that are rich, and others that have people living in poverty. 

### Analysis
The average Income (USD) and Case Fatality Rates (%) of US Counties were explored. Using the merged data frames, the case fatality rate in each county was calculated by dividing the number of deaths in the County by the number of cases in the County using the data from the end of 2021. The reason behind using that particular date is because we are looking at a snapshot in time and the data frame provides the cumulative number of cases. The County data was then sorted by case fatality rate and separately by the average income in each state to produce the following four bar graphs.

![county lowest CFR]()

![county highest CFR]()

![county lowest income]()

![county highest income]()

The expectation was that counties with higher average income would have a lower case fatality rate. The bar plots do not show a definitive relationship. As a result, the data was further explored by looking at the relationship between County and State Average Income (USD) and CFR (%). Outliers were removed from both the County and State level data frames and plotted on a scatter plot to visualize the distribution of data. 

![CFR county income]()

![CFR state income]()

The correlation values for the above two graphs were both very weak: -0.25 for County and -0.18 for State. Taking a deeper look at the State scatter plot, the data is clustered almost like a U shape which inspired the next step of the analysis which was to split the average income data for each State into two groups based on whether they fall below the median income or above the median income. The median income was calculated to be around USD$55k.

T-testing: A T-test was performed for to check if the mean income of two different income groups were different from each other. The results gave a pvalue of 2.2347e-11 which meant we could reject the null hypothesis and that the means from the two groups were different enough. The data was split into the two groups used for T-testing by finding the median income across all of the States in the dataframe. The data was visualized using a scatterplot containing a regression analysis.

![CFR vs avg income < median income]()

![CFR vs avg income > median income]()

The results of these two graphs are interesting and show that areas below the median income have a moderate negative association with poverty rate and CFR. There is a weak positive association with average income higher than the median income in the US and CFR, however, because of the low R^2 value, the distribution of this relationship around the linear regression may not be significant.

The relationship between poverty rate and CFR was also analyzed. Based on the graph below, there is a weak positive correlation between the poverty rate of states in the US and the case fatality rate.

![poverty vs cfr]()

### Summary, Limitations, & Next Steps
Two metrics were analyzed against the case fatality rate of COVID-19 in the US: (1) Average Household Income, and (2) Poverty Rate. The following are observations from the data analysis:
* Average household income in the states seems to play a larger role on COVID-19 CFR when areas are below the median household income in the US based on the dataset that was analyzed.
* The CFR for States in the US with average household incomes greater than the median household income did not show a significant relationship.
* The general trendline for poverty rate vs the CFR for the States in the US shows a weak positive correlation.

A few limitations of the dataset were identified:
* Datasets were analyzed mainly at the State level: not granular enough to capture the social gradient between the upper and lower classes in each State.
* With respect to the median income and poverty rates against COVID-19, the data only looks at a snapshot in time, and does not consider the changing nature of reactions to the pandemic (non-pharmaceutical interventions).
* The only metric used to analyze the impact of COVID-19 on different areas was the case fatality rate. Another metric to consider would be hospitalization rates as they may tell more about the impact of the virus in certain areas.
* The COVID-19 case fatality rate does not represent the full impact of COVID-19. Deaths related to other health conditions are not considered in the analysis and may tell a different story.

To uncover more about the dataset keeping in mind the limitations of this analysis, some ideas for further analysis next steps are highlighted below:
* Analyze the same information by zip code and see if the results are more what the team expected.
* Look more at population density distributions against case fatality rate.
* Hospital ranking.
* Look at the relationship between average quality of healthcare and population density against COVID-19 metrics.