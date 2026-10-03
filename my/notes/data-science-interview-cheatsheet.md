# Data-science interview cheat sheet

Use this as a **reasoning checklist**, not a script to memorise. In an interview, clear assumptions and a sensible baseline matter more than a fancy model.

## 1. Start any data question this way

1. What decision will this analysis or model support?
2. What is one row of the data (the table's *grain*)?
3. What are we predicting, for whom, and at what future time?
4. Which data are actually available at prediction time? (Avoid leakage.)
5. How will success be measured, and what do false positives / false negatives cost?
6. What simple baseline should we beat?

**A good spoken structure:** clarify goal -> define metric and population -> inspect data -> build a simple baseline -> validate -> explain trade-offs -> recommend and monitor.

## 2. NumPy and data basics

| Idea | Meaning / useful tools |
|---|---|
| Inspect first | `x.shape`, `x.dtype`, missing values, duplicates, and a few example rows |
| Rows and columns | Usually `(n, d)` = `n` samples (rows), `d` features (columns) |
| `axis=0` | Work down rows; result is one value per **column** / feature |
| `axis=1` | Work across columns; result is one value per **row** / sample |
| `*` | Element-by-element multiplication |
| `@` | Matrix multiplication (`np.matmul`) |
| Broadcasting | `(n, d) - (d,)` subtracts the same feature vector from every row |
| Common tools | `np.mean`, `np.std`, `np.sum`, `np.sqrt`, `np.where`, `np.argmax`, boolean masks, `reshape` |
| Linear algebra | `np.linalg.det`, `np.linalg.solve`, `np.linalg.inv`, `np.linalg.norm` |

Standardising a feature means: subtract its training-set mean, then divide by its training-set standard deviation. Constant features need special handling because their standard deviation is zero.

## 3. Statistics and A/B tests

- **Mean** is sensitive to outliers; **median** is more robust.
- **Variance / standard deviation** measure spread.
- **Correlation is not causation.** A third factor may explain both variables.
- A **confidence interval** is an uncertainty range produced by a method and its assumptions.
- A **p-value** asks: *if the null hypothesis were true, how surprising would this result (or a more extreme one) be?* It is not the probability that the null is true.
- **Type I error:** false positive. **Type II error:** false negative. **Power:** chance of detecting a real effect.

For an A/B test, say you would define in advance:

- hypothesis and primary metric;
- eligible population and randomisation unit;
- experiment duration and sample size;
- guardrail metrics (for example, cancellations or latency);
- decision rule and minimum practically useful effect.

Always distinguish **statistical significance** from **business significance**.

## 4. Machine-learning essentials

| Topic | Key point |
|---|---|
| Supervised learning | Learn from labelled examples. Regression predicts a number; classification predicts a class or probability. |
| Train / validation / test | Fit models and preprocessing on train; choose settings on validation; report final performance once on test. |
| Leakage | Using future or otherwise unavailable information. It makes validation look falsely good. |
| Underfitting | Model is too simple to capture the pattern. |
| Overfitting | Model learns noise; training performance is much better than new-data performance. |
| Regularisation | Penalises overly complex models; can reduce overfitting. |
| Cross-validation | Repeats train/validation splits to estimate performance more reliably. |
| Baseline | A simple comparison: mean prediction, majority class, or a simple linear model. |

### Metrics

- **MAE:** average absolute error; easy to explain and less dominated by outliers.
- **RMSE:** penalises large errors more strongly.
- **Precision:** when I predict positive, how often am I right?
- **Recall:** of all actual positives, how many did I find?
- **F1:** balances precision and recall.
- **ROC-AUC:** ranking quality across thresholds.
- **PR-AUC:** often more useful when positives are rare.

Choose a classification threshold from the cost of errors; `0.5` is only a default, not a business decision.

Scaling usually matters for distance- and gradient-based models (k-NN, logistic regression, SVM); it is usually unnecessary for tree-based models.

## 5. SQL essentials

- Core clauses: `SELECT`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `CASE WHEN`, CTEs.
- Logical order: `FROM/JOIN -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY -> LIMIT`.
- `INNER JOIN` keeps matches only; `LEFT JOIN` keeps every row from the left table.
- Before a join, state the grain of both tables. A one-to-many join can accidentally duplicate rows.
- `COUNT(*)` counts rows; `COUNT(column)` ignores `NULL`; `COUNT(DISTINCT column)` counts unique non-null values.
- Use `IS NULL`, not `= NULL`; use `COALESCE` for a fallback value.
- Know window functions such as `ROW_NUMBER()`, `LAG()`, and `SUM(...) OVER (...)`.

## 6. Communication and edge cases

- State assumptions aloud instead of silently making them.
- Mention likely problems: missing values, duplicates, class imbalance, leakage, sampling bias, confounding, stale data, and fairness.
- Work through a tiny example when coding; check shapes and edge cases.
- For behavioural questions, use **STAR**: Situation, Task, Action, Result.
- End a case answer with an action: what you recommend, how you would measure impact, and what you would monitor after launch.

> Interview rule of thumb: a correct simple approach explained clearly is better than an unexplained complicated one.
