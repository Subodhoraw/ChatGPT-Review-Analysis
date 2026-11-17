# ChatGPT Review Analysis

A reproducible Python project that analyses written ChatGPT app reviews and star ratings to understand user sentiment, recurring themes, and changes in feedback over time. The workflow uses Pandas for data preparation, TextBlob for baseline sentiment scoring, scikit-learn's `CountVectorizer` for keyword and phrase frequency, and Matplotlib/Seaborn for visualisation.

## Project objectives

- Measure the distribution of star ratings and the average rating.
- Calculate sentiment polarity and subjectivity for non-empty review text.
- Classify reviews as positive, neutral, or negative using a transparent polarity rule.
- Compare text-derived sentiment with star ratings.
- Extract frequent unigrams and bigrams from positive and negative reviews.
- Examine review volume, average polarity, subjectivity, and rating by month.

## Dataset

The supplied CSV contains **196,727 rows** and four fields:

| Source column | Description |
|---|---|
| `Review Id` | Review identifier |
| `Review` | Written review text |
| `Ratings` | User rating (observed values: 1–5) |
| `Review Date` | Review timestamp |

Observed date coverage: **25 July 2023 to 23 August 2024**. Initial audit of the supplied file found 6 missing review texts, 2,511 exact duplicate rows, and 3,573 repeated Review ID occurrences after the first occurrence. These are separate data-quality measures; repeated IDs are not automatically removed.

### Dataset access

The raw CSV is intentionally **not included** in this public repository because redistribution rights and permission to republish user-written review text have not been established. Place the authorised `chatgpt_reviews.csv` file in the project root, or upload it when running the notebook in Google Colab. Do not publish raw review text unless its source terms and privacy requirements permit redistribution.

## Repository structure

```text
ChatGPT-Review-Analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── README.md
├── docs/
│   └── presentation-outline.md
└── notebooks/
    └── ChatGPT_Review_Analysis.ipynb
```

## How to run

### Google Colab

1. Open `notebooks/ChatGPT_Review_Analysis.ipynb` in Google Colab.
2. Run the installation/import cell.
3. Run the data-upload cell and select the authorised `chatgpt_reviews.csv` file.
4. Run all cells from top to bottom.
5. Use the generated summary tables and charts for the presentation.

### Local Jupyter

1. Create and activate a Python environment.
2. Install dependencies: `pip install -r requirements.txt`.
3. Put `chatgpt_reviews.csv` in the project root.
4. Open and run `notebooks/ChatGPT_Review_Analysis.ipynb`.

## Methodology

1. Preserve the original DataFrame for traceability.
2. Rename fields to consistent snake_case names.
3. Parse review timestamps and numeric ratings.
4. Remove exact duplicate rows from the analysis copy only.
5. Keep repeated Review IDs for investigation when the remaining row content differs.
6. Exclude blank review text from text-based sentiment and keyword analysis, while retaining records with valid ratings/dates for appropriate non-text analysis.
7. Use TextBlob polarity and subjectivity as baseline lexicon-based indicators.
8. Classify polarity `> 0` as Positive, `< 0` as Negative, and `= 0` as Neutral.
9. Use `CountVectorizer` with English stop words and a small set of generic app/product terms to extract frequent unigrams and bigrams.
10. Aggregate review volume and mean metrics by calendar month.

## Interpretation and limitations

- TextBlob scores are approximate language-based signals, not human-labelled ground truth or a validated measure of customer satisfaction.
- Sarcasm, negation, context, mixed opinions, emojis, spelling variations, short reviews, and multilingual text can be misclassified.
- Keyword frequency identifies recurring terms; it does not prove why a user is satisfied or dissatisfied. Inspect representative reviews before making product recommendations.
- Ratings and text sentiment measure different things and should be compared rather than treated as interchangeable.
- The dataset covers roughly 13 months; do not infer long-term or recurring seasonality from this period alone.
- Review IDs that repeat after exact-row deduplication should be investigated using source-specific rules rather than silently deleted.

## Presentation

The notebook includes an automatically generated findings section. Run the notebook and use its current outputs for all numbers in the project presentation. Do not manually reuse figures from an earlier run if the data-cleaning decisions change.

## Tools

Python, Pandas, NumPy, TextBlob, scikit-learn, Matplotlib, Seaborn, Jupyter Notebook / Google Colab.
