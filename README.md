# Classical Natural Language Processing

This repository contains NLP projects using classical approaches, without word vectors.

## Bayesian Probability

* [Spelling Correction](https://github.com/msfchen/classical_nlp/tree/master/spellcorrect): 
  - Goal: to suggest the top n most likely correctly spelled words that are 1 and 2 edit distance from the mis-spelled word 
  - Approach: probability of a word being correct P(c|w) = P(w|c) * P(c) / P(w) where P(w|c) is the probability of having a word w given that it is correct, P(c) is the probability of being correct in general, and P(w) is the probability of the word w appearing in general.

* [Auto-Complete with N-gram Language Model](https://github.com/msfchen/classical_nlp/tree/master/autocomplete): 
  - Goal: to suggest the most likely next word and show its probability for the given previous N words 
  - Approach: N-gram Language Model (P(w_t|w_t-n, ..., w_t-1))

## Hidden Markov Models

* [Part-of-Speech, POS, Tagging with Viterbi Algorithm](https://github.com/msfchen/classical_nlp/tree/master/postaghmm): 
  - Goal: to assign the most likely part-of-speech tag (Noun, Verb, Adjective...) to each word in an input word_seq
  - Approach: Viterbi algorithm using dynamic programming

  