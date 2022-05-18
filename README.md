# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: NLP & Classification

# Problem Statement
**Brandeis University's science department is planning to build an online forum for students and faculties to freely exchange  scientific questions of their interests:**

This project seeks to find a strategy to filter out 'troll' forum posts, that are scientifically irrelevant. By utilizing natural language processing and classification models on two different subreddits, 'AskScience' and 'ShittyAskScience', the project will explore the differences in the texts of troll and legitimate scientific questions and try to classify between them. 

# Background
Reddit is an online platform where the users freely exchange social news, rate web contents, and hold discussions on different topics ([*source*](https://en.wikipedia.org/wiki/Reddit)). The site's content is divided into categories or communities known as "subreddits"; there are more than 138,000 communities that are actively being used. 

For the purpose of this project, submissions in the following two subreddits will be utilized:

1. [**Ask Science Subreddit:**](https://www.reddit.com/r/askscience/)
This subreddit is one of the most utilized communities with 22.5M members. The community is encourage to ask science-related questions, and users can expect to get real scientific answers. 

2. [**Shitty Ask Science Subreddit:**](https://www.reddit.com/r/shittyaskscience/)
This subreddit is meant to be a fun community where users post "scientific sounding" quandaries that does not actually scientifically makes sense. 1M members have joined the community since 2011. The users    

# Data 

#### Dataset Collection from Reddit:

1. A Reddit PushShift API will was used to scrape 5,000 text submissions from each subreddit.
    * [askscience.csv](../data/askscience.csv)
    * [shittyaskscience.csv](../data/shittyaskscience.csv)

2. The two individually collected dataframe was concatenated together to build classification model.
    * [data_final.csv](../data/data_final.csv)
    
# Analysis
**interpretations:**
- **accuracy:** percentage of correct subreddit classification
- **Sensitivity(Recall):** Among the actual ShittyAskScience submissions, how many(or proportion) did I predict correctly
- **Specificity(True negative rate):** Among the actual AskScience submissions, how many(or proportion) did I predict correctly
- **Precision(Positive predictive value):** Among the posts I predicted as ShittyAskScience, how many did I get correct?

Comparing across the four different models, the model with the most accuracy was random forest with 72.6% accuracy. However, the multinomial naive bayes model had comparable accuracy of 72% despite the fact that it was only using bag of words features. 

This may be because the additive features including text length, sentiment score, complexity that were used in latter three models(RF, logistic regression, and KNN classifier) were not too distinctively different between the two subreddits. 

Putting into Context of the problem, we may want to aim for higher recall than specificity in order to enhance the integrity of the forum; if we classify a post falsely as a troll question when it actually is a legitimate question, we can implement a back up review method to re-examine the pool of troll posts so that none of the legitimate posts get left behind. According to this logic, KNNClassifier would win the competition; however, this leaves a huge pool(~60%) of legitimate scientific posts in the pull of troll post, requiring a more expensive reexamination process. 

On the other hand, aiming for highger specificity hence possibly a lower sensitivity may lead us to let the troll posts to be submitted. If we choose to stick with Random Forest classifier with highest specificity  of 80% and sensitivity of 65%, we let 35% of troll posts leaking into the forum. This may be a less expensive method in human workload, as the forum managers will likely rely on the user report of the troll posts, possibly reducing the second filtering workload of re-examining the posts classified as a troll. 



# Conclusions
This project seeks to build a reliable model to filter out 'troll' forum posts, that are scientifically irrelavent by referring to the posts uploaded on Reddit. By utilizing natural language processing and classification models on two different subreddits, 'AskScience' and 'ShittyAskScience', the project aimed to explore the differences in the texts of troll and legitimate scientific questions and try to classify between them. 

Overall, the metrics of 4 different models showed that the accuracy of any models did no better than 72%(rf, mnb). Highest sensitivity and specificity were at 82%(knn) and 80%(rf) respectively, but this would lower the complimentary specificity and sensitivity scores. 

Choosing amongst the four models, MultinomialNB would be the best bet with the highest accuracy and f1 score, which indicates that there is the best balance between the sensitivity and specificity.  

One enhancement that I can make is actually accessing the text body of the submissions, which was not available with the shortcoming of Pushshift API. Also, I might need to do a more thorough datacleaning/preprocessing steps to filter out the posts that are completely out of context (such as ads) to make the model much more thorough. 