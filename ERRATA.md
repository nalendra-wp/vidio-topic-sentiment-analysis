# Corrections and Clarifications

This file lists corrections and clarifications to the published paper:

> Pinilih, N. W., Dewi, I. N., & Alzami, F. (2026). *An Integrated Topic–Sentiment Analysis of User Reviews in Vidio Application Using BERTopic and IndoRoBERTa.* Journal of Applied Informatics and Computing, 10(3), 2685–2698. https://doi.org/10.30871/jaic.v10i3.12952

It is an informal note by the first author, based on re-checking the paper against the notebook in this repository. It does not replace the published version, and any official correction is the journal's decision. The headline findings (topic coherence improvement, 72% accuracy, advertising as the dominant negative topic) are not affected by the items below.

Last updated: October 2026

## Corrections

| # | Where in the paper | Paper says | Correct value (from the notebook) |
|---|---|---|---|
| 1 | Table II, "Distribution of sentiment classes in the dataset" | Positive 2,052 · Neutral 830 · Negative 5,972 | These are the **model-predicted** counts. The rating-based labels are Positive 3,159 · Neutral 701 · Negative 4,994 (as in Table IX and the confusion matrix). |
| 2 | Table VII, number of reviews per topic | Topic 2: 802 · Topic 3: 453 · Topic 4: 282 · Topic 5: 148 · Topic 6: 137 · Outliers: 1.231 | Final counts are those in Table XI: Topic 2: 380 · Topic 3: 245 · Topic 4: 82 · Topic 5: 48 · Topic 6: 37 · Outliers (−1): 2,311. Topics 0 and 1 (3,917 and 1,834) are correct. All counts sum to 8,854. |
| 3 | Section II.A, collection period | 2 May 2025 – 2 April 2026 | The notebook filters 1 April 2025 – 1 April 2026. The retained data span 1 April 2025 – 31 March 2026. |
| 4 | Section II.A–B, filtering | Duplicates removed; reviews with fewer than three words removed; 15,000 reviews collected in the period | The scraper requested 15,000 reviews. Of these, 10,602 fell within the study period, and 8,854 remained after removing **one-word** reviews. The notebook does not remove duplicate reviews explicitly. |
| 5 | Figures 12–14 | Topic numbering 1–8; text states Topic 2 is the advertising topic | These figures were generated from an integrated dataset in which reviews were matched by text, which duplicated rows (14,714 rows instead of 8,854). Their counts differ from Table XI (for example, Topic 0 negative: 3,584 in the heatmap vs 2,869 in Table XI). Table XI is the correct reference. Advertising is Topic 0, and the figures should use the 0–6 topic numbering. |
| 6 | Table XIII, Section III.E | Kruskal–Wallis H = 5072.07; Spearman ρ = 0.7910 | Both tests were run on the same duplicated dataset as item 5. Also, the Spearman test in the notebook correlates **star rating with predicted sentiment class**, not topic prevalence with sentiment intensity as described in Section II.H. The values need to be recomputed on the 8,854-row dataset. Until then, treat them as indicative. |
| 7 | Section III.D, Topic 1 | "A strong positive cluster" | Table XI shows 780 positive (42.5%) and 892 negative (48.6%) reviews. Topic 1 has the highest share of positive reviews of all topics, but it is not majority positive. |

## Clarifications

- **Baseline coherence:** the paper reports 0.4076, and the notebook run in this repository gives 0.4072. The baseline and the tuned model also use different topic representations (single words vs. bigram/trigram phrases split into words), so the comparison is indicative.
- **Sentiment model:** `w11wo/indonesian-roberta-base-sentiment-classifier` is used as a pre-trained model, without fine-tuning, and is evaluated on the full dataset against rating-based labels. The word "baseline" in Tables IX and Section III.C refers to this setup.
- **Parameters not listed in Table II (BERTopic):** `max_df=0.5` in the vectorizer and `metric="euclidean"` in HDBSCAN.
- **Topic list in Section III.B:** the list of dominant topics mentions "streaming quality and buffering", which is not one of the seven topics in the topic table.

## Typographical issues

- Two tables are numbered "Table II" (class distribution and BERTopic parameters).
- Equation (5) is missing from the numbering.
- Equation (16): "potitive" should be "positive".
- Equation (3): the definitions of *w* and *w′* are swapped.
- Equation (7): the index range of the n-gram set is incorrect.
- Table I sample dates (April 2025) are consistent with the actual collection period in item 3.
- The first paragraph of the Conclusion ends with a duplicated sentence fragment.
