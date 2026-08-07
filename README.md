<div align="center">

# Ariyan Tipu

**BSc Mathematics with Data Science (2:1, upper second class), City, University of London**

**MSc Statistics, King's College London, from September 2026**

I work in Python and SQL across applied machine learning, statistical modelling
and data engineering.

**Applying for 2027 graduate data, machine learning and software roles.**
Available for short-term work before the MSc begins this September, and for
part-time London roles during it.

London, UK · Right to work in the UK, no visa sponsorship required

[ariyantipu39@gmail.com](mailto:ariyantipu39@gmail.com) ·
[LinkedIn](https://www.linkedin.com/in/ariyantipu/) ·
[**Dashboard demo**](https://ariyan-tipu.github.io/realtime-orders-platform/)
(runs in the browser on simulated events)

</div>



## Projects

### 1. [Customer retention on 99,441 real e-commerce orders](https://github.com/ariyan-tipu/olist-customer-retention)

`PySpark` · `scikit-learn` · `R` · `MATLAB` · `FastAPI` · `Docker`

Churn modelling, survival analysis and experiment design on the Olist
Brazilian e-commerce dataset, across nine relational tables.

- Predicted repeat purchase at a **0.975% base rate**, reaching **2.0x to 2.45x
  lift in the top decile**, which captures 20 to 24% of all repeaters at twice
  the background rate.
- Fixed the selection metric to cross-validated **average precision** before
  scoring the holdout, then applied it even though gradient boosting won ROC-AUC
  (0.652 against 0.611) while losing average precision. At 1% positives ROC-AUC
  flatters: the ROC and precision-recall curves rank the two models in opposite
  orders from the same predictions, and both curves are in the repository.
- Ran **Kaplan-Meier, Cox and Weibull AFT** survival analysis on 93,350 spells
  at **98.1% right-censoring**. A poor first review cuts the repurchase hazard
  by 27% (HR 0.727, p = 0.0002); late delivery loses significance once the
  review is controlled, because it does its damage through the review.
- Re-derived the Weibull fit in **MATLAB** by maximising the censored
  log-likelihood from first principles, agreeing with R's `survreg` to **2e-07**
  on every parameter.
- Showed a realistic +15% uplift test would need **76,101 customers per arm**,
  more than a quarter's entire intake, and recommended against running it as
  specified.

### 2. [A language model checked against a chess engine](https://github.com/ariyan-tipu/opening-theory-engine)

`PyTorch` · `Transformers` · `PEFT` · `TRL` · `JAX` · `FastAPI` · `Stockfish`

A small model fine-tuned to explain chess opening moves, where each claim the
parser recognises is checked against Stockfish at depth 14 rather than against a
human rating.

- **Built the evaluation harness first, and it is what the project is for.**
  After fine-tuning, only **2% of responses** pass full verification, and the
  tuned models quote an illegal move in roughly **95%** of their engine lines.
  Nothing subjective would have caught that.
- Built and ran the full **QLoRA supervised fine-tuning then DPO** pipeline for
  Qwen2.5-3B-Instruct in 4-bit on a free Colab T4. Adapters, curves and results
  are published in the
  [v0.1.0 release](https://github.com/ariyan-tipu/opening-theory-engine/releases/tag/v0.1.0).
- Generated preference pairs from **engine evidence with no human labels**: a
  deterministic parser extracts each claim and checks it against Stockfish's
  evaluation, principal variation and material arithmetic.
- Raised format compliance from **1% to 100%** and verdict accuracy from **0.29
  to 0.50**. DPO's gain over supervised fine-tuning (claim precision 0.5721 to
  0.5745) is too small for one 150-position run with a single seed to call real,
  and the repository says so.
- The same verifier runs in training, evaluation and serving, so all three mean
  the same thing. Serving is an explain-verify-regenerate loop that ships a
  verification report with every response.

### 3. [Real-time orders platform](https://github.com/ariyan-tipu/realtime-orders-platform) · [dashboard demo](https://ariyan-tipu.github.io/realtime-orders-platform/)

`Python` · `Django` · `FastAPI` · `PostgreSQL` · `C++17` · `Vue 3` · `TypeScript` · `Docker`

An order and inventory backend built around the parts that are easy to get
quietly wrong.

- Every stock write goes through one service that takes row-level locks in
  **primary-key order**, so writers using it cannot oversell and cannot deadlock
  on lock ordering. Proven by a test that releases **eight simultaneous
  transactions against five units** through a barrier: exactly five succeed,
  stock lands at zero, never negative.
- Streamed order and stock events to a Vue dashboard over WebSockets fed by
  PostgreSQL `LISTEN/NOTIFY`, emitted inside the committing transaction, so no
  event can exist for work that rolled back. This removes the dual-write race a
  message broker would introduce, and the repository documents where the
  guarantee stops: the channel is transactional but not durable.
- Wrote the pick-path optimiser **twice**, in Python and C++17 via pybind11,
  with a 150-case randomised parity suite asserting exact equality and a
  Held-Karp solver bounding solution quality. The C++ engine is roughly **100x
  faster** on large orders and releases the GIL while it runs.
- Cut a ranked per-warehouse aggregation from about **105 ms to 4 ms** with a
  partial covering index, documented with the query plans, including the first
  index design the planner correctly ignored.
- Access control is a project-wide default rather than a per-view decision:
  reads are open, writes need authentication unless demo mode is on, and
  lifecycle transitions, which move stock, need it either way. Every environment
  switch fails closed and CI fails the build on any Django deployment-check
  warning.

---

## Education

**MSc Data Science**, King's College London, from September 2026

*Modules include:* Data Mining · Databases, Data Warehousing and Information
Retrieval · Statistics for Data Analysis · Pattern Recognition, Neural Networks
and Deep Learning, plus a 60-credit individual project.

**BSc Mathematics with Data Science**, City, University of London. Awarded a 2:1
(upper second-class honours)

*Group dissertation: linear, non-linear and solitary waves, and their
application to traffic flow.* Traffic jams behave as travelling waves: a
disturbance propagates backwards through a queue while the cars themselves move
forwards. The work covered the linear and non-linear wave equations,
D'Alembert's solution, KdV solitary waves, the viscous and inviscid Burgers'
equations, the method of characteristics, the Rankine-Hugoniot jump condition
and conservation laws in integral and differential form.

*A-levels:* Mathematics · Further Mathematics · Computer Science

*Relevant modules:* Machine Learning · Statistics and Probability 2 ·
Techniques of Data Science · Principles of Data Science

## Experience

- **Lead Tutor:** redesigned the A-level Further Mathematics curriculum I taught
  from, and mentored students one to one and in small groups.
- **Bright Network Internship Experience UK (Technology):** a short virtual
  insight programme covering how technology teams operate, with a group project.

## Technical skills

**Languages** Python · SQL · R · C++ · TypeScript · MATLAB

**Data and ML** PyTorch · Transformers · PEFT (LoRA/QLoRA) · TRL · scikit-learn ·
PySpark · JAX · pandas · NumPy · statsmodels

**Engineering** Django · FastAPI · PostgreSQL · Redis · Docker · Vue 3 · pytest ·
Git · GitHub Actions

**Statistics** survival analysis (Kaplan-Meier, Cox, AFT) · experiment design and
power analysis · imbalanced classification · calibration · maximum likelihood

**Spoken languages** English (native) · Bengali (fluent)
