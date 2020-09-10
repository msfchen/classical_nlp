# Part-of-Speech, POS, Tagging using Viterbi Algorithm

- Goal: to assign the most likely part-of-speech tag (Noun, Verb, Adjective...) to each word in an input word_seq
- Approach: Viterbi algorithm using dynamic programming

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
  