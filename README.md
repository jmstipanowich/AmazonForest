# The Amazon Rainforest: The Fight Against Deforestation

![Amazonforest.img](Images/Bernardo-Flores_Barcelos_6.jpg)

Author: James Stipanowich

## Project Overview

The Amazon rainforest is disappearing at an alarming rate. Each year thousands of kilometers of rainforest are destroyed. The Amazon rainforest is the world's biggest rainforest.  The Amazon rainforest offers a huge ecosystem that holds about 30 percent of the world's species. The Amazon sustains many people, animal, and plant varieties. What happens if the developing life in this part of the world is destroyed? What massive repercussions could there be on the world as a whole? The Amazon has the power to create its own weather. How will weather patterns change if the Amazon is destroyed? What if people attempt to overtake nature and destroy the Amazon by human means? How will the deforestation of the Amazon influence many aspects of life such as the conquests for forest fires, the configurations of weather phenomena, the growth of population, and the expansion of GDP? Will the Amazon rainforest still exist in years to come if deforestation continues? 


## Business Problem

For this project I am acting as a data scientist with a wildlife organization in Brazil to determine if Amazon deforestation is increasing. I want to determine what factors influence the deforestation of the Amazon and on what scale their influence lies. I plan to conclude whether forest fires are correlated with deforestation and what patterns and information lie with the occurrences of forest fires for a variety of Brazilian states that may impact deforestation.

## The Data

The data for my project came from a variety of different sources. 

I compiled three Kaggle datasets for my project from https://www.kaggle.com/mbogernetto/brazilian-amazon-rainforest-degradation. The first Kaggle dataset on Amazon deforestation was originally sourced from The Brazilian Amazon Rainforest Monitoring Program by Satellite. The dataset contains 16 rows and 11 columns. The second Kaggle dataset about fire outbreaks came from The Fires Database at The National Institute for Space Research. The dataset holds 16 rows and 4 columns. The third Kaggle dataset on weather phenomena was initially derived from Golden Gate Weather Services. The dataset has 2104 rows and 6 columns.

I obtained additional data of Brazilian population statistics from https://www.macrotrends.net/countries/BRA/brazil/population. 

I used data of Brazil GDP statistics from The World Bank Group at https://data.worldbank.org/indicator/NY.GDP.PCAP.CD?end=2019&locations=BR&start=1960&view=chart.

All data I included occurred between the years 1999 and 2019.

## Data Preparation

In order to start to distinguish if Amazon deforestation is decreasing, I created a plot of the total deforestated area across all states for each year between 2004-2019. The plot is below:

![Deforestation.img](Images/Amazondeforestationtotals.png)

The year 2004 had the most deforestation out of the years between 2004 and 2019 and the year 2012 had the least deforestation out of the years between 2004 and 2019. Deforestation generally decreased from 2004-2012, but then steadily increased in more current time from 2012-2019. 

I desired to identify how Amazon deforestation totals as a whole associate with each Brazilian state, weather phenomena, forest fires, population, and GDP(US dollars). I constructed a variety of plots and graphs to look at each of the mentioned features in relation to Amazon deforestation totals between 1999-2019.

Weather phenomena was found to have little correlation with Amazon deforestation between 1999-2019 so I did not include this element for analysis when I went on to further analysis and modeling. Overall, there was a lack of a strong relationship between weather phenomena and Amazonian deforestation, which suggests more human causes of deforestation than natural causes.

I created a dataset to look at the correlation of the other deforestation related features in comparison with Amazon deforestation as a whole. My correlation plot is as follows:

![Correlation.png](Images/correlation.png)

The deforestation amounts for the Brazilian states of Mato Grosso, Para, and Rondonia were the most correlated with total Amazon deforestation amounts across all states.  These states are pretty large states so holding high correlation percentages with total Amazonian deforestation is not unusual. Firespots were about 83% correlated with the Amazon deforestation total suggesting a strong relationship between fire outbreaks and Amazonian deforestation. Fire outbreaks may lead to deforestation. Population and GDP per capita(US dollars) had strong inverse correlations with total deforestation. The more the Amazon was deforested, the less population and GDP per capita(US dollars). Population was about 71% inversely correlated with total Amazon deforestation and GDP per capita(US dollars) was about 86% inversely correlated with total Amazon deforestation. Population decreasing with more Amazon deforestation sadly makes sense. GDP per capita(US dollars) decreasing with increasing deforestation of the Amazon could be concerning.

I used the correlation plotted features that relate to Amazon deforestation when I went on to modeling. 

## Data Modeling

### Modeling 1: 

The first model I designed was a baseline linear regression model to predict how population, GDP per capita(US dollars), and firespots related to Amazon deforestation totals.

My model predicted population, GDP per capita(US dollars), and firespots all as having an inverse relationship with my target variable of total deforestation. That means that population, GDP per capita(US dollars), and firespots all decrease with more deforestation. This result was different than my correlation plot with regard to firespots. The causes of firespots vary in general because firespots can be activated in both human and natural ways. My model was very overfit with an 86% r2 score for my training data and a 44% r2 score for my testing data. This is probably due to the small amount of data fed into my model influencing a tight fitting to few individual data points. Because of the r2 scores, I do not necessarily trust the inverse relationship this model projected between firespots and deforestation. I plan to look at firespots in more detail in future models because they seem to produce varying results. 

### Modeling 2:
Fire outbreaks seemed to have a predominant decline in volume between the years 1999-2019, but there are periods or years with a higher number of firespots than previous years that I noticed in my analyses. 

I created a function that formulates a dataframe with the number of firespots per month for a given year in a dataset and also contains the minimum, maximum, and mean number of firespots per month for each of the previous years in the dataset combined to analyze how one given year of monthly firespots compares to other previous years of monthly firespots across all states.

I tested my dataframe function on the year 2019 because I have been using that year to do a lot of modeling analyses and comprehend firespots correlations between that year and previous years. I desired to know how 2019 compared to previous years in terms of firespot totals from the dataset to better understand if deforestation is increasing over time with relation to firespots. I graphed my analysis as well:

![YearlyFires.png](Images/yearlyfires2019.png)

The year 2019 generally had a lower than average number of firespots compared to total firespot averages for previous years between 1999-2019. However, the months of March and April had a number of firespots in 2019 that was higher than the maximum number of firespots for those months in previous years. This is concerning data. The high number of firespots in March and April of 2019 suggests there are still times when firespot totals are reaching dangerously high levels. The numbers could be significantly problematic when related to the deforestation of the Amazon in Brazil in the future.

### Modeling 3:

Because firespots had a correlation with Amazon deforestation of 83%, I decided to do more firespots anaylsis in relation to deforestation. I generated time series for each Brazilian state encompassing the Amazon that displayed fire outbreak amounts per month and year. I graphed the time series together below:

![StateTimeSeries.png](Images/statetimeseries.png)

The group of time series graph above shows that most all of the Brazilian states follow similar seasonality trends.  The Brazilian states of Mato Grosso, Para, and Rondonia appear to lead the group of trends with their high firespot totals. Roraima is the only Brazilian state that seems to have its own trend line that follows a different pattern than the other Brazilian states, but its trend is still a seasonal trend. Seasonal firespot trends may influence deforestation totals.

I proceeded to use arima modeling procedures on each Brazilian state within the Amazon individually to predict the number of firespots per month in the year 2019 and interpret the impact firespots had on each Brazilian state within the Amazon in 2019. The Brazilian states of Amazonas and Roraima had higher total firespot outbreaks in 2019 than all previous years from the data provided. Also, the actual total number of firespots for these states was higher than the predicted values for the number of firespots for these states.

## Conclusions

- Acknowledge high deforestation totals and strong seasonality trends of firespots within the Brazilian states of Mato Grosso, Para, and Rondonia to mitigate further and continuing deforestation issues identified within these states. Deforestation has not necessarily decreased over time in these states or as a whole.

- Recognize implications of unprecedented firespots for the months of March and April in 2019 and the states of Amazonas and Roraima in 2019 in correlation with deforestation of the Amazon rainforest.

- Make appropriate environmental preparations for the seasonality trends of firespots.

- Employ efforts to enforce stronger fire restrictions during strong firespot season to reduce deforestation.


## Recommendations for Further Analysis

- Integrate more features such as annual soybean yields, annual timber production amounts, and number of cattle ranches in Brazil per year in future modeling. Soybean production, the manufacturing of timber, and the formations of cattle ranches strongly impact the quantities of Amazonian deforestation in Brazil.

- Incorporate and analyze satellite image classification information that show different activities relating to deforestation and whether or not deforestation is occurring at given times. These images aid in dertermining when deforestation is happening.


## For More Information

See the full analysis of my findings in Amazon.ipynb

Contact me at jmstipanowich@gmail.com

## Repository Structure

├── Images

├── README.md

├── RecommendationSystems.pdf

├── Recommendations.ipynb

