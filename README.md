# BT4222
Group Project for BT4222 -- Mining for Web data

## Problem Definition
Social Care is defined as the customer service provided via Social Media platforms. This is an increasingly popular platform for customers to engage a company and it is key that companies respond to enforce strong customer relationships. Through our research, we have identified that the airline industry is known for receiving overwhelming volume of queries - many of which can be answered with replybots. 
We explore the possibility of replying to some of these customer tweets by a replybot, as this would ease time taken to reply and the resources spent on maintaining customer relationships.

## Data Sources
**(1) Customer Support on Twitter -- Kaggle Dataset** <br/>
The Customer Support on Twitter dataset from Kaggle is a large, modern corpus of tweets and replies to aid innovation in natural language understanding and conversational models, and for study of modern customer support practices and impact. The dataset consists of a CSV file with more than 280,000 observations where each row represents a tweet. Every conversation included has at least one request from a consumer and at least one response from a company. (cr: https://www.kaggle.com/thoughtvector/customer-support-on-twitter/data) 
This dataset will act as both our training and validation sets. The raw dataset is also available inside the Data folder, titled as "fromkaggle.csv". 

_Labelling the dataset_ <br/>
As our use case dictates the presence of the "Answerable" label which does not exist in the original dataset, we had to devise a labelling algorithm to do the labelling of the dataset. The labelling algorithm will look at the company replies to a particular tweet, and tweets that have no company responses would be filtered out of the dataset. Based on the content of the company response, we will label a customer tweet as 1 if the company response contains certain keywords such as, “DM (direct message)” and “Send us”. Additionally, tweets with company responses that contain keywords indicating clear instructions from the company such as "email information", are treated as answerable and labelled with 1. The labelling algorithm can be found in the Modelling folder, titled "labelling_final.ipynb". 

**(2) Tweets to Budget Airline firms -- Twitter Dataset** <br/>
Using Tweepy and the Twitter API, we collected only English tweets that have been directed at any one of the 5 budget airlines, and the structure of the data is shaped to be similar to the Kaggle dataset for ease of usage. With a standard Twitter developer account, we are allowed to only collect tweets from the past week at the point of crawling, and we collected a dataset amounting to more than 7000 tweets from customers directed at any of the 5 budget airlines. Additionally, the company which the tweet was directed at was labelled under the "customer_of" column for this dataset. This dataset is also available in the Data folder, titled as "cust_tweets.csv". This dataset is used purely as a test dataset, to explore how relevant our proposed solution is in a real-world setting.


## Models
There are two main parts to our project, the first of which deals with classifying whether a certain tweet is answerable by a reply bot of not. The second part deals with categorising the answerable tweets in an effort to assist the companies in generating responses to these answerable tweets. 

**(1) Model 1 -- Classification model to determine Answerability of tweets** <br/>
An initial exploration phase showed that the logistic regression classifier was the best-performing algorithm among the other explored algorithms. The chosen model (model1.ipynb) is a logisitic regression classifier, and can be found inside the Modelling folder, together with the other models explored during the initial exploration phase. The logReg classifier uses the L1 Regularization to penalise heavily on words that are comparatively less important, which is important in our case where feature dimensionality is high.

**(2) Model 2 -- Multi-class Classification model to categorise tweets** <br/> 
Customer tweets are clustered using K-means to form K clusters based on the content of the company responses to the tweet. This clustering algorithm will be repeated on the Twitter dataset, which will generate the K clusters (or categories in our case), and the most frequent words for each case. These words would be used for determining which tweet falls into which category, and can therefore aid the company in determining a suitable response for every tweet from each of the categories.


## File Position Specification
**./Data** <br/> 
The Data folder includes all the data files we used in our modelling. 
- The **fromkaggle.csv** <br/> is the original kaggle dataset.
- The **kaggle_labeled.csv** <br/> is the balanced training kaggle customer tweets after we preprocessed the labelling
- The **kaggle_inter.csv** <br/> is an intermediate dataset we used for generating the second model
- The **cust_tweets.csv** <br/> is an the twitter data we crawled ourselves
