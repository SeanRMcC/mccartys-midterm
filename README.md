# CS506 Midterm Writeup 

By Sean McCarty

---
## Features
 * NumExclamation & NumQuestion: The number of question marks and exclamation points in the Text column
 * TextPolarity & SummaryPolarity: Using sentiment analysis from the [TextBlob](https://textblob.readthedocs.io/en/dev/quickstart.html#sentiment-analysis) package, these features range from -1 to 1 where -1 is the most negative sentiment while 1 is the most positive sentiment. Used `TextBlob.sentiment.polarity`
 * TextSub & SummarySub: Using the aforementioned sentiment analysis package, these values ranged from 0 to 1 where 0 is the most object and 1 is the most subjective. Used `TextBlob.sentiment.subjectivity`
 * Helpfulness: Equal to HelpfulnessNumerator / HelpfulnessDenominator, which is the proportion of users who thought the review was helpful out of users who voted
 * TextLen: The number of words in the Text column
 * AvgMovieRating & AvgUserRating: These features are the average rating for a given ProductId the average of all ratings a UserId gave respectively. I calculated these using the training split only, and then applied these averages to both the local and kaggle test data, assigned a default average of 2.5 if the ProductId or UserId was not in the training data
 ---
 ## Observations 
 * Both polarity features seemed to correlate linearly with the number of stars, with 1 star reviews having a negative polarity & 5 star reviews having a high polarity
 * 
 ---
 ## Model

For my model I used the [HistGradientBoostingClassifier](https://scikit-learn.org/dev/modules/generated/sklearn.ensemble.HistGradientBoostingClassifier.html) from scikit-learn. This model is known for its performance, with my training time on 20% of the data being around 10 seconds, giving me the ability to iterate and test different features & parameters. Here is a breakdown of how the model works:
 * This is an ensemble model, meaning that it creates independent models that work together to vote on a classification
 * It employs gradient boosting to create an ensemble of decision trees
 * As a means to achieve performance, it turns the features into bins and constructs a histogram from those bins instead of dealing with the raw data

Out of all of the models I experimented with (KNN, Naive Bayes, SVM), this is the one that had the best accuracy while also being quick to train & predict on my Macbook Air.

---
 ## Results
My local accuracy was 