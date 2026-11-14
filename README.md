# customer-feedback-segmentation
A Python pipeline that takes e-commerce reviews (star rating + free-text comment), cleans them, and segments customers according to how satisfied they really are. The goal is to know who should be left alone, who should be thanked, and who needs attention, without asking people who have already reviewed for another review.
# Why
Star ratings and comments don't always agree. Reviewers can commit errors (e.g. 5 stars with a complaint in the text). Using both signals gives a more reliable picture of customer satisfaction than stars alone, and lets us handle the ambiguous middle (3-star reviews) with the comment as a tiebreaker.
#Scope
Included
Cleaning: load the raw reviews, handle missing values and duplicates, normalise text.
Segmentation: classify the sentiment of each comment, combine it with the star rating, and assign each review to a segment.
