---
platform: universal
format: data-analysis
constraints:
  max_chars: null
  image_ratio: null
  max_hashtags: null
---

# Best Practices: Data Analysis and Reporting

## Core Principles

Data analysis turns raw numbers into decisions. The goal is not to describe what happened, but to explain why it happened and recommend what to do next.

- **Start with a question, not a dataset.** Analysis without a question produces observations, not insights.
- **Distinguish correlation from causation.** Two metrics moving together does not mean one causes the other.
- **Insight = What + So what.** "Conversions dropped 20%" is a finding. "Conversions dropped 20% because landing page load time increased after the deploy" is an insight.

## Analysis Process

### Step 1: Define the Question
- Business question: "Why did revenue drop in Q3?"
- Analytical question: "Which segment, channel, or product drove the Q3 revenue decline?"
- Success metric: "The analysis is complete when we can name the primary causal factor and its magnitude."

### Step 2: Data Collection and Validation
- Identify data sources and their freshness
- Check for null values, duplicates, and outliers
- Validate against a known baseline or external benchmark
- Document data limitations upfront

### Step 3: Exploratory Analysis
- Summarize distributions: mean, median, standard deviation
- Look for trends over time
- Segment by key dimensions (geography, product, cohort, channel)
- Identify anomalies and investigate their cause

### Step 4: Hypothesis Testing
- State a hypothesis: "We believe [X] caused [Y] because [Z]"
- Select appropriate statistical test (t-test, chi-square, regression)
- Set significance threshold (p < 0.05 for most business contexts)
- Interpret results — significance does not always mean practical importance

### Step 5: Visualization
- Choose chart type by relationship:
  - Trends over time: line chart
  - Comparisons: bar chart
  - Composition: stacked bar or pie (use pie only for 2–4 categories)
  - Distribution: histogram or box plot
  - Correlation: scatter plot

### Step 6: Communication
- Lead with the insight, not the methodology
- Use the "So What" test on every finding
- Present data in the audience's language, not the analyst's

## Structure (Analysis Report)

```
[EXECUTIVE SUMMARY — 3–5 bullet points max]
- The question
- The key finding
- The recommended action

[CONTEXT AND METHODOLOGY]
- Data sources, date range, sample size
- Limitations and caveats

[FINDINGS]
- Finding 1: [Insight + supporting data]
- Finding 2: ...
- [Charts and tables with clear titles and labeled axes]

[ROOT CAUSE ANALYSIS]
- Causal chain or contributing factors

[RECOMMENDATIONS]
- Action 1: [What to do] — Owner: [who] — Timeline: [when]
- Action 2: ...

[APPENDIX — raw tables, methodology detail]
```

## Guidelines

- Every chart must have: a title that states the insight (not just the metric), labeled axes, a data source note, and a date range.
- Never present a single number without context: comparison to prior period, target, or benchmark.
- Round numbers appropriately for the audience: executives get "~$2M", analysts get "$1,847,320."
- Avoid 3D charts — they distort perception of values.
- Confidence intervals: always show uncertainty in forecasts and statistical estimates.
- Reproducibility: document data sources, transformations, and calculations so the analysis can be replicated.
- For dashboards: limit to 5–7 KPIs per view; group related metrics; use consistent color coding.
