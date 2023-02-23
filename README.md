# Data-science-project-of-Recipes-and-Ratings
### Introduction



### Cleaning and EDA

#### Data Cleaning

We first load the two data sets and merged the two datasets to keep all the information from the recipes. We also calculated the average rating for each recipes. 

We noticed some of the ratings are 0 for no specifc reasons. Therefore, to make sure these rating wouldn't affect the overall rating of each dish, we replace them with NaN. 

In addition, we noticed the information in columns steps, tags, ingredients, and nutrition is not stored as a list. We turned the string to a list for each entry. 

In order to help answering our questions, we add another column for calories derived from nutrition column. In addition, to help us better categorize different rating levels with the average rating, we added another column called rating_comment. The standard for the value assigned is illustrated below. 

If the average rating is larger or greater than 0 and smaller than 2, we categorize it as 'bad.' 
If the average rating is larger or greater than 2 and smaller than 3, we categorize it as 'ok.'
If the average rating is larger or greater than 3 and smaller than 4, we categorize it as 'good.'
The other higher average rating is categorized as 'excellent.'
This new columns helps us organized the continuous average rating to different discrete level. This helps us better analyze our overall questions and make the data more readable. 

|    | name                                 |     id |   minutes |   contributor_id | submitted   | tags                                                                                                                                                                                                                        | nutrition                                    |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | description                                                                      | ingredients                                                                                                                                                                    |   n_ingredients |   average_rating | rating_comment   |   calories | rating_missing   |
|---:|:-------------------------------------|-------:|----------:|-----------------:|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|----------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|:-----------------|-----------:|:-----------------|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] | ['38.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.']     |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                  | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies th | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 |                4 | excellent        |       38.4 | False            |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               | ['95.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.'] |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !'] | this is the recipe that we use at my school cafeteria for chocolate chip cookies | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 |                5 | excellent        |       95.1 | False            |
|  2 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | ['94.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.']    |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                              | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i d | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |                5 | excellent        |       94.8 | False            |


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
According to the graph, the mean calories of rating 'ok','good',and 'excellent' are about the same. However, the recipes with'bad' rating comment has a greater amount of mean calories compared with other scales. This is an interesting pattern and we want to investigate it a little bit further.


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


