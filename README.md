Data used in the paper:
Aron Culotta, Nirmal Ravi Kumar, and Jennifer Cutler. ["Predicting Twitter User Demographics using Distant Supervision from Website Traffic Data"](http://tapilab.github.io/user%20attribute%20inference/2016/03/01/predicting/) *Journal of Artificial Intelligence*, 2016.

Please see the accompanying notebook for usage:
https://github.com/tapilab/jair-2016-demographics

- **brand2counts.pkl**: Map from a brand's Twitter ID to a dict in which the key is a Twitter account and the value is an int indicating how many followers of the brand also follow that Twitter account. E.g.
```python
>>> list(brand2counts.keys())[0]
15650816
>>> list(list(brand2counts.values())[0].items())[:10]
[(76611584, 2), (8519682, 1), (419168262, 2), (34668551, 1), (9633802, 2), (12, 20), (13, 15), (27394062, 1), (41298605, 7), (73269264, 2)]
```
This indicates that 2 of the followers of the brand with Twitter ID 15650816 also follow the Twitter account with ID 76611584.
- **brand_followers.csv**: A comma-separated file in the format <brand twitter handle>, <brand id>, [list of Twitter IDs of followers of this brand].
- **brands.json**: List of demographic information of each brand, as crawled from QuantCast.com. Also includes the Twitter handle for this brand.
- **fetch_tweets.py**: code to fetch the tweets of each ID in brand_followers.csv
- **follower_tweets.json.gz**: Most recent 200 tweets of each follower in brand_followers.csv
- **gender.txt**: Twitter users labeled with gender and with the list of accounts they follow, space separated.
- **geo-centric.user.time.tsv**: Data from Svitlana Volkova containing political affiliation of Twitter users.
- **geo-ids-fol.json**: For each user in `geo-centric.user.time.tsv`, the list of Twitter accounts that they follow.
- **get_follower_of_brands.py**: Script to print out the followers of each brand.
- **id2brand.pkl**: dict from twitter ID -> brand information dictionary. E.g.,
```python
>>> list(id2brand.items())[0]
(15650816, {'total': 5000, 'last_cur': 1471204691488271125, '_id': 15650816, 'max': 5000, 'brand_name': 'broadwayworld', 'is_processed': True, 'is_taken': False, 'demo': {'Female': '57%', 'Male 25-34': '10%', 'Male': '43%', '18-24': '12%', 'Other': '1%', 'Grad School': '20%', 'Female 45-54': '9%', 'Female 25-34': '13%', 'Caucasian': '73%', 'Male 35-44': '10%', '$50-100k': '29%', 'African American': '11%', '$100-150k': '14%', '45-54': '16%', 'Male 65+': '2%', '35-44': '22%', '65+': '4%', '55-64': '11%', '< 18': '13%', 'Female 35-44': '12%', 'No Kids': '65%', 'Hispanic': '10%', '$150k+': '10%', 'Female 55-64': '6%', 'College': '44%', '25-34': '23%', 'Male 18-24': '5%', 'Asian': '5%', 'brand': 'broadwayworld.com', 'No College': '36%', 'Female 65+': '2%', 'Male 55-64': '4%', 'Male 45-54': '7%', 'twitter': 'broadwayworld', 'Female 18-24': '7%', '$0-50k': '47%', 'Male < 18': '5%', 'Has Kids': '35%', 'Female < 18': '7%'}})
```
- **labeled_tweets.json.gz**: Most recent 200 tweets for each user in `gender.txt` and `race.txt`.
- **pol_text_data.pkl**: Most recent 200 tweets for each user in `geo-centric.user.time.tsv`
- **race.txt**:  Twitter users labeled with gender and with the list of accounts they follow, space separated.
- **race_text_data.pkl**: A cPickled version of a processed form of `labeled_tweets.json.gz`, containing a tuple (twitter_handles, csr_matrix), where twitter_handles is a list of N Twitter users from `race.txt`, and csr_matrix is a N x M sparse boolean matrix of text features, where 1 in position i, j indicates that user i has posted at least one tweet containing the term j.
- **results.pkl**: A cPickled version of all the experimental results. This contains the average correlation across all attributes, as well as the raw predictions for each demographic attribute. This is a list of the values returned by the `do_cv` function in the notebook.
- **sites.txt**: The original list of 1830 websites extracted from QuantCast.com
- **text_data.pkl**: A tuple of (text_vec, X_followers, follower_ids), where 
  - text_vec is a sklearn CountVectorizer
  - X_followers is a matrix where cell i,j indicates whether user i has tweeted term j
  - follower_ids is a list of the Twitter ids for each row (user) in X_followers.
- **twitter-creds.json**: Twitter tokens used by `fetch_tweets.py`. You'll have to enter your own credentials here if you want to run that script.
- **username2brand.pkl**: Like `id2brand.pkl`, but maps from Twitter username to the brand demographic information. E.g.
```python
>>> list(username2brand.items())[0]
('tomandlorenzo', {'total': 5000, 'last_cur': 1468581160936248801, '_id': 16190305, 'max': 5000, 'brand_name': 'tomandlorenzo', 'is_processed': True, 'is_taken': False, 'demo': {'Female': '80%', 'Male 25-34': '5%', 'Male': '20%', '18-24': '12%', 'Other': '2%', 'Grad School': '33%', 'Female 45-54': '10%', 'Female 25-34': '26%', 'Caucasian': '77%', 'Male 35-44': '5%', '$50-100k': '31%', 'African American': '8%', '$100-150k': '14%', '45-54': '13%', 'Male 65+': '1%', '35-44': '26%', '65+': '2%', '55-64': '7%', '< 18': '9%', 'Female 35-44': '21%', 'No Kids': '67%', 'Hispanic': '8%', '$150k+': '10%', 'Female 55-64': '5%', 'College': '47%', '25-34': '31%', 'Male 18-24': '2%', 'Asian': '5%', 'brand': 'tomandlorenzo.com', 'No College': '21%', 'Female 65+': '2%', 'Male 55-64': '2%', 'Male 45-54': '3%', 'twitter': 'tomandlorenzo', 'Female 18-24': '10%', '$0-50k': '44%', 'Male < 18': '2%', 'Has Kids': '33%', 'Female < 18': '7%'}})
```
