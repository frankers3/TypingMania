# Typing Mania

Typing Mania is a recommendation system designed to improve touch typing speed by suggesting practice words based on typing performance and word similarity. Unlike traditional typing tutors that use pre-written texts or random words, this project employs an algorithmic approach to recommend words that are both commonly used and similar to those typed slowly, enhancing "real world" typing efficiency.

## Features
- **Custom Word Similarity Metric**: Utilizes a convolution-based algorithm to measure word similarity by comparing substrings, prioritizing longer matches to reflect typing patterns.
- **Word Popularity Integration**: Leverages a dataset of 61,426 words, filtered from the Kaggle English Word Frequency dataset and Unix dictionary, to prioritize frequently used words.
- **WordRank Algorithm**: Adapts the PageRank algorithm to rank words by their usefulness, combining word similarity and popularity using a random surfer model with an alpha of 0.85.
- **Recommendation System**: Identifies words typed slower than average and recommends similar words for practice, calculated using inefficiency metrics (word time - average time × word rank).
- **Testing Framework**: Simulates typing performance to evaluate the system, demonstrating significant improvements in targeting problematic substrings (e.g., 57% of final paragraph words contained the substring "end" in tests).

## How It Works
1. **Dataset**: Combines the Kaggle English Word Frequency dataset with the Unix dictionary, reducing it to 61,426 valid words to eliminate misspellings and irrelevant terms.
2. **Similarity Graph**: Constructs an adjacency list graph where edges represent word similarities (threshold > 0.4), computed using a custom convolution-based formula.
3. **WordRank**: Ranks words based on similarity and popularity, using a random surfer model to prioritize words that are both common and connected to other common words (e.g., "in" ranks higher than "the").
4. **Recommendation**: Identifies slow-typed words, calculates their inefficiency, and suggests similar words for practice, dynamically generating paragraphs for typing practice.
5. **Testing**: Evaluates the system by simulating typing with a focus on specific substrings, measuring the percentage of recommended words containing those substrings.

## Key Metrics
- **Typing Efficiency**: Proposes a new metric, \( T_s = \sum_{k=1}^d \frac{s_k p_k}{\text{total}(p)} \), weighting words by speed (\( s_k \)) and popularity (\( p_k \)), instead of traditional WPM.
- **Inefficiency Score**: \( \text{Inefficiency} = (\text{wordtime} - \text{averagetime}) \times \text{wordrank} \), used to prioritize words for practice.
- **Similarity Formula**: \( \text{similarity} = \frac{\sum_{k=1}^n w_k^2}{s_1 \times s_2} \), adjusted for strings of different lengths to better reflect typing similarity.

## Implementation
- **Python Scripts**:
  - `create_similarity_graph.py`: Generates the word similarity graph, stored in `graph.csv`.
  - `recommend_words.py`: Handles recommendation logic, using word ranks and typing performance to suggest practice words.
- **Dependencies**: Uses `numpy`, `csv`, `random`, `time`, and `math` for data processing and simulation.
- **Dataset**: Sourced from [Kaggle English Word Frequency](https://www.kaggle.com/rtatman/english-word-frequency) and `/usr/share/dict/words`.

## Results
- The system successfully prioritizes useful words (e.g., "in" over "the" due to higher connectivity).
- Testing shows the algorithm effectively targets problematic substrings, with 57% of recommended words containing the substring "end" after 50 iterations (compared to 0.83% in the dataset).

## Usage
1. Clone the repository: `git clone https://github.com/frankers3/TypingMania`
2. Ensure Python and required libraries are installed.
3. Run `create_similarity_graph.py` to generate the similarity graph.
4. Use `recommend_words.py` to generate practice paragraphs based on typing performance.

## Future Improvements
- Refine the similarity metric for words of vastly different lengths.
- Optimize the convolution algorithm for larger datasets.
- Enhance the UI for a more interactive typing experience.

## References
- Ignjatovic, A., 2021. [DFT, DCT and Convolution](http://www.cse.unsw.edu.au/cs4121/lectures_2019/DFT_DCT_CONV_short.pdf).
- Ignjatovic, A., 2021. [Google PageRank and Markov Chains](http://www.cse.unsw.edu.au/cs4121/lectures_2019/pagerank_slides_short.pdf).
- Ignjatovic, A., 2021. [Recommender Systems](http://www.cse.unsw.edu.au/cs4121/lectures_2019/recommender_systems_short.pdf).
- Wu, G., 2021. [String Similarity Metrics - Edit Distance](https://www.baeldung.com/cs/string-similarity-edit-distance).
- Goel, A., 2021. [Applications of PageRank to Recommendation Systems](https://web.stanford.edu/class/msande233/handouts/lectures.pdf).
