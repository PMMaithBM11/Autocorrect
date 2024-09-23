# Autocorrect System

This project implements an autocorrect system in Python that utilizes statistical and similarity-based approaches to correct misspelled words. The system operates by analyzing a large corpus of text, extracting word frequencies, and computing correction suggestions based on the Jaccard similarity between the input word and words in the corpus.

## System Overview

### Key Components

1. **Word Frequency Extraction**: The system processes an input text file, tokenizes the words, and computes the frequency of each word using the `collections.Counter` class.
   
2. **Word Probability Calculation**: Each word is assigned a probability, calculated as the relative frequency of the word in the corpus (i.e., the frequency of the word divided by the total number of words).

3. **Jaccard Similarity**: To generate suggestions for misspelled words, the system computes the Jaccard similarity between the input word and each word in the corpus using the `textdistance` library. This similarity metric compares the set of unique character n-grams (q-val = 2) of both words.

4. **Ranking Algorithm**: Suggestions are ranked by two criteria:
   - **Similarity**: Words with higher Jaccard similarity to the input word are preferred.
   - **Probability**: Among words with similar similarity scores, more frequent words (higher probability) are preferred.

5. **Output**: For misspelled words, the system outputs the top 3 word suggestions, ordered by similarity and word probability.

## Algorithmic Details

- **Word Frequency Calculation**: Given a text corpus `T` containing words \( w_1, w_2, ..., w_n \), we compute the frequency \( f(w) \) for each word \( w \in T \) as:
  \[
  f(w) = \frac{\text{count}(w)}{\sum_{i=1}^{n} \text{count}(w_i)}
  \]
  
- **Jaccard Similarity**: For two words \( w \) and \( v \), the Jaccard similarity based on bi-grams is defined as:
  \[
  J(w, v) = \frac{|B(w) \cap B(v)|}{|B(w) \cup B(v)|}
  \]
  where \( B(w) \) represents the set of bi-grams in word \( w \).

- **Ranking**: The final ranking is determined first by Jaccard similarity, then by word frequency if multiple words have similar similarity scores.

## Possible Future Improvements

-**N-gram Models**: Incorporate an n-gram model to suggest corrections based on context (e.g., bigrams or trigrams).

-**Levenshtein Distance**: Replace Jaccard similarity with Levenshtein distance for more nuanced suggestions, especially for words with minor spelling errors.

-**Dynamic Corpus Update**: Add functionality to dynamically update the corpus with user input to improve correction over time.

