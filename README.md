# Classical NLP

This repository contains NLP projects using classical approaches.

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