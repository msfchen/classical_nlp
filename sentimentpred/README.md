# Sentiment Prediction with Naive Bayes Classifier

- Goal: to predict positive/negative sentiment of the given text
- Approach: Approach: Naive Bayes Classifier

  - Data Processing:
    - load postive and negative tweets; split each into train and test; combine train and test to contain equal number of positive and negative
    - remove stopwords, stock tickers, retweet symbols, hyperlinks, hashtags, punctuations; apply stemming
    - build a dict freqs = { (stemmed word, label): frequency }
    
  - Training: 
    - def train_naive_bayes(freqs, train_x, train_y) returns logprior, loglikelihood
      - logprior = np.log(D_pos) - np.log(D_neg) = 0 in this study
      - loglikelihood = { word : np.log(p_w_pos/p_w_neg) } 

  - Testing:
    - def naive_bayes_predict(tweet, logprior, loglikelihood) returns p
      - p = logprior + all the logliklihoods of each word in the tweet (if found in the dictionary)
      - Note: p > 0 means positive, else negative
      
    - def test_naive_bayes(test_x, test_y, logprior, loglikelihood) returns accuracy

  - Filter words by Ratio of positive to negative counts
    - We can calculate the ratio of positive to negative frequencies of a word.
    - We can then filter a subset of words that have a minimum ratio of positivity / negativity or higher.
    
