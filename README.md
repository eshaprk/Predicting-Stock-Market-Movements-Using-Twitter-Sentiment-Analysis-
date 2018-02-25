# Predicting-Stock-Market-Movements-Using-Twitter-Sentiment-Analysis-

# Abstract

Twitter messages, or tweets, can provide an accurate reflection of public sentiment when taken in aggregation. In this paper, we investigate the relationship between Twitter feed content and stock market movement. Specifically, we wish to see if, and how well, sentiment information extracted from these feeds can be used to predict future shifts in prices. We accomplish this by mining tweets and stock price information, construct a model, estimate its accuracy and subsequently processing it for analysis. For the task of determining sentiment, we test the effectiveness of two machine learning techniques: Naive Bayes classification and Support Vector Machines. 

# Introduction

Today we live and breathe data. As people are free to say their opinions on anything using various social networking sites like Twitter, Facebook, Discussion forums, and blogs, particularly Microblogging and text messaging have emerged and become dominated tools over the web. Twitter messages (tweets) is often used to share opinions and sentiments about the surrounding world. The availability of social content generated on sites such as Twitter creates new opportunities to study public opinion about the entity. For analysis, we took twitter data for sentiment classification. The sentiment analysis is done on a per-Tweet basis. 
Forecasting the stock exchange data is an important financial subject which involves an assumption that the fundamental information publicly available in the past has some predictive relationships to the future stock returns. In the decision-making process, each piece of information is very important. This paper aims to combine the Twitter sentiment with the Stock prices using information from the Google Finance to predict movement in stock price. In this paper, both fundamental and technical data on a selected stock are collected from the Twitter API and Google Finance. 

# Approach

1.	System Outline
Figure 1 provides an overall outline of our system. The first step is to gather data from Google Finance and Twitter using web scraping and APIs. The stock data is then used to calculate the direction of stock by comparing with previous day’s closing price. The tweet messages are cleaned and a corpus is created. The score for each day’s tweets is computed by performing sentiment analysis. The data is combined and finally, our system can make predictions on stock behavior using the sentiment score.

 

2.	Data Collection
Tweets about specific companies are captured using keywords (e.g.  #Apple, @Apple, and Stock ticker $AAPL). We considered below companies for our work mainly due to  their popularity and there is a large amount of information online that is relevant to our research and can facilitate us in evaluating ambiguous sentiments collected from the tweets using Twitter API’s. All the companies are listed in NASDAQ or NYSE. We have collected roughly 450,000 tweets for our analysis.

The following is the list of companies:

Company Name	Tags used to collect data	Type of Industry
Amazon	$AMZN, @Amazon, #Amazon	E-Commerce
AMD	$AMD, @AMD, #AMD	Semiconductor
Apple	$AAPL, @Apple, #Apple	Technology
Bank of America	$BAC, @BankofAmerica, #BankofAmerica	Banking
Boeing	$BA, @Boeing, #Boeing	Aerospace
Deutsche Bank	$DB, @DeutscheBank, #DeutscheBank	Banking
Facebook	$FB, @Facebook, #Facebook	Social Networking
Google	$GOOGL, @Google, #Google	Technology
Microsoft	$MSFT, @Microsoft, #Microsoft	Technology
Starbucks	$SBUX, @Starbucks, #Starbucks	Coffee Shop
Tesla Motors	$TSLA, @TeslaMotors, #TeslaMotors	Automotive

We collected daily stock prices from 17th October 2016 to 13th December 2016 from Google Finance and Twitter respectively. This data set contains the open, high, low, close and adjusted close prices of stocks. We are focusing on close price of the stocks. The closing stock price is significant for several reasons. Investors, traders, financial institutions, regulators and other stakeholders use it as a reference point for determining performance. In fact, investors and other stakeholders base their decisions on closing stock prices. Institutional investors monitor a stock's closing price to make decisions regarding their investment portfolios


3.	Calculating Sentiment Score
Sentiment analysis, also called Opinion mining, is the field of study that analyzes people’s opinions, sentiments, evaluations, appraisals, and emotions towards entities such as products, services, organizations, individuals, issues, events, topics and their attributes. In order to compute sentiment score, we create a tweet corpus for each day, clean it and convert it into a document term matrix. These terms are then matched to our positive and negative words lexicon to calculate the count of each type of word in the document. The final score is computed as follows:
 
              To count the number of positive and negative words, we need a very important ingredient:
an opinion lexicon in English, which fortunately it is provided by Hu and Liu and it can be accessed from: http://www.cs.uic.edu/~liub/FBS/sentiment-analysis.html


4.	Algorithms Used
a)	Support vector machine

Support Vector Machines are one of the best binary classifiers. They create a decision boundary
such that most points in one category fall on one side of the boundary while most points in the
other category fall on the other side of the boundary. Consider an n-dimensional feature vector
x = (X1…., Xn). We can define a linear boundary (hyperplane) as
 
Then elements in one category will be such that the sum is greater than 0, while elements in the    another category will have the sum be less than 0. We can rewrite the hyperplane equation using inner products.
 
	
where * represents the inner product operator. Note that the inner product is weighted by its label.

The optimal hyperplane is such that we maximize the distance from the plane to any point. This is   known as the margin. The maximum margin hyperplane (MMH) best splits the data. The crucial element is that only the points closest to the boundary matter for hyperplane selection; all others are irrelevant. These points are known as the support vectors, and the hyperplane is known as a Support Vector Classifier (SVC) since it places each support vector in one class or the other.

 
As per, the Gaussian and Laplace RBF and Bessel kernels are general-purpose kernels used when there is no prior knowledge about the data. The linear kernel is useful when dealing with large sparse data vectors as is usually the case in text categorization. The polynomial kernel is popular in image processing, and the sigmoid kernel is mainly used as a proxy for neural networks. The splines and ANOVA RBF kernels typically perform well in regression problems.
b)	Naïve Bayes

Naive Bayes classifiers can handle an arbitrary number of independent variables whether continuous or categorical. A Naïve Bayes classifier tries to find the probability that A will happen given that B has already occurred, commonly denoted by P (A | B) (the probability of A given B). Bayes’ theorem can be used to make prediction based on prior knowledge and current evidence. With accumulating evidence, the prediction is changed. In technical terms, the prediction is the posterior probability that investigators are interested in. The prior knowledge is termed prior probability that reflects the most probable guess on the outcome without additional evidence. The current evidence is expressed as likelihood that reflects the probability of a predictor given a certain outcome. The training dataset is used to derive likelihood. Bayes’ theorem is formally expressed by the following equation.
P(A|B) = {P(B|A) ×P(A)}/ P(B)

5.	Creating Models and Evaluation
The dataset used for modeling contains the sentiment score for each day, and stock’s direction (UP/DOWN) based on the closing prices of the previous day. Our aim is to create a model which has the highest accuracy in terms of predicted values of the stock’s direction.

We have created a total of 4 models (SVM-3, NaïveBayes-1) and evaluated the accuracies for each model for all the 11 companies. We tuned the SVM models by trying different values of ‘cost’ and ‘gamma’ parameters, and finally evaluated the models accuracies based on the best ‘cost’ and ‘gamma’. The accuracies are calculated based on correct predictions made by the model.

A sample dataset (Amazon) is shown below:

Date	Score	ClosePrice	Direction
11/22/2016	0.401126	785.33	Up
11/23/2016	0.196673	780.12	Down
11/25/2016	0.249196	780.37	Up
11/28/2016	0.004318	766.77	Down
11/29/2016	0.038797	762.52	Down
11/30/2016	0.187265	750.57	Down
12/1/2016	0.006039	743.65	Down
12/2/2016	0.0625	740.34	Down
12/5/2016	0.213054	759.36	Up
12/6/2016	0.259168	764.72	Up
12/7/2016	0.535408	770.42	Up
12/8/2016	0.437118	767.33	Down
12/9/2016	0.315542	768.66	Up
12/12/2016	0.356316	760.12	Down
12/13/2016	0.292607	774.34	Up

The accuracy for each model is calculated by dividing the number of correct predictions by total number of predictions and multiplying it with 100 to get percent accuracy.

 


# Results

Below is the final table of accuracies for each model. The SVM models were tuned for best cost and gamma parameters before computing the accuracies.

Company Name	SVM-Linear	SVM-Radial	SVM-Sigmoid	Naïve Bayes
Amazon	56.09%	56.09%	58.53%	36.36%
AMD	47.55%	51.65%	49.36%	35.52%
Apple	51.23%	54.78%	52.61%	37.42%
Bank of America	42.12%	43.91%	42.65%	38.73%
Boeing	50.63%	53.85%	52.07%	40.64%
Deutsche Bank	39.37%	44.76%	40.54%	35.87%
Facebook	53.56%	56.17%	52.94%	41.07%
Google	52.13%	55.95%	51.83%	39.66%
Microsoft	49.47%	52.19%	50.26%	32.88%
Starbucks	38.67%	44.38%	40.74%	39.02%
Tesla Motors	50.93%	54.39%	51.46%	33.83%

Based on the above table, we infer that SVM classification with Radial kernel gives the highest accuracy for almost every company. We also conclude that our model can predict the direction of stock market (UP/DOWN) with an accuracy of near about 43% to 55%. Though these percentages are not very high but can be used to perform initial analysis. 

# Future Scope
As we noticed that our predictions are almost correct half of the times and we have used single predictor variable with limited data. We hope to improve these values if more data is utilized for training the models. Also, there are several factors which can also be considered such as stock volatility and momentum which if combined with twitter sentiment score will yield more accurate results.
