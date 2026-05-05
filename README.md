# Book Discount Analysis – Czech Book Week

A statistical analysis of discount pricing across 4,553 book titles during the Book Wook promotional campaign run by a Czech online bookstore. The project covers data preparation, random sampling, descriptive statistics, conditional probability, and price–discount relationship modeling — all implemented in Microsoft Excel.

---

## Dataset

- **Source:** Real promotional data from a Czech e-commerce bookstore (Book Week campaign)
- **Raw data:** 4,596 book titles with 6 variables: title, author, pre-campaign price, Book Week price, binding type, genre
- **Working population:** 4,553 discounted titles (absolute discount > 0 CZK)
- **Working sample:** 500 titles selected via simple random sampling

---

## Workbook Structure

| Sheet | Contents |
|-------|----------|
| Sheet 1 | Full source dataset with all calculated variables |
| Sheet 2 | Cleaned base population (n = 4,553) and random sample (n = 500) with sampling helper column |
| Sheet 3 | Genre frequency tables (overall, print, online) and comparative bar chart |
| Sheet 4 | Descriptive statistics of SLEVA_PERC by binding type and genre; box plots and histograms |
| Sheet 5 | Probability calculations for random title selection (P5) |
| Sheet 6 | Population-level discount group frequency table and probabilities (P6a) |
| Sheet 7 | Binomial and geometric probability analysis — the "Docent" scenario (P6b) |

---

## Calculated Variables

| Variable | Type | Description |
|----------|------|-------------|
| `SALE_ABS` | Numeric (CZK) | Absolute discount: pre-campaign price minus Book Week price |
| `SALE_PERC` | Percentage | Relative discount: absolute discount divided by pre-campaign price |
| `PRINTED_ONLINE` | Binary (0/1) | Distribution format: 1 = digital/online, 0 = print |
| `SALE_GROUP` | Categorical (1–4) | Discount tier based on SLEVA_ABS: Low (<25 CZK), Medium (25–75), High (75–150), Very High (>150) |

---

## Sampling Methodology

A simple random sample of 500 titles was drawn from the cleaned population using:

```excel
=SORTBY(SEQUENCE(4553), RANDARRAY(4553))
```

The generated order was immediately pasted as static values to prevent recalculation on file reopen. All titles had an approximately equal selection probability (~11%), satisfying Central Limit Theorem requirements for n = 500.

> Do not delete or overwrite the static helper column on Sheet 2. Regenerating it would change the sample composition and make results unreproducible.

---

## Key Findings

### Genre Distribution
- Least represented genre: **Cooking & Lifestyle** (3.40% of sample)
- **Romance & Erotica** skews heavily toward digital distribution (28.72% online vs. 9.36% print), likely driven by reader anonymity preferences
- **Children & Young Adult** dominates in print (15.76% print vs. 6.38% online), consistent with the physical nature of illustrated and board books
- The distribution patterns suggest a statistically meaningful association between genre and distribution format

### Discount Statistics
`SALE_PERC` was selected as the primary analytical metric over `SALE_ABS` due to lower right-skew and better comparability across price ranges.

- Mean: **34.0%** | Standard deviation: **16.6%**
- Chebyshev intervals (used instead of the empirical rule due to non-normal distribution):
  - At least 75% of titles fall within: **0.8% – 67.2%**
  - At least 88.9% of titles fall within: **0% – 83.9%**

**Discount variability by binding type:**

| Binding | Std. Dev. | Range |
|---------|-----------|-------|
| Hardcover | 10.47% | 38.7% |
| Paperback | moderate | — |
| Board book | 6.88% | 14.2% |

Hardcover titles show the highest discount variability, making their pricing least predictable. Board books are the most consistent.

### Price–Discount Relationship (Bonus)

A positive correlation exists between pre-campaign price and absolute discount. The most expensive quartile (Q4) averaged **150.56 CZK** in savings, suggesting a deliberate strategy of high nominal discounts on premium titles to maximize perceived value.

| Price Group | Mean Discount (CZK) | Median Discount (CZK) |
|-------------|---------------------|-----------------------|
| Q1 – Cheapest | 71.71 | 68.00 |
| Q2 – Lower-mid | 114.84 | 110.00 |
| Q3 – Upper-mid | 90.92 | 83.00 |
| Q4 – Most expensive | 150.56 | 126.00 |

### Probability Analysis

Using a binomial distribution (n = 15, p = 20.65%) for genre-targeted selection among print titles:

- Probability of selecting a title of interest on any single draw: **20.65%**
- Expected number of relevant titles per 15 draws: **E(X) = 3.1**
- P(first relevant title on exactly the 5th draw): **8.19%**
- P(at least 10 relevant titles in 15 draws): **0.02%**
