# Machine-Learning-Sentiment-analysis
Predicting Stock Market Fluctuations: A Sentiment Analysis Approach Utilizing Business Insider News Headlines and VIX Data to Determine Market Direction

Please go through the "questions" to understand what all I did in depth and "Solution" to understand what the output tells us.

Steps I performed:

Preprocessing and Corpus Creation: I started with preprocessing the raw text data from Business Insider. This is crucial to reduce noise and create a more digestible form for machine learning algorithms. I performed a variety of cleaning steps, including removal of numbers, lowercasing, removal of stopwords, and stemming. I then used the PlaintextCorpusReader to read this processed data into a corpus. Each document in this corpus corresponds to a different date in the dataset.

Creating the Document-Term Matrix (DTM): I created a DTM to convert the text data into a numerical format. The DTM is a sparse matrix (contains a lot of zeros), highlighting that each document uses only a small subset of the total vocabulary.

Creating a Frequency Matrix: I computed the column sums of the DTM to create a frequency matrix, which provides insights about word frequencies across the dataset. I then visualized this data with a bar plot to show words that occur more than 25 times.

Wordcloud Creation: I created a wordcloud of the 20 most frequent words to gain a more visual understanding of the typical headlines' subjects. The wordcloud served to highlight words that intuitively could influence stock market returns.

Defining Variables for Model: I defined the endogenous variable y_data as 'label' and the exogenous matrix x_data as the DTM. The goal here was to create an index that predicts the VIX's direction of change based on the words in the DTM.

Splitting the Data: I split the data into a training set that includes data up to and including 2016-12-31, and the remaining data was set aside for out-of-sample testing.

Fitting Regular Logistic Regression: I initially attempted to fit a regular logistic regression model using y_data and x_data with the training dataset. However, this didn't work due to the high dimensionality of the data and possible multicollinearity.

Running Ridge Logistic Regression: I then ran a ridge logistic regression with a cross-validation strategy. The ridge constraint helps manage multicollinearity and overfitting, thus providing a viable model (a coefficient vector) even with a high dimensional data set.

Interpreting Ridge Logistic Regression Results: Using the penalizing term chosen by cross-validation (.C_), I examined the chosen words and their associated coefficients. This helped me understand which words were important predictors in this model.

Creating a Sentiment Word List: I created a predefined sentiment word list and ran the ridge regression using this sentiment-focused DTM. I then compared the coefficients of these sentiment words with the previous results to understand the sentiment words' role in predicting VIX movements.

ROC Curves Creation: I created ROC curves for the sentiment model, using the penalizing term to obtain the coefficient vector. I used these curves to evaluate the model's predictive performance, comparing it to random chance.

Out-of-Sample Testing: Finally, I used the test sample and the sentiment model to assess the model's predictive performance on unseen data. I computed the proportion of days the model made correct predictions, comparing this rate to a 50/50 random chance.
