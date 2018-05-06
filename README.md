# Air Quality Effect

For this project I have investigated the relationship between various baseball team stats and the air quality in the cities where those teams reside. 

#### Data

The data used for this project comes from two seperate sources. The first is Sean Lahman's baseball datebase, found here http://www.seanlahman.com/baseball-database.html.

The second dataset used is the Air Quality Annual Summary. This data comes from the EPA's Air Quality System and is collected through monitors located at many different cities throughout the US. The version of the dataset that I used can be found on Kaggle here https://www.kaggle.com/epa/air-quality. Due to the large size of the EPA dataset I was unable to store it on github with the rest of the files and so it needs to be downloaded manually

#### Approach

Since there was no natural intersection between the two datasets, the first and largest step to this project was cleaning and formatting the data to make comparisons easier. 

After importing the datasets into Pandas the next step was to remove uneeded information from the EPA dataframe to make future joins more efficient. With the EPA dataframe using more than 2GB of memory this is an important step. I accomplished this by creating a list of shared cities, places that contain both EPA collected data and also have a MLB team contained within the Lahman database. This ended up reducing the dataframe size by 90%.

The goal of the next step is to join the two dataframes on the years the data was collected and the city the data was collected in. Since there is no city column within the lahman teams dataframe it needs to be created. Luckily within the teams dataframe there is a "name" column that does contain the city. For example, the name for the two Chicago teams are "Chicago White Sox" and "Chicago Cubs". Creating the a new city column was accomplished by creating a dictionary mapping team names to city. The city name can be extracted from the team name by stripping off the first one or two words. Finally the shared columns between the two dataframes are renamed as prep for the merge.


