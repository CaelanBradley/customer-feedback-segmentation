# customer-feedback-segmentation
A Python pipeline that takes e-commerce reviews (star rating + free-text comment), cleans them, and segments customers according to how satisfied they really are. The goal is to know who should be left alone, who should be thanked, and who needs attention, without asking people who have already reviewed for another review.

# Why
Star ratings and comments don't always agree. Reviewers can commit errors (e.g. 5 stars with a complaint in the text). Using both signals gives a more reliable picture of customer satisfaction than stars alone, and lets us handle the ambiguous middle (3-star reviews) with the comment as a tiebreaker.

# Scope
Cleaning: load the raw reviews, handle missing values and duplicates, normalise text.
Segmentation: classify the sentiment of each comment, combine it with the star rating, and assign each review to a segment.
# Pipeline
raw reviews (comment + stars)
        │
        ▼
   1. Cleaning
        │
        ▼
   2. Segmentation  (comment sentiment + stars)
        │
        ▼
segmented reviews (CSV)

# Segmentation rules

| Stars | Comment sentiment | Segment | Intended downstream use |
| --- | --- | --- | --- |
| 5 | Positive | Promoter + newsletter | Treated as promoters, no follow-up |
| 4 | Positive | Newsletter invitation | Newsletter, no follow-up |
| 3 | Positive / Neutral / negative | Follow-up | Multiple-choice follow-up |
| 1-2 | Negative | Escalation | Customer service escalation list |
| 4-5 | Negative | Needs review | Stars and comment disagree |
| 1-2 | Positive | Needs review | Stars and comment disagree |

**Notes**

- The "downstream use" column describes the intended purpose of each segment. These actions are not implemented yet; the pipeline only produces the segment labels.

# Project structure
.
├── data/
│   ├── raw/            # original reviews (not committed)
│   └── processed/      # cleaned and segmented output
├── src/
│   ├── cleaning.py
│   ├── segmentation.py
│   └── config.py       # thresholds and segment rules
├── notebooks/          # exploration
├── tests/
├── requirements.txt
└── README.md
