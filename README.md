# stc tv Viewer Analytics

An end-to-end data analytics project built on over 1 million real stc tv viewing events: cleaning and exploring the data, forecasting future demand, building a recommendation engine, and presenting the findings to a non-technical audience.

Completed as part of a data analytics internship (Misk Skills / stc Corporate Analytics and Data program).

## Overview

The project works through four stages, each building on the last:

1. **Data cleaning & exploratory analysis** — turning a messy raw export into a usable dataset and uncovering real viewing patterns
2. **Demand forecasting** — projecting future watch hours with Prophet
3. **Recommendation engine** — suggesting programs based on shared viewing behavior
4. **Data storytelling** — packaging the findings into a presentation for decision-makers

## Project Structure

```
├── notebooks/
│   ├── stctv_task1.ipynb        # Cleaning, feature engineering, viewer behavior analysis
│   ├── stctv_task2.ipynb       # Prophet-based time series forecast
│   └── stctv_task3.ipynb    # Collaborative filtering recommendation system
├── presentation/
│   └── stctv_task4.pptx # Final stakeholder-facing deck
└── README.md
```

> **Note on data:** the raw datasets used in this project were provided as part of the internship program and are not included in this repo, since they aren't mine to redistribute. The notebooks document the full analysis and are reproducible against the original files.

## 1. Data Cleaning & Exploratory Analysis

The raw export had program genre and title concatenated in a single field, an Excel serial-number date column, and inconsistent whitespace in program names. After cleaning:

- **1,048,575** viewing events across **11,578** unique users and **8,013** distinct programs
- **Movies vs. series:** movies draw 74% of viewers but only account for 29% of total watch hours; series draw 26% of viewers but generate 71% of watch hours, a much smaller but far more engaged audience
- **HD vs. SD:** movie viewers lean toward HD (64%), while series viewers lean toward SD (56%), a pattern worth investigating further (bandwidth conservation during binge sessions, device type, or HD content availability)
- **Most-watched titles:** animated family films dominate the top 10, led by *The Boss Baby*

## 2. Demand Forecasting

Built a Prophet model to project total daily watch hours two months ahead.

- Training data covered January–April 2018 but had **zero records for any Saturday or Sunday**, discovered while validating the model rather than assumed. Weekly seasonality was disabled in the model since there was no real evidence to support it.
- The forecast shows a continued downward trend in watch hours, but this comes with a caveat: the training window is only 4 months long, so the model has no prior summer to learn from, and real viewership in the forecast period is likely higher than shown due to seasonal effects (school break, vacations) the model can't see.

## 3. Recommendation Engine

Built an item-based collaborative filtering system using cosine similarity, comparing three different signals:

- **Explicit ratings** (1–4 scale)
- **Implicit engagement**, derived from watch duration relative to each program's typical (median) watch time
- **A blended model** averaging both signals

All three approaches converged on nearly the same result. For example, viewers who watched *Moana* were recommended *Trolls*, *Surf's Up: WaveMania*, *The Mermaid Princess*, and *The Boss Baby* — every one an animated family title, despite the model never being told the genre.

## 4. Presentation

The final deliverable is a slide deck translating these findings into recommendations for the stc tv team: fixing the weekend data gap, preparing for a likely summer demand increase, investigating the series HD gap, and deploying the recommendation engine platform-wide.

## Tools & Techniques

`pandas` · `numpy` · `plotly` · `Prophet` · `scikit-learn` (cosine similarity) · `pptxgenjs`

## Author

Turki Almuayli — [LinkedIn](https://linkedin.com/in/turki-almuayli-264525409/) · [GitHub](https://github.com/TurkiAlMuayli)
