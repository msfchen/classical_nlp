# Classical Natural Language Processing

This repository contains NLP projects using classical approaches.

## Bayesian Probability

* [Spelling Correction](https://github.com/msfchen/classical_nlp/tree/master/spellcorrect): [6/29/2020, Coursera NLP Specialization]
  - Goal: to suggest correctly spelled words that are 1 and 2 edit distance from the mis-spelled word 
  - Approach: probability of a word being correct P(c|w) = P(w|c) * P(c) / P(w) where P(w|c) is the probability of having a word w given that it is correct, P(c) is the probability of being correct in general, and P(w) is the probability of the word w appearing in general.
  - Data Preprocessing: turn corpus into a list of words -> word_count_dict -> P(w)
  - String Manipulations: 
    - def delete_letter(word) returns a list of all possible strings obtained by deleting 1 character from word; 
    - def switch_letter(word) returns a list of all possible strings with one adjacent charater switched; 
    - def replace_letter(word) returns a list of all possible strings where one letter from the original word was replaced by another letter (including itself).
    - def insert_letter(word) return a list of all possible strings with one new letter inserted at every offset
  - Combining the edits to find the most likely correct words:
    - def edit_one_letter(word, allow_switches = True) returns a set of strings with all possible one edit from word.
    - def edit_two_letters(word, allow_switches = True) returns a set of strings with all possible two edits from word.
    - def get_corrections(word, probs, vocab, n=2) return n number of best (by P(w)) suggested correct words for the given word.
  - Find minimum edit distance between two strings using dynamic programming

## Hidden Markov Models

* [Part-of-Speech, POS, Tagging using Viterbi Algorithm](https://github.com/msfchen/classical_nlp/tree/master/postaghmm): [6/29/2020, Coursera NLP Specialization]
  - assigning a part-of-speech tag (Noun, Verb, Adjective...) to each word in an input text
  - explore the preprocessed and POS-tagged training and test corpra; build vocab = { word: idx } from the given hmm_vocab.txt
  - use training_corpus to build emission_counts = {(tag, word):count}, transition_counts = {(prev_tag, tag):count}, tag_counts = {tag:count}; use tag_counts to build states = sorted list of all possible tags
  - POS tag for a word is determined by the (tag, word) of the word in the emission_counts that has the highest count. 
  - create transition probabilities P(t_i|t_i-1) matrix A and emission probabilities P(w_i|t_i) matrix B
  - Viterbi algorithm utilizes dynamic programming, which can be decomposed into 3 steps:
    - initialization: initialize best_paths and best_probs matrices; best_paths: matrix of dimension (num_tags, len(word_seq)) of integers; best_probs: matrix of dimension (num_tags, len(word_seq)) of floats
      - Both matrices will be initialized to zero except for column zero of best_probs. Column zero of best_probs is initialized with the assumption that the first word of the word_seq was preceded by a start token ("--s--"). Reference the A matrix for the transition probability.
      - 𝑖𝑓𝐴[𝑠𝑖𝑑𝑥,𝑖]!=0:𝑏𝑒𝑠𝑡_𝑝𝑟𝑜𝑏𝑠[𝑖,0]=𝑙𝑜𝑔(𝐴[𝑠𝑖𝑑𝑥,𝑖])+𝑙𝑜𝑔(𝐵[𝑖,𝑣𝑜𝑐𝑎𝑏[word_seq[0]]; 𝑖𝑓𝐴[𝑠𝑖𝑑𝑥,𝑖]==0:𝑏𝑒𝑠𝑡_𝑝𝑟𝑜𝑏𝑠[𝑖,0]=𝑓𝑙𝑜𝑎𝑡(′−𝑖𝑛𝑓′)
    - Viterbi forward
      - compute the probability and path for the 𝑖𝑡ℎ word in the word_seq, the prior word 𝑖−1 in the word_seq, current POS tag 𝑗 , and previous POS tag 𝑘:
      - prob=𝐛𝐞𝐬𝐭_𝐩𝐫𝐨𝐛𝑘,𝑖−1+log(𝐀𝑘,𝑗)+log(𝐁𝑗,𝑣𝑜𝑐𝑎𝑏(word_seq_𝑖)); retain the highest probability computed for the current word as best_prob_i and the corresponding best_path_i = k
    - Viterbi backward
      - The Viterbi backward algorithm gets the predictions of the POS tags for each word in the word_seq using the best_paths and the best_probs matrices.
      - Go through each POS tag for the last word (last column of best_probs) to find the row (POS tag integer ID) with highest probability for the last word
      - Find the best POS tags by walking backward through the best_paths From the last word in the word_seq to the 0th word in the word_seq; return the corresponding POS_tag_seq.
  