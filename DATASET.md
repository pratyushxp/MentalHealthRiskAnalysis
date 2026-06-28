# About the Dataset

This repository contains the full data collection, cleaning, and modeling
pipeline (`MentalHealthRiskAnalysis.ipynb`), but it does **not** include the
raw or cleaned dataset files. This was a deliberate choice, explained below.

## Why the dataset isn't included

The data was collected from public posts on Reddit (subreddits including
`r/depression`, `r/anxiety`, `r/lonely`, `r/socialanxiety`, `r/healthanxiety`,
and others), combined with three external public datasets covering similar
mental-health text. While the source posts were publicly visible, redistributing
them as a bundled, downloadable CSV introduces risks that don't exist when the
posts are scattered across the original platform:

- **Direct re-identification.** Each scraped row keeps the original Reddit
  `post_id`. That ID can be pasted directly into a Reddit URL to land back on
  the original post and the original author's account — this is not
  theoretical anonymity, it's a direct link back to a real person.
- **Loss of the author's control.** If someone later deletes or edits their
  post on Reddit (common for posts disclosing depression, self-harm, or
  suicidal ideation), a copy sitting in this repo would preserve it forever,
  outside their control and against their later wishes.
- **Aggregation harm.** A single post about depression, on its own, blends
  into Reddit's normal traffic. The same post bundled into a labeled,
  searchable "depression dataset" alongside thousands of others is far more
  discoverable and easier to misuse — for profiling, scraping by bad actors,
  or simply embarrassment if the author is later identified.
- **Sensitive subject matter.** This data includes raw, personal statements
  about depression, anxiety, loneliness, and in some cases suicidal ideation.
  Publishing it for anyone to download, with no oversight on how it's reused,
  doesn't meet the bar most institutional/ethics review processes would set
  for this kind of data, even when each individual post was technically public.
- **Third-party dataset licensing.** The Kaggle, Twitter sentiment, and
  SuicideWatch datasets merged into this pipeline belong to their original
  authors/sources. Redistributing them again from this repo could conflict
  with their original terms — they should be downloaded from their original
  source, not from here.

This mirrors how most published mental-health NLP research handles this
trade-off: the **code** is shared openly so the methodology is reproducible,
but the **raw text data** is either kept private, gated behind a data-use
agreement, or simply not redistributed in bulk.

## What's included instead

- The full notebook (`MentalHealthRiskAnalysis.ipynb`), so the entire
  pipeline — scraping, cleaning, merging, modeling — can be inspected or
  re-run.
- `dataset_summary.txt`, which the notebook generates automatically. It
  contains only aggregate statistics (row counts, label distribution,
  subreddit distribution) — no raw post text.

## How to regenerate the dataset yourself

1. Run the **Data Collection** and **Merging External Datasets** sections of
   the notebook. These rebuild `mental_health_dataset.csv` from scratch by
   querying Reddit's public JSON API directly.
2. Download the three external datasets from their original sources and
   place them alongside the notebook before running the merge cells:
   - Kaggle Reddit depression dataset → `depression_dataset_reddit_cleaned.csv`
   - Twitter sentiment dataset → `sentiment_tweets3.csv`
   - SuicideWatch dataset → `Suicide_Detection.csv`
3. Run the **Data Cleaning** section to produce
   `mental_health_dataset_cleaned.csv` locally.

All dataset files (`mental_health_dataset.csv`,
`mental_health_dataset_cleaned.csv`, and the external source CSVs) are listed
in `.gitignore` so they're never committed by accident.
