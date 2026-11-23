# NLP Text Classification – Detailed Text Preprocessing

University assignment for the Artificial Intelligence and Smart System Research Lab.
Task: movie review **sentiment classification** (positive / negative) with the main focus on **detailed text preprocessing**.

## Project structure

```text
NLP_Text_Classification/
├── data/
│   └── IMDB_Dataset.csv                      # original dataset (never modified)
├── outputs/
│   ├── figures/                              # class_distribution.png, text_length.png, confusion_matrices.png
│   └── results/                              # model_comparison.csv, preprocessing_comparison.csv,
│                                             # preprocessing_stage_statistics.csv, run_summary.json
├── NLP_Text_Classification.ipynb             # executed notebook (outputs included)
├── NLP_Text_Classification_Presentation.pptx # 10 slides, about 10 minutes
└── README.md
```

## Dataset

- **IMDB Movie Reviews (50K)**, downloaded from GitHub:
  https://raw.githubusercontent.com/Ankit152/IMDB-sentiment-analysis/master/IMDB-Dataset.csv
- Columns: `review` (text) and `sentiment` (label: `positive` / `negative`).
- 50,000 reviews, 25,000 per class, 418 duplicate rows, no missing values.
- The notebook downloads the file automatically if `data/IMDB_Dataset.csv` is missing.
- For speed, the notebook uses a **stratified sample of 10,000 reviews** (duplicates removed first) and an
  **80:20 stratified train/test split** (`random_state=42`). Set `SAMPLE_SIZE = None` in Section 3.9 to use all reviews.

## How to run (local Conda environment)

```bash
conda create -n nlp_assignment python=3.11 -y
conda activate nlp_assignment
pip install pandas numpy matplotlib seaborn nltk scikit-learn notebook ipykernel
cd NLP_Text_Classification
jupyter notebook NLP_Text_Classification.ipynb      # or open the folder in VS Code
```

Then choose **Run All**. Notes:

- Run the notebook **from the project folder** (all paths are relative).
- NLTK resources (stopwords, wordnet, omw-1.4, punkt, punkt_tab) are downloaded by Section 2 and need internet access the first time.
- Everything is seeded (`SEED = 42`), so results are reproducible.
- Expected run time: about 1-2 minutes with the default 10,000-review sample.

## Notebook outline

1. Introduction  2. Libraries  3. Dataset exploration  4. **Detailed text preprocessing (10 steps + reusable functions)**
5. Preprocessing comparison table  6. Feature extraction (Bag of Words, TF-IDF, n-grams)
7. Classification (Logistic Regression, SVM, Multinomial Naive Bayes)  8. Evaluation  9. Prediction on new text  10. Conclusion

Preprocessing steps: lowercasing, HTML removal, URL removal, special-character removal (negative contractions expanded first),
whitespace normalization, tokenization, stopword removal (negations `no`, `nor`, `not`, `never` kept),
Porter stemming, WordNet lemmatization, final text. The lemmatized text is used for classification.

## Presentation

`NLP_Text_Classification_Presentation.pptx` has 10 slides with speaker notes and timing hints; slides 4-7 cover preprocessing.
All examples and numbers on the slides come from the executed notebook (`outputs/results/run_summary.json`).
**Before presenting, replace `[Your Name]` and `[Course name]` on slide 1.**
