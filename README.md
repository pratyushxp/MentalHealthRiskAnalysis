# MentalHealthRiskAnalysis

A hybrid machine learning and deep learning pipeline for mental health risk
detection from text, built on a multi-source dataset of over 265,000 Reddit
and public-domain records.

This repository contains the companion code for the published paper:

> **Mishra, P.** (2026). *A Hybrid Machine Learning and Deep Learning Approach
> for Mental Health Detection using Text Analysis.* Zenodo.
> https://doi.org/10.5281/zenodo.20971534

If you use this code or build on this work, please cite the paper above.

```bibtex
@article{mishra2026mentalhealth,
  author  = {Mishra, Pratyush},
  title   = {A Hybrid Machine Learning and Deep Learning Approach for Mental Health Detection using Text Analysis},
  year    = {2026},
  publisher = {Zenodo},
  doi     = {10.5281/zenodo.20971534},
  url     = {https://doi.org/10.5281/zenodo.20971534}
}
```

## Overview

The notebook (`MentalHealthRiskAnalysis.ipynb`) implements the full pipeline
described in the paper:

1. **Data collection** — scraping Reddit's public JSON API across multiple
   mental-health-related subreddits
2. **Dataset merging** — combining the Reddit data with public datasets
   (a Kaggle Reddit-depression dataset, a Twitter sentiment dataset, and the
   SuicideWatch dataset) into a single labeled dataset
3. **Data cleaning & feature engineering** — text normalization, TF-IDF
   vectorization, label encoding
4. **Exploratory data analysis** — label distribution, word frequency,
   word clouds, text length analysis
5. **Classical ML models** — Logistic Regression, Naive Bayes, Random
   Forest, SVM, KNN, XGBoost, and a Voting Ensemble
6. **Deep learning baseline** — a CNN + LSTM model trained on tokenized,
   padded sequences
7. **Inference pipeline** — risk scoring, sentiment analysis, keyword
   highlighting, a confidence score, and a plain-language explanation for
   any input text

### Results

| Model | Accuracy |
|---|---|
| Voting Classifier (ensemble) | **83.68%** |
| CNN + LSTM | 78.34% |

(See the paper for the full breakdown across all models, plus precision/recall/F1.)

## Repository contents

| File | Description |
|---|---|
| `MentalHealthRiskAnalysis.ipynb` | Full pipeline: data collection through model training and the inference demo |
| `DATASET.md` | Why the raw/cleaned dataset isn't included here, and how to regenerate it |
| `.gitignore` | Excludes dataset files and generated artifacts from version control |
| `LICENSE` | MIT License |

**Note:** No dataset files are included in this repository. See
[`DATASET.md`](DATASET.md) for the reasoning and instructions on how to
regenerate the dataset locally.

## Running the notebook

1. Clone this repository.
2. Install the dependencies used across the notebook:
   ```bash
   pip install requests pandas numpy matplotlib scikit-learn wordcloud textblob xgboost tensorflow
   ```
3. Open `MentalHealthRiskAnalysis.ipynb` in Jupyter.
4. Run the **Data Collection** and **Merging External Datasets** sections to
   build the dataset from scratch (see `DATASET.md` for details on the
   external datasets you'll need to download separately).
5. Run the remaining sections in order to reproduce cleaning, EDA, model
   training, evaluation, and the interactive inference demo.

## Disclaimer

This project is for educational and research purposes only. It is **not** a
clinical or diagnostic tool, and its predictions should never replace
professional mental health assessment or support.

## License

This project is licensed under the MIT License — see [`LICENSE`](LICENSE) for details.
