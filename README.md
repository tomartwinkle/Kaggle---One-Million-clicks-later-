# One Million Clicks Later — IEEE SBM Kaggle Competition

This was a private Kaggle competition hosted by IEEE-SBM, MIT Manipal.
It required participants to predict whether a user would click on a video recommendation, based on their interaction history and video metadata.
<br>
It was my first full end-to-end machine learning competition, and it involved a large dataset, noisy columns, time constraints, and a fair amount of debugging.
Definitely a memorable two-day sprint.

## Dataset Summary

The dataset included behavioral and platform interaction logs with columns such as:

- user_id, video_id

- video_duration, watch_time, watch_percent

- liked, commented, subscribed_after

- timestamp

- device, category, source

- recommended (whether a video was recommended)

- clicked (target column)

The target was binary, but the distribution was highly imbalanced — the majority of entries were clicked = 0.

## Approaches Tried

I experimented with two main modeling approaches.

1. Standard Supervised Classification

I trained several models including Logistic Regression, Random Forest, Gradient Boosting, and XGBoost.
After comparisons, XGBoost performed best because it:

handled sparse and noisy data well

scaled efficiently with the dataset size

allowed tuning for class imbalance (scale_pos_weight)

- To deal with imbalance, I tried:

oversampling and undersampling

SMOTE

Edited Nearest Neighbours (ENN)

threshold optimization instead of relying on default probability cut-offs

The performance improved gradually, and most of the work went into feature engineering rather than model selection.

2. Recommendation-Focused Modeling

Since the problem statement specifically asked to predict whether a user would click a recommended video, I explored the idea of modeling only the subset where recommended = 1.

Initially, I made a mistake by filtering too aggressively and unintentionally removing useful negative samples.
A more correct approach would have been:

Filter dataset to recommended = 1, but keep both classes (clicked = 0 and 1), because not all recommended videos are clicked.

This reduced noise and aligned the model more closely with the intended real-world use case.

## Key Challenge: Class Imbalance

The dataset was heavily skewed toward clicked = 0, which meant naïve models could predict everything as “not clicked” and still appear accurate.

This forced me to:

evaluate performance using F1 score instead of accuracy

tune thresholds

apply class balancing strategies

carefully validate generalization rather than memorization

## Final Result

All participants eventually reached the same official leaderboard score:
F1 Score: 0.853 (public leaderboard)

The model performed realistically — not perfect, but meaningful given the user behavior patterns and available features.
