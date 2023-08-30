# Sentiment analysis applied at Airbnb reviews

**1 Introduction**

Natural language processing (NLP) is a theory-motivated range of computational techniques for the automatic analysis and representa-tion of human language.” Cambria (2014).
In other words, NLP is a way that machines and computers under-stand our language. In this context, the project will explore a case study about Text Mining which nowadays is a very powerful technique to evaluate large collections of documents and discover new infor-mation and answer questions. Considering the amount of information present on the World Wide Web. However, the most of this text data is produced for human consumption, leading to unstructured data which requires pre-processing techniques to make the data understandable to the machines.
In the scope of this project, sentiment analysis was done, which it is the process used to determine the emotional tone for of a piece of text. This analysis It is an important tool for businesses in order to understand customer feedback, social media sentiment, and brand reputation due to their sentiment analysis has several diverse applications in the real world.
Intended to make this the sentiment analysis, we used the NLTK (Natural Language Toolkit) for that. It consists of a package from Python which provides a wide range of libraries for text analysis, furthermore, it is widely used, well-documented and has a large community of users and contributors. NLTK includes pre-trained models for sentiment analysis, which was used to classify the sentiment of Airbnb reviews (a piece of text) as positive, negative, or neutral.
The data used was collected from insideairbnb.com which is a project that provides data about Airbnb services along the world. Within the data available on the site, we chose to analyze the data concerning the guest reviews and the data about the accommodation’s characteristics.
The goal of this project is to demonstrate with real data the challenges of transforming a business problem into a data problem, through a huge quantity of data available from guest reviews for Airbnb accommodations at the Boston City between 2015 and 2023.
Leading to how text mining and sentiment analysis can be used to extract insights from a large volume of unstructured data, and how it can help businesses make data-driven decisions that improve customer satisfaction.

**2 Background and problem description**

The tourism industry has always been heavily connected to customer satisfaction. With the rise of online platforms such as Airbnb, the volume of guest reviews has increased exponentially. Considering that manually analyzing this vast amount of data can be time-consum-ing and error prone, there is a growing need for automated tools and techniques that allow the extraction of valuable insights from this data.
Sentiment analysis is a powerful tool for analyzing customer feed-back and sentiment in the tourism industry, using NLP and machine learning techniques, sentiment analysis can automatically classify guest reviews as positive, negative, or neutral, and extract valuable in-sights into customer satisfaction and preferences. We will then use the insights gained from the sentiment analysis to identify trends, patterns, and opportunities, which can be valuable for improving customer sat-isfaction.

**2.1 Data pre-processing**

Firstly, we started by deleting any unnecessary columns from both datasets, the review dataset and the listings dataset. We also decided that we should consider only reviews with the length higher than 30 characters because for the sentiment analysis longer reviews are more useful than shorter ones.
Considering that the data is real and there are reviews from several languages, in order to simplify the computational effort and reduce the noise in data, we decided to consider only reviews in English. The function langdetect from detect package was used to detect the lan-guage from each review. Firstly, the DataFrame available at http://insideairbnb.com/ has 162.916 rows and after dropping the unused rows the DataFrame has 144.969 rows, which is a huge number of reviews to analyze.
We used the NLTK library to manipulate the data in order to tokenize, remove the stop words and count the frequency of each word on each review, with the functions word_tokenize, FreqDist, stop-words. Finished the Data pre-processing, we perform the sentiment analysis using the nltk.sentiment.vader.SentimentIntensityAnalyzer, it is a pre-trained model for sentiment analysis in English text being part of the VADER (Valence Aware Dictionary and sentiment Reasoner) module from NLTK library.
The VADER Sentiment Analyzer is designed for sentiment analysis in social media context, where traditional sentiment analysis models may struggle because of the informal language used. VADER is trained on a vast amount of social media data and uses a combination of lexical and grammatical heuristics to estimate the sentiment intensity of a given text. (Keita,2022)
For the following analysis, we consider the compound score given by polarity_scores() method, which represents an aggregated senti-ment intensity ranging from -1 (extremely negative) to 1 (extremely positive). To have a better view of the result, a histogram and a boxplot were made. 
    
    ![image](https://github.com/GuiSilvaPereira/Sentiment-analysis-applied-at-Airbnb-reviews/assets/133000426/5e69c274-e526-474e-8c09-a870c3f127f8)
    ![image](https://github.com/GuiSilvaPereira/Sentiment-analysis-applied-at-Airbnb-reviews/assets/133000426/bfeb3d9d-cbd4-4452-bfdc-06676cde501c)

The figures showed that the mean of the compound from we can see that from the reviews tend to be positive, which is good information for Airbnb, but it creates some difficulties in our analysis, more specifically how can we detect the similar sentiment scores once it has a very low variance and tends to be very positive. To avoid this similarity between the "compound" of the reviews, we decided to discretize the “compound” value, creating a new column named “sentiment_class” using the qcut function from Pandas library. The function computes the quantiles based on the distribution of the data, then splits the data in the number of bins defined where each bin will have approximately the same number of observations.The distribution after implementation, can be seen in next figure.
    
    ![image](https://github.com/GuiSilvaPereira/Sentiment-analysis-applied-at-Airbnb-reviews/assets/133000426/2e032d19-ada5-476e-ab05-29a5bd51356c)

