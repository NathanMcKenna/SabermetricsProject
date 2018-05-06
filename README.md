# Air Quality Effect

For this project I have investigated the relationship between various baseball team stats and the air quality in the cities where those teams reside. 

#### Data

The data used for this project comes from two separate sources. The first is Sean Lahman's baseball database, found here http://www.seanlahman.com/baseball-database.html.

The second dataset used is the Air Quality Annual Summary. This data comes from the EPA's Air Quality System and is collected through monitors located at many different cities throughout the US. The version of the dataset that I used can be found on Kaggle here https://www.kaggle.com/epa/air-quality. Due to the large size of the EPA dataset I was unable to store it on github with the rest of the files and so it needs to be downloaded manually

#### Approach

Since there was no natural intersection between the two datasets, the first and largest step to this project was cleaning and formatting the data to make comparisons easier. 

After importing the datasets into Pandas the next step was to remove unneeded information from the EPA dataframe to make future joins more efficient. With the EPA dataframe using more than 2GB of memory this is an important step. I accomplished this by creating a list of shared cities that contain both EPA collected data and also have a MLB team contained within the Lahman database. This ended up reducing the dataframe size by 90%.

The goal of the next step is to join the two dataframes on the years the data was collected and the city the data was collected in. Since there is no city column within the Lahman teams dataframe it needs to be created. Luckily within the teams dataframe there is a "name" column that does contain the city. For example, the names for the two Chicago teams are "Chicago White Sox" and "Chicago Cubs". Creating a new city column was accomplished by creating a dictionary mapping team names to city. The city name can be extracted from the team name by stripping off the first one or two words. Finally the shared columns between the two dataframes are renamed as prep for the merge. The frames are then merged on the year and city_name columns.

#### Results

A preliminary step was to calculate the correlation matrix for all columns in the new merged dataframe. Unsurprisingly, there are no significant correlations between the columns. However, there is an explanation for this. There are over 1,000 different EPA reading types ranging from ambient temperature and wind speed to concentrations of obscure compounds such as 123-Trimethylbenzene. As it is currently all of these readings are being lumped together as if they are all the same type, completely obscuring any correlations that might exist. Therefore I have chosen particular reading types to isolate and investigate further.

The first reading type I chose was sulfur dioxide concentration, a poisonous gas that makes it very difficult to breath that is formed as a byproduct of burning impure fossil fuels. In this correlation matrix we can start seeing more significant results, with the average yearly sulfur dioxide concentration having a negative correlation of -0.384775 with a team’s strikeout rate and -0.316838 with a team’s fielding percentage. There is also a positive correlation of 0.275465 between the average sulfur dioxide concentration and error rates of players. 

The next reading type I chose to investigate was ozone, a well-known greenhouse whose overabundance can contribute to global warming. Surprisingly there were no apparent correlations here between any baseball stat and ozone concentrations, with no correlation coefficients being larger than +- 0.08

The next up is carbon monoxide concentration, another toxic gas. Again there appears to be a negative correlation with strike out rates (-0.471309), and fielding percentage (-0.412036) while also having a positive correlation with error rates (0.355490).

Moving away from these specific gases I turned to more general readings collected from the EPA. The two readings I investigated next were Suspended Particulate and Total Hydrocarbon concentrations. Similarly to the toxic gases above, there appears to be a negative relationship between strikeout rates and fielding percentage and a positive relationship for error rates.Based on these results it would seem that higher concentrations of "harmful" gases make the game more difficult for the defending team. Pitchers throw fewer strikeouts per season while fielding players "screw up" more frequently.

Next I decided to move away from gas concentrations and turn to more general atmospheric information, namely temperature and wind speed. Surprisingly average ambient temperature did not have any meaningful correlations, with the largest being a negative correlation with strikeouts and homeruns of about -0.1. Wind speed had a similar lack of meaningful results. However there was a positive correlation between wind speed and the number of home runs produced by a team. This makes some sense, as a beneficial wind direction and speed would make the baseball fly farther.

#### Conclusions

This preliminary analysis shows that there is at least some relationship between atmospheric air quality and baseball performance. Concentrations of harmful gases such as carbon monoxide and sulfur dioxide correlate with decreased defensive performance, chiefly in increased strike out rates and fielding errors and overall lowered fielding percentages.

However, as we know, correlation does not equal causation. While it makes intuitive sense that increases in toxic gases decrease athletic performance, this is not enough to definitively say that these gas concentrations are the cause. To truly determine the effect of each individual gas all other gas concentrations and variables would need to be controlled. This type of atmospheric manipulation is not feasible now, but maybe in the future it will be an option. For now, I think it is best for the players to have access to as clean of air as possible, both for performance on the field and living a healthy lifestyle off of it. 





