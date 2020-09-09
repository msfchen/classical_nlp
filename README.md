# Classical Natural Language Processing

This repository contains NLP projects using classical approaches.

## Bayesian Probability

* [Spelling Correction](https://github.com/msfchen/classical_nlp/tree/master/spellcorrect): [6/29/2020, Coursera NLP Specialization]
  - Goal: to suggest the top n most likely correctly spelled words that are 1 and 2 edit distance from the mis-spelled word 
  - Approach: probability of a word being correct P(c|w) = P(w|c) * P(c) / P(w) where P(w|c) is the probability of having a word w given that it is correct, P(c) is the probability of being correct in general, and P(w) is the probability of the word w appearing in general.

## Hidden Markov Models

* [Part-of-Speech, POS, Tagging using Viterbi Algorithm](https://github.com/msfchen/classical_nlp/tree/master/postaghmm): [6/29/2020, Coursera NLP Specialization]
  - Goal: to assign the most likely part-of-speech tag (Noun, Verb, Adjective...) to each word in an input word_seq
  - Approach: Viterbi algorithm using dynamic programming

  