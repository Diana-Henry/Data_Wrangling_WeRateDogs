# Introduction:
> wrangle WeRateDogs Twitter data to create interesting and trustworthy analyses and visualizations.
# # Part one: Data Wrangling:
### Install

This project requires **Python** and the following Python libraries installed:

- [Tweepy](https://tweepy.readthedocs.io/en/v3.5.0/)
- [Requests](https://www.pythonforbeginners.com/requests/using-requests-in-python)
- [json](https://docs.python.org/2/library/json.html)
- [io](https://docs.python.org/2/library/io.html)
- [bs4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [os](https://docs.python.org/2/library/os.html)
- [time](https://docs.python.org/2/library/time.html)
- [re](https://docs.python.org/3/library/re.html)
- [NumPy](http://www.numpy.org/)
- [Pandas](http://pandas.pydata.org)
- [matplotlib](http://matplotlib.org/)
You will also need to have software installed to run and execute a [Jupyter Notebook](http://ipython.org/notebook.html)

## a-  Gathering Data:
- `First`: Gathering data from "twitter-archive-enhanced.csv" which is download manually.
- `Second`: Gathering data from "image_predictions.tsv" that will be downloaded programmatically using the Requests library.
- `Third`: Gathering data from query the Twitter API for each tweet's JSON data using Python's Tweepy library and store each tweet's entire set of JSON data in a file called "tweet_json.txt" file.


## b- Assessing Data: 
After gathering each of the above pieces of data, assess them visually and programmatically for quality and tidiness issues was our next step.
We could detect and document the following quality issues and tidiness issues.

#### Quality issues:
##### `twitter_archive` table:
- tweet_id is int instead of being a string.
- Each of( in_reply_to_status_id , and in_reply_to_user_id, retweeted_status_id,in_reply_to_status_id) is float not a string.
- "in_reply_to_status_id" and "in_reply_to_user_id" have only 78 non null values.
- "retweeted_status_id" and "retweeted_status_user_id" have only 181 non null values.
- Nulls represented as 'None' in each of doggo,floofer,pupper, and puppo.
- doggos has 2259 value equal to 'None'.
- floofer has 2346 value equal to 'None'.
- pupper has 2099 value equal to 'None'.
- puppo has 2326 value equal to 'None'.
- expanded_url column has 59 missing values. 
- Nulls represented as 'None' in name column.
- lowercase names have unsuitable data like (all, the , a , an , by , old, not, his, this..... )
- Capitalize the rest of lowercase.
- name ='O' has to be replaced with Nan.
- some of rating_numerators and rating_denominators values are incorrect.
- rating_numerators and rating_denominators is int instead of float.
- timestamp is object instead of being datetime type.

##### `image_prediction` table:
- tweet_id is int not a string.
- jpg_url column has duplicated photos (66 row are duplicated) have to be removed
- it includes 2074 row, there are some missing rows comparing to  `twitter_archive` rows'counts(2356 row).
- rows with p1_dog, p2_dog and p3_dog with False value should be removed

##### `tweet_data` table:
- id is int not a string.
- the 'id' column should be renamed to "tweet_id" to match the other 2 tables.
- it includes 2331 row, there are missing rows comparing to  `twitter_archive` rows'counts (2356 row).

#### Tidiness 
##### `twitter_archive` table:
- Combine (Doggo, floofer, pupper, puppo) in one column named dog_type.
- Dropping uneeded columuns ( in_reply_to_status_id' , 'in_reply_to_user_id','retweeted_status_id','retweeted_status_user_id','expanded_urls','source')
- Combine rating_numerator and rating_denominator one column in twitter_archive_clean.

##### `image_prediction` table:
- The first True prediction for all image will be saved to new column (dog_type)with its confidence in another column named (confidence_degree).
- Dropping uneeded columns.
- Combine `image_prediction` with `twitter_archive` using tweet_id.

##### `tweets_data` table:
- Combine `tweets_data` with `twitter_archive` using tweet_id.

## c-  Cleaning Data:
- making a copy of the datasets.
- Using the two types of cleaning, the manual and programmatic.

# Part 2 : Data Visualization:
## Insights:
> 1- The most  and the least favorite dog stage according to the dataset.
> 2- The top 10 favorite dog type for according to the dataset.
> 3- The least 10 favorite dog type for according to the dataset.
> 4- The Top 10 favorite count in total according to the dog type.
> 5- The Top 10 retweet count in total according to the dog type.
> 6- The Top 10 retweet count in average according to the dog type.
> 7- The Top 10 favorite count in average according to the dog type.
> 8- The Top 10 rate in average according to the dog type.
> 9- The least 10 rate in average according to the dog type.
> 11- Calculate different statistic for dog_stage according to rate.
 
 ## Insight Summary:
 ##### We can notice the following:
- Floofer has the highest rate in average (sure it affected by count of floofer (`7`).
- Doggo has the minimum rate in average ( equal to `5`).
- Each of Doggo, Pupper, and Puppo has maximum rate in average equal to  `14`.
- 75% of Doggo, Floofer, and Puppo has rate in average equal to `13`.
- 50% of Doggo, Floofer, and Puppo has rate in average equal to `12`.
- 25% of Doggo, Floofer, and Puppo has rate in average equal to `11`.

# Visualization:
> Research Question 1: What is the type of correlation between favorite_count And retweet_count? 
> Research Question 2:  What is the distribution of dogs_stage? 
> Research Question 3:  Is there a relation between rate and tweet count? 
> Research Question 4: Is there a relation between rate and favorite count? 

# Conclusions:
- The highest rating doesn't receive the most favorite count or retweet count.
- There is strong relation between favorite count and retweet count. The one increased the othher increased too.

- Pupper has the highest frequent `(179)` and floofer has the lowest `(7)`.

- Japanese_spaniel takes the lowest rate in average = `5/10`.
- Bouvier_des_Flandres takes the highest rate in average = `13/10`. 

- Bedlington_terrier takes the highest favorite_count in average= `22731.5`.
- Bedlington_terrier takes the highest retweet_count in average = `7165`

- golden_retriever takes the highest retweet_count in total = `508771`.
- golden_retriever takes the highest favorite_count in total = `1769933`.

- the most favorite dog type is the golden_retriever with count `175`.




