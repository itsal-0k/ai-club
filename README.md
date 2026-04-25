# ai-club
task submissioon


since we had to find the electricity consumed in the next hour we used models to predict it.

first i cleaned the data. the economic dataset had a lot of indicators but i only kept the useful ones which were gdp per capita, total population, urban population share, gdp growth, and electricity access. the weather data also had one extra row on top that was not useful so i removed that too.

after cleaning i merged all three datasets together. the economic data was joined using the year column and the weather data was joined on the exact datetime so each hour gets the right weather info.

then i handled the missing values. for columns like solar, wind, and power imports from india and nepal i used forward fill for data after 2015 and filled the rest with zero since those sources did not exist before. for weather columns like temperature and humidity i used linear interpolation to fill the gaps.

after that i made new features from the data. i added lag features which were demand from 1 hour ago, 24 hours ago, and 1 week ago so the model could learn from what happened before. i also added time features like hour of the day, day of week, and month. since friday and saturday are weekends in bangladesh i made a weekend flag too. i also pulled day peak and evening peak info from the remarks column. rolling averages of temperature and humidity over 6 and 12 hour windows were also added.

before building the models i did a quick eda. i plotted the demand distribution and flagged spikes using mean plus two standard deviations. i also made a correlation heatmap which showed that the 1 hour lag and hour of day were most closely linked to demand.

for modelling i split the data 80-20 by time so the test set is always in the future. i trained three models which were xgboost, random forest, and linear regression as a baseline. xgboost gave the best result with a mape of 4.64%, random forest got 5.84%, and linear regression got 5.94%. so xgboost was clearly the best model for this task.
