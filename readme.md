# Background
Reddit is an American social news aggregation, web content rating, and discussion website. Registered members submit content to the site such as links, text posts, and images, which are then voted up or down by other members. Posts are organized by subject into user-created boards called "subreddits", which cover a variety of topics such as news, politics, science, movies, video games, music, books, sports, fitness, cooking, pets, and image-sharing. Submissions with more up-votes appear towards the top of their subreddit and, if they receive enough up-votes, ultimately on the site's front page. Despite strict rules prohibiting harassment, Reddit's administrators spend considerable resources on moderating the site.

The S&P 500, or simply the S&P,is a stock market index that measures the stock performance of 500 large companies listed on stock exchanges in the United States. It is one of the most commonly followed equity indices. The S&P 500 index is a capitalization-weighted index and the 10 largest companies in the index account for 27.5% of the market capitalization of the index. The 10 largest companies in the index, in order of weighting, are Apple Inc., Microsoft, Amazon.com, Facebook, Tesla, Inc., Alphabet Inc. (class A & C), Berkshire Hathaway, Johnson & Johnson, and JPMorgan Chase & Co., respectively. 

In this study, post from subreddit will be scraped to find the correlation against S&P 500. Posts from the following investment related subreddit were being examined:
- (1) r/wallstreetbets
- (2) r/securityanalysis
- (3) r/investing 
- (4) r/stockmarket
- (5) r/technicalanalysis 

While there are other subreddits that have topics of investing within it, the primary consideration was that it should be established and has high traffic.


# Analysis and Predictive Modeling

This project aimed to predict whether if the S&P 500 will be Bullish or Bearish from a particular post from reddit through their sentiment. A classification model will be devised and evaluated based on accuracy score. This helps potential investor better understand if the stock market performance can be analysed based on sentiments of the general public or not.

After thorough data cleaning and exploratory analysis, we ran 2 different vectorizers (cvec & tvec) along with 4 different models using Logistic Regression, Multinomial NB, Random Forest and AdaBoost. For model evaluation, we recorded train and test scores, ROC-AUC scores, specificity, sensitivity and F1 scores for each of the models. Based on the accuracy score, the Multinomial NB model with tvec has the best accuracy. However, it is only doing slightly better than the benchmark due to the high similarity between the two classes of up and down trend.

**Daily Title dataset**<br>
In this dataset, the title was combined on a daily basis for 2019 and 2020. There are about 500+ data which corresponds to the number of trading days in 2019 and 2020. While there are no null or duplicate values based on the huge dataset being pivoted to on a daily basis. There is still the presence of common words in both target variables. 

**Title + Post in 2019 Dataset**<br>
In this dataset, the title was combined on a daily basis. Started out with 500,000 posts spanning across 2019 and 2020., the dataset was sliced to 2019 which contains approx 60,00 posts. The post was further reduced to approx 27,00 posts that were captured based on trading days. While there are no null or duplicate values based on the huge dataset being pivoted to on a daily basis. There are still the presence of common words in both target variables. 

**Exploratory Data Analysis**<br>
In the Exploratory Data Analysis phase, the following were examined:
- Comparing number of post in terms of years, months, month_year
- Significant changes during certain period of the year
- Top uni-/bi-/tri-grams of the dataset

Comparing 2019 and 2020, the most prominent explanation would be due to Covid. As Covid surged the number of posts when comparing year-on-year and there was a huge market correction in Mar 2020. This cost a mixed reaction by the investors as two groups of investor's appear which results in buying and selling regardless of the performance of the S&P 500. This is possible due to some seeing it as an opportunity to buy stocks at a lower price while some fear a potential market crash hence panic sell occured. 

Overall, the EDA process is a very good indicator that there will be a huge challenge in producing a good model due to the huge similarity in the features against two different classifiers. There are also additional insights to consider to be part of the feature like comparing the number of posts during a certain period of time to better classify between up and down trends.

In Sentiment Analysis, both dailytitle and titlepost dataset shows that even the most positive or negative sentiment, contains posts that were either in the up or down trend in either sentiments. This is also possibily due to having neutrality within some of the posts. 

Number of posts by year shows a high surge from one year to another. This was due to the pandemic(corona/Covid-19) faced in 2020 which caused a lot of uncertainty within the stock market and worries among the investors. Comparing year-on-year, keywords like Covid, Corona, Correction, Market Crash, appeared more in 2020 as compared with 2019. Generally, in 2019, the number of posts was less than 10,000 per month as there was nothing significant occuring during that year. However, in 2020, the number of posts surged throughout the months. Especially in Mar 2020, where there was a huge market correction which got many investors concerned. Hence, the huge spike in the number of posts.

Comparing the number of posts, it seems to indicate that in an event of a significant change in the market, the number of posts for that month will significantly increase also. Most dates shows that there was a huge change in the period of Mar 2020. Hence, top 30 changes during the period of 2019 and 2020 are mainly due to performance of the stock market in Mar 2020.

In the following EDA, the top 50 uni-gram/bi-gram/trigram were reflected with emphasis to two stages; (1) Before increasing the stopwords and (2) After increasing the stopwords.Before cleaning, there are a huge amount of similar words between the Up and down trends. Despite cleaning, there still remains a huge amount of similar words between the Up and down trends. 


# Model Limitations

As shown during the EDA process, there are too many common words between the up and down class regardless if it is within the uni-gram, bi-gram or tri-gram. Additionally using NLTK Vader, the returns of the results indicate that despite being in either the positive or negative sentiment, there will still be a mixture of up and down trends to either of the sentiment.

# Conclusion
As the sentiment is a balanced mix regardless of a bearish or bullish trend in the S&P 500, the reddit community cannot determine whether S&P 500 will be going up or down. There will always be people buying and selling whenever it is a trading day. 


# Data Dictionary
| Column          | Type     | Origin                                         | Description                             |
|-----------------|----------|------------------------------------------------|-----------------------------------------|
| Date            | datetime | project_df_dailytitle_cleaned.csv              |  Date of Post                           |
| combined_title      | object | project_df_dailytitle_cleaned.csv | Title combined on daily basis |
| percent_change_class | object | project_df_dailytitle_cleaned.csv | Target variable for up and down trend |
| title_len | int | project_df_dailytitle_cleaned.csv | Length of the cleaned_title |
| title_cleaned |object | project_df_dailytitle_cleaned.csv | combined_title which has been preprocessed |
| date | datetime | project_titlepost2019_df_cleaned.csv | date of post |
| title | object | project_titlepost2019_df_cleaned.csv | title of post |
| selftext | object | project_titlepost2019_df_cleaned.csv | body of post |
| month | datetime | project_titlepost2019_df_cleaned.csv | month of the post |
| year | datetime | project_titlepost2019_df_cleaned.csv | year of post |
| year_and_month | object | project_titlepost2019_df_cleaned.csv | month of a particular year |
| week_of_year | object | project_titlepost2019_df_cleaned.csv | week of the year |
| precentage_change_class | object | project_titlepost2019_df_cleaned.csv | Target variable for up and down trend |
| title_len | int | project_titlepost2019_df_cleaned.csv | Length of the title of post |
| text_len | int | project_titlepost2019_df_cleaned.csv | Length of the body of post |
| first_title_cleaned | object |  project_titlepost2019_df_cleaned.csv | Initial preprocessing of title of post |
| first_selftext_cleaned | object | project_titlepost2019_df_cleaned.csv | Initial preprocessing of body of post |
| final_title_cleaned | object |  project_titlepost2019_df_cleaned.csv | Updated preprocessing of title of post |
| final_selftext_cleaned | object | project_titlepost2019_df_cleaned.csv | Updated preprocessing of body of post |
| fresh_meat | object | project_titlepost2019_df_cleaned.csv | Combination of first_title_cleaned & first_selftext_cleaned|
| lean_meat | object | project_titlepost2019_df_cleaned.csv | Combination of final_title_cleaned & final_selftext_cleaned|
| lean_meat_len | int | project_titlepost2019_df_cleaned.csv | Length of the lean_meat |
