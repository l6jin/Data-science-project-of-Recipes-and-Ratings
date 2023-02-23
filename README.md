# Data-science-project-of-Recipes-and-Ratings
### Author: Luming (Selina) Jin and Jialing Li (Freya)

### Introduction
The two datasets contain recipes and ratings from the website food.com. We selected the subset of the raw data, containing only the recipes and reviews posted since 2018 because the original data is quite large. 

Our analysis is centered around the question: Could we interpret the Recieps' calories by their Ratings?

Our question tries to establish a connection between the calories and ratings of recipes. It is a significant and interesting question to analyze since it sheds light on how people value the recipes based on the amount of calories. If high-calories recipes are generally rated "bad", it may motivate the invention of more "healthy" recipes.  

Some general information about our datasets: "recipes" dataset contains 83782 rows  while "interaction" dataset has 731927 rows . We are interested in the column "rating" and "nutrition". "rating" column gives each recipe's rating by each unique user_id. "nutrition" column contains nutrition information in the form[calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for "percentage of daily value"], and our interested elem "calories" is in the column.


### Cleaning and EDA

#### Data Cleaning

We first loaded the two data sets and merged the two datasets to keep all the information from the recipes. We also calculated the average rating for each recipes. 

We noticed some of the ratings are 0 for no specifc reasons. Therefore, to make sure these rating wouldn't affect the overall rating of each dish, we replace them with NaN. 

In addition, we noticed the information in 'columns' 'steps', 'tags', 'ingredients', and 'nutrition' is not stored as a list. We turned the string to a list for each entry. 

In order to help answering our question, we added another column for calories derived from nutrition column. In addition, to help us better categorize different rating levels with the average rating, we added another column called rating_comment. The standard for the value assigned is illustrated below. 

If the average rating is larger or greater than 0 and smaller than 2, we categorize it as 'bad.' 

If the average rating is larger or greater than 2 and smaller than 3, we categorize it as 'ok.'

If the average rating is larger or greater than 3 and smaller than 4, we categorize it as 'good.'

The other higher average rating is categorized as 'excellent.'

This new column helps us organize the continuous average rating to different discrete level. This helps us better analyze our overall questions and make the data more readable. We also dropped the columns for 'tags','steps',and'ingredients' because they are not very related to our current exploring interest or question. 

Below is the first three rows of our cleaned data.: 

|    | name                                 |     id |   minutes |   contributor_id | submitted   | nutrition                                    |   n_steps | description                                                                                                                                                                                                                                                                                                                                                                          |   n_ingredients |   average_rating | rating_comment   |   calories |
|---:|:-------------------------------------|-------:|----------:|-----------------:|:------------|:---------------------------------------------|----------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|:-----------------|-----------:|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['38.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.']     |        10 | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!...                                                                                                              |               9 |                4 | excellent        |       38.4 |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['95.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.'] |        12 | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead....                                                                                                                                            |              11 |                5 | excellent        |       95.1 |
|  2 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['94.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.']    |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008... |               9 |                5 | excellent        |       94.8 |

#### Univariate Analysis
Below shows the distribution of average rating for the recipes. We can see the most of the recipes has an average rating around 5, which is aroudn 75 percent. Less recipes has an average rating around 1 and 2. 
<iframe src="assets/rating_distrbution.html" width=800 height=600 frameBorder=0></iframe>

Below shows the distribution of the steps each recipe take. We can see that it is skewed to the right. Most recipes would take 6 to 10 steps. Very few recipes can take up to 100 steps. 
<iframe src="assets/nsteps_distrbution.html" width=800 height=600 frameBorder=0></iframe>

#### Bivariate Analysis

Scatter plot between average rating and calories

The scatter plot shows how the amount of calories are distributed across the differet average ratings. The data are concentrated around the 0-1200 calories with few outliers. From the graph, we expect to see the calories are evenly distributed across the ratings. Maybe the recipes with "excellent" as their rating comment will have higher calories on average. But, in the following exploration, we find it is actually not!

<iframe src="assets/scatterplot.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/comment_univa.html" width=800 height=600 frameBorder=0></iframe>

Bar graph of Average Calories by Differnt Rating Comments

According to the graph, the mean calories of rating 'ok', 'good', and 'excellent' are about the same. However, the recipes with 'bad' rating comment has a greater amount of mean calories compared with other scales. This is an interesting pattern and we want to investigate it a little bit further.


<iframe src="assets/bargraph.html" width=800 height=600 frameBorder=0></iframe>

#### Interesting Aggregates

As we can see from the pivot table, recipes with 'bad' rating comment has higher average calories. The rest of the recipes have roughly the same amount of average calories. Therefore, we want to further investigate whether this is related to chance or there's a realtionship between calories and rating. 

| rating_comment   |    mean |   count |
|:-----------------|--------:|--------:|
| bad              | 69.23   |     610 |
| excellent        | 62.7267 |   78432 |
| good             | 65.0887 |    3940 |
| ok               | 65.1865 |     800 |

### Assessment of Missingness
#### NMAR Analysis

There are 70 missing entires in the 'description' column. We believe this is NMAR. The other columns so far do not tell us why the entry for 'description' is missing. Possible reasons might be that 'description' itself that are missing can be considered as too verbose to write down or it is too short/easy that people don't think it need to be written down. We could gather more data for n_steps or minutues. Maybe recipe with more steps or needs longer time would require a description that is verbose, which is related to the missingness. With more data, we might be able to explain the missingness. 

#### Missingness Dependency
There are 2609 missing average rating entries. We suspect that the missingness of rating may be related to the n_ingredients column and n_step column. 

##### Null Hypothesis: The missingness of rating is MCAR. 
##### Alternative Hypothesis: The missingness of rating is depend on the number of steps in the reciepes
<iframe src="assets/steps_dist.html" width=800 height=600 frameBorder=0></iframe>

From the distribution graph above, we can see the n-steps distibution by the missingenss of average rating. This shows that we need to use ks statistics for the permutation test. 

<iframe src="assets/ks_steps.html" width=800 height=600 frameBorder=0></iframe>

From the graph above and our p-value: around 0 from the permutation test, we should reject our null hypothesis. Therefore, we have evidence to say that the missingness of rating is depend on the number of steps in the reciepes.

We also suspect that the missingness of rating does not depend on the n_ingredients column. 

##### Null Hypothesis: The missingness of rating is MCAR. 
##### Alt Hypothesis: The missingness of rating is depend on the n_ingredients.

<iframe src="assets/ks_ingredients.html" width=800 height=600 frameBorder=0></iframe>

The graph above shows our empirical ditribution. From the distribution graph above, we can see the n-ingredients distibution by the missingenss of average rating. This shows that we need to use ks statistics for the permutation test. 


<iframe src="assets/fig_steps.html" width=800 height=600 frameBorder=0></iframe>

The graph above shows our empirical ditribution. From the graph above and the p-value: around 0.112, we fail to reject null hypothesis. Therefore, the missingess of rating is not depend on the n_ingredients columns


### Hypothesis Testing

#### Hypothesis Testing

##### Null Hypothesis: Calories and rating_comment is not related. The high calories we saw in entries that has 'bad' rating_comment is due to chance alone. 

##### Alternative Hypothesis: Calories and rating_comment are not related. The high calories we saw in entries that has 'bad' rating_comment is not due to chance alone.


We picked sample average of calories as our test statistics and significance level of 0.05. The resulting p-value is 0.12056 which is much larger than the significance level of 0.05. We failed to reject the null hypothesis and we concluded that the high average calories with "bad" rating comment is due to chance alone.


Our choice of null hypothesis is a good choice since it is a probability model that we can simulate under.
Our alternative hypothesis works well as a different viewpoint on how the recipe and rating data were generated compared with null hypothesis. Sample average is a reasonable choice of test statistics since calories is numerical. 0.05 is common cutoff for hypothesis testing and provides us significant level of confidence to reject the null hypothesis.


We also embeded the empirical distribution of sample mean of calories with "bad" rating comment 


<iframe src="assets/hypothesis_testing.html" width=800 height=600 frameBorder=0></iframe>


