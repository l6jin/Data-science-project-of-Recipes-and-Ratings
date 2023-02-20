# Data-science-project-of-Recipes-and-Ratings
### Introduction



### Cleaning and EDA

#### Data Cleaning

We first load the two data sets and merged the two datasets to keep all the information from the recipes.

We noticed some of the ratings are 0 for no specifc reasons. Therefore, to make sure these rating wouldn't affect the overall rating of each dish, we replace them with NaN. 

In addition, we noticed the information in columns steps, tags, ingredients, and nutrition is not stored as a list. We turned the string to a list for each entry. 

In order to help answering our questions, we add another column for calories derived from nutrition column. 

#### Univariate Analysis
Below shows the distribution of rating for the recipes. We can see the most of the recipes has a rating of 5, which is aroudn 77 percent. Less recipes has a rating of 1 and 2. 
<iframe src="assets/rating_distrbution.html" width=800 height=600 frameBorder=0></iframe>

Below shows the distribution of the steps each recipe take. We can see that it is skewed to the right. Most recipes would take 8 or 9 steps. Very few recipes can take up to 100 steps. 
<iframe src="assets/nsteps_distrbution.html" width=800 height=600 frameBorder=0></iframe>

#### Bivariate Analysis

Scatter plot between rating and calories
The scatter plot shows how the amount of calories are distributed across the ratings. The data are concentrated around the 0-1800 calories with few outliers. From the graph, we expect to see the calories are evenly distributed across the ratings. But, in the following exploration, we find it is actually not!

<iframe src="assets/scatterplot.html" width=800 height=600 frameBorder=0></iframe>


Bar graph of Average Calories by Rating
According to the graph, the mean calories of rating 2,3,4 is about the same. However, rating 1 has a greater amount of mean calories compared with other rating scales. This is an interesting pattern and we want to investigate it a little bit further.


<iframe src="assets/bargraph.html" width=800 height=600 frameBorder=0></iframe>

#### Interesting Aggregates
As we can see from the pivot table, recipes with rating of 1 has higher average calories. The rest of the recipes with rating of 1 to 4 have roughly the same amount of average calories. Therefore, we want to further investigate whether this is related to chance or there's a realtionship between calories and rating. 

### Assessment of Missingness
#### NMAR Analysis

There are 58 missing entires in the review column. We believe this is NMAR. Some people might not want to spend too much time to write a review for the recieps or some people has tried the recipe and rated it before. The other columns so far does not tell us why the entry for reivew is missing. We could gather more data for ratings. Maybe recipe with higher ratings are more popular and the chance of a person who doesn't like to leave a reivew when they rate the recieps is higher. 

#### Missingness Dependency
There are 15036 missing rating entries. We suspect that the missingness of rating is depend on the n_ingredients colums. The plot below shows our empirical distribution of test statistics. 

##### Null Hypothesis: The missingness of rating is MCAR. 
##### Alternative Hypothesis: The missingness of rating is depend on the number of steps in the reciepes

<iframe src="assets/fig_steps.html" width=800 height=600 frameBorder=0></iframe>

From the graph above and our p-value from the permutation test, we should reject our null hypothesis. Therefore, we have evidence to say that the missingness of rating is depend on the number of steps in the reciepes.

We also suspect that the missingness of rating does not depend on the minutes column. 

##### Null Hypothesis: The missingness of rating is MCAR. 
##### Alt Hypothesis: The missingness of rating is depend on the minutes

<iframe src="assets/fig_mins.html" width=800 height=600 frameBorder=0></iframe>

From the graph above and the p-value: around 0.114, we fail to reject null hypothesis. Therefore, the missingess of rating is not depend on the minutes columns


### Hypothesis Testing

#### Hypothesis Testing

##### Null Hypothesis: ratings and calories are not related - the high average calories in rating 1 is due to chance alone. In other words, if we picked 2870 ratings randomly from the population, it is reasonable to see an average that high.


##### Alternative Hypothesis: ratings and calories are related - the high average calories in rating 1 is not due to chance alone.


We picked sample average of calories as our test statistics and significance level of 0.05. The resulting p-value is 0.00017 which is much smaller than the significance level of 0.05. We rejected the null hypothesis and we conclude that the high average calories in rating 1 is not due to chance alone.


Our choice of null hypothesis is a good choice since it is a probability model that we can simulate under.
Our alternative hypothesis works well as a different viewpoint on how the recipe and rating data were generated compared with null hypothesis. Sample average is a reasonable choice of test statistics since calories is numerical. 0.05 is common cutoff for hypothesis testing and provides us significant level of confidence to reject the null hypothesis.


We also embeded the empirical distribution of sample mean of calories


<iframe src="assets/hypothesis_testing.html" width=800 height=600 frameBorder=0></iframe>


