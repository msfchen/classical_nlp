# Auto-Complete with N-gram Language Model

- Goal: to suggest the most likely next word and show its probability for the given previous N words
- Approach: N-gram Language Model (P(w_t|w_t-n, ..., w_t-1))

  - Data Preprocessing: 
    - load twitter data; split into sentences; tokenize sentences (lists of words); randomly split into train/test by 8:2
    - build a dict that maps word (token) to frequency (int)
    - create a list of the most frequent words in the training set, called the closed vocabulary.
    - handle out of vocabulary (OOV) words: 
      - use a special token 'unk' to represent all unknown words. 
      - modify the data by converting all the other words that are not part of the closed vocabulary to the token 'unk'.
        
  - Develop N-gram Language Model:
    - def count_n_grams(data, n, start_token='<s>', end_token = '<e>') returns a dictionary that maps a tuple of n-words to its frequency
    - def estimate_probability(word, previous_n_gram, n_gram_counts, n_plus1_gram_counts, vocabulary_size, k=1.0) returns a probability using k-smoothing.
      - P(w_t|w_t-n, ..., w_t-1) = (C(w_t-n, ..., w_t-1, w_t)+k) / (C(w_t-n, ..., w_t-1)+k|V|)
    - def estimate_probabilities(previous_n_gram, n_gram_counts, n_plus1_gram_counts, vocabulary, k=1.0) returns a dictionary mapping from next words to the probability.
      - loops over all words in vocabulary to calculate probability as if the word is the next word
    - def make_count_matrix(n_plus1_gram_counts, vocabulary) returns count_matrix of the shape (len(n_grams), len(vocabulary))

  - Perplexity:
    - Perplexity is used as an evaluation metric of language models. 
      - Perplexity is Nth-root of the product of the inverse of P(w_t|w_t-n, ..., w_t-1) of the (n+1)th ~ Nth words in a given text of length N.
      - The higher the probabilities are, the lower the perplexity will be. Lower perplexity means better language model.
    - may use backoff - when n-gram is not found in the corpus, use (n-1)-gram; if also not found, use (n-2)-gram; until a probability is found.

  - Build an Auto-Complete System:
    - def suggest_a_word(previous_tokens, n_gram_counts, n_plus1_gram_counts, vocabulary, k=1.0, start_with=None) returns (most likely next word, corresponding probability)
    - def get_suggestions(previous_tokens, n_gram_counts_list, vocabulary, k=1.0, start_with=None) returns a list of suggestions
      - loop over various n-gram models (unigram, bigram, trigram, quadgram, qintgram) to get multiple suggestions, one best suggestion from each n-gram model.