# Best NYC Locations for a New Chinese Restaurant


## Introduction/Business Problem
As many existing businesses are striving to succeed, new ones are just beginning to leave their mark. A new Chinese restaurant is opening in New York City, but the location has yet to be determined. It is very important to choose a good, reputable location when starting a new business to attract a large customer base. In this project, we will help the client find an ideal list of neighborhoods to open a Chinese restaurant.


## Data
Most potential customers nowadays will turn to the internet to find a new place to visit. They may compare restaurants to see which place better fits them and their cravings. Some features that they may look at is the rating, reviews, cuisine type, price range, menu items, etc.  Since these people are potential customers, businesses want to build a good reputation to make themselves stand out.  A couple of factors that make a business stand out on the web is a high rating and a large number of positive feedback. These two features can be a big indicator of the success of the restaurant and the quality of its food and service. 

The location can also be a factor in the success of a restaurant. Selecting a location for a restaurant is not easy, but it is critical to find the right neighborhood for your business. One way to start this search is by evaluating what others business owners have done before you. Looking at the average neighborhood reputation for Chinese restaurants can be helpful as you do not want to start your business in a negative light. It is also important to factor in the demographic data because that can impact the number of customers that you will receive. In this project, we will include both the reputation (average and variance of rating and number of likes) and the demographic data (population density, total population, and Chinese population). The goal is to cluster the neighborhoods by using different subsets of these features and then find the best cluster with the highest average rating. This will help narrow down the locations during the location selection process.

The three important pieces of information for this project is the neighborhood, demographic, and reputation data. The neighborhood and demographic data can both be obtained by using BeautifulSoup to scrape the tables off of external sites. Then geocoder is used to find the latitude and longitude of the neighborhoods in NYC. Using these locations, Foursquare can be accessed to find nearby Chinese restaurants and the reputation for each restaurant. The reputation data can be obtained by using Foursquare’s venue detail endpoint. If neighborhoods or restaurants do not have certain data, they will be disregarded.

The three sources of the data are http://www.usa.com/rank/new-york-state--population-density--zip-code-rank.htm, https://www.health.ny.gov/statistics/cancer/registry/appendix/neighborhoods.htm, http://zipatlas.com/us/ny/zip-code-comparison/percentage-chinese-population.htm.


## Methodology
As mentioned in the data section, three types of data were needed: neighborhood, demographic, and reputation data. The first two could be retrieved from external sites using python requests. BeautifulSoup makes it easy to scrape a table off of websites. The final data is retrieved through Foursquare. 

The two Foursquare endpoints that were used were the venue search endpoint and the venue detail endpoint. For each neighborhood, the venue search endpoint was used to find up to 50 Chinese restaurants in the area. Ten of the 50 were randomly selected to explore in detail. This means that 10 venues in every neighborhood are evaluated. The mean of all 10 ratings and like-count are stored for each neighborhood. The variance is also stored because some neighborhoods may have fluctuating values.

K-means clustering was used to cluster the neighborhoods because the goal was to find neighborhoods that had the best venue data. By using clustering, the neighborhoods are grouped in a way such that the most similar neighborhoods are grouped. This clumps the better rated Chinese restaurant neighborhoods together. To find the best k value for K-means clustering, I used YellowBrick’s kelbow_visualizer. This clustering method is applied four times for four different lists of features. During each application, the Folium map is generated and a pivot table is created. The pivot works by grouping all rows with the same pivot value into a single dataframe row. All non-pivot entries will be calculated using the aggregate function. Our aggregate function is mean. With our pivot being the cluster label, we can see the average ratings and average like-count for each cluster label.


## Results
When you compare the four pivot tables against each other, it is obvious that the first pivot table contains the highest average rating and the highest average like-count. The values were 7.647857 and 308.7 respectively. The latter three pivot tables all produced a high average rating of approximately 7.3. We will use the data from the first pivot table.

![pivot table 1](../master/pivot_table.png)

Cluster 5 had an average rating of 7.647857. It is made up of Greenwich Village and SOHO and Lower Manhattan. Cluster 1 had the second-highest average rating of 7.53. The neighborhood in cluster 1 is Lower East Side. These two clusters all reside in Downtown Manhattan, which suggests that the best place to open a new Chinese Restaurant is in Downtown Manhattan.

Cluster 1 (Lower East Side) had the highest number of average likes with 308.7. Cluster 4 (Gramercy Park and Murray Hill) has the second-highest average number of likes with 284.8.


## Discussion
The Lower East Side has a relatively high Chinese population (about 18 percent of the population) and the highest average density compared to other clusters. It has the highest average number of likes and the second-highest average ratings. Since the Lower East Side is the only neighborhood in the top two for both the average rating and the average number of likes, it would be the best neighborhood for a new Chinese restaurant. As mentioned in the results section, choosing a restaurant in Downtown Manhattan would be a good choice because all the ratings were well above ratings in other areas of NYC.

One flaw of our method is that only ten Chinese restaurants were evaluated per neighborhood. If more premium calls were allowed on Foursquare, there would not have been that tight of a restriction. Having a larger dataset to calculate the average rating would call for a more accurate representation of neighborhoods. It would have also allowed for the clustering of zip codes instead of neighborhoods.


## Conclusion
Using K-means clustering, we were able to determine the neighborhoods with a high average rating and a high average like-count. The ideal Chinese restaurant location would be located in Downtown Manhattan. Downtown Manhattan is made up of many neighborhoods such as  Greenwich Village and SOHO, Lower Manhattan, Lower East Side, etc. We can conclude that the Lower East Side would be the best option out of the group. 
