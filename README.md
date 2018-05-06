# Air Quality Effect

For this project I have investigated the relationship between various baseball team stats and the air quality in the cities where those teams reside. 

#### Data

The data used for this project comes from two seperate sources. The first is Sean Lahman's baseball datebase, found here http://www.seanlahman.com/baseball-database.html.

The second dataset used is the Air Quality Annual Summary. This data comes from the EPA's Air Quality System and is collected through monitors located at many different cities throughout the US. The version of the dataset that I used can be found on Kaggle here https://www.kaggle.com/epa/air-quality. Due to the large size of the EPA dataset I was unable to store it on github with the rest of the files and so it needs to be downloaded manually

#### Approach

Since there was no natural intersection between the two datasets, the first and largest step to this project was cleaning and formatting the data to make comparisons easier. 

After importing the datasets into Pandas the next step was to remove uneeded information from the EPA dataframe to make future joins more efficient. With the EPA dataframe using more than 2GB of memory this is an important step. I accomplished this by creating a list of shared cities, places that contain both EPA collected data and also have a MLB team contained within the Lahman database. This ended up reducing the dataframe size by 90%.

The goal of the next step is to join the two dataframes on the years the data was collected and the city the data was collected in. Since there is no city column within the lahman teams dataframe it needs to be created. Luckily within the teams dataframe there is a "name" column that does contain the city. For example, the name for the two Chicago teams are "Chicago White Sox" and "Chicago Cubs". Creating the a new city column was accomplished by creating a dictionary mapping team names to city. The city name can be extracted from the team name by stripping off the first one or two words. Finally the shared columns between the two dataframes are renamed as prep for the merge. The frames are then merged on the year and city_name columns.

#### Results

A preliminary step was to calculate the correllation matrix for all columns in the new merged dataframe. Unsurprisingly, there are no significant correlations between the columns. However, there is an explanation for this. There are over 1,000 different EPA reading types ranging from ambient temperature and wind speed to concentrations of obscure compouns such as 123-Trimethylbenzene. As it is currently all of these readings are being lumped together as if they are all the same type, completely obscuring any correlations that might exist. Therefore I have chosen particular reading types to isolate and investigate further.

The first reading type I chose was sulfur dioxide concentration, a poisonous gas formed as a by product of burning impure fossil fuels. In this correlation matrix we can start seeing more significant results, with the average yearly sulfur dioxide concentration having a negative correlation of -0.384775 with a teams strikeout rate and -0.316838 with a teams fielding percentage.




