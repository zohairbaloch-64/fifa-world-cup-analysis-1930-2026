# 🏆 The Ultimate FIFA World Cup Analysis (1930–2026)

An end-to-end data analysis of 96 years of World Cup football — every match, every goal, every penalty kick, and the road to the newly-expanded 2026 tournament — built with the **PACE** framework (Plan → Analyze → Construct → Execute).

**[View the notebook on Kaggle](https://www.kaggle.com/zohairbaloch)** · **[GitHub](https://github.com/zohairbaloch-64)** · **[LinkedIn](https://www.linkedin.com/in/zohair-baloch-data-analyst)**

---

## 📌 Project Overview

This project merges five independent public data sources into a single analytical base to answer six questions:

1. How has scoring and match volume evolved across 23 tournaments (1930–2026)?
2. Which nations have historically dominated on goals and appearances?
3. How are matches actually decided — regular time, extra time, or penalties — and has that changed over time?
4. What does the 2026 squad landscape look like: average age, club diversity, position mix?
5. Are penalty shootouts really a lottery, or does pressure, kick order, and scoreline matter?
6. Can a machine learning model meaningfully predict whether a penalty kick is scored?

## 🗂️ Data Sources

| File | Grain | Size |
|---|---|---|
| `world_cup_matches.csv` | 1 row per match, 1930–2026 | 1,074 × 10 |
| `world_cup_2026_squads.csv` | 1 row per registered player, 2026 | 1,248 × 7 |
| `team_summaries_2026.csv` | 1 row per 2026-qualified nation | 48 × 5 |
| `country_iso_mapping.csv` | Country → ISO-3 code (for maps) | 48 × 2 |
| `wc_penalty_shootouts.xlsx` | 1 row per individual penalty kick, 1982–2026 | 352 × 13 |

Original dataset: [The Ultimate FIFA World Cup Dataset (1930–2026)](https://www.kaggle.com/datasets/eshaansunthankar2/the-ultimate-fifa-world-cup-dataset-1930-2026/data) on Kaggle.

## 🧹 Data Quality & Cleaning

The raw data was audited before analysis, and the following issues were found and fixed:

- **16 exact duplicate rows** in the match data — dropped.
- **33 raw `Stage` labels** (e.g. `"Group A"`, `"Group 1"`, `"group stage"`, `"Group Stage"`) collapsed into **7 consistent categories**.
- **94 unplayed 2026 fixtures** (no kickoff datetime, placeholder 0–0 score) identified and excluded from all historical scoring statistics.
- **Inconsistent outcome labels** in the penalty shootout file (`"Miss"` vs. `"Missed"`) merged into one category.
- Win-condition text parsed into a clean `Decided_By` field (Regular time / Extra Time / Penalties).

## 📊 Analysis & Key Findings

### Tournament history
- The World Cup has grown roughly **5.7×** in matches since 1930 (18 → 64 matches), and 2026 will expand further with 48 teams.
- Goals-per-match has steadily declined from **~3.89 in 1930 to ~2.69 in 2022**, reflecting more tactically disciplined, defensively organized football.
- **Brazil, Argentina, and France** are the top 3 all-time goal scorers among 2026-qualified nations.
- Only **3.6% of all historical matches** have ever been decided by a penalty shootout.

### Road to 2026
- Average squad age across the 48 qualified nations ranges from **25.3 years (Ivory Coast)** to **30.0 years (Panama)**.
- **Centre-back is the most-registered position** (234 of 1,248 players) — every squad prioritizes defensive depth.
- **Sweden and Cape Verde** field the most "globalized" squads, with players drawn from 26 different clubs each.

### Penalty shootouts
- Overall conversion rate across 352 kicks: **69.0%** — roughly 1 in 3 kicks is not scored.
- The standout finding: **"must-score" kicks convert at only 17.6%**, versus **71.6%** for routine kicks — clear evidence that pressure is real, even in a small sample.
- **Harald Schumacher** holds the record for most World Cup penalty saves by a goalkeeper in this dataset.

### Predictive modeling (XGBoost + SHAP)
- A classifier trained to predict individual penalty outcomes (kick order, scoreline margin, pressure flag, match stage) achieved **ROC-AUC ≈ 0.55** — barely better than chance.
- This is reported as an honest finding, not a shortcoming of the modeling: it confirms, rather than contradicts, the EDA — penalty outcomes are dominated by factors outside this dataset (technique, goalkeeper positioning, nerve).
- SHAP analysis confirms `Is_Must_Score` is the single strongest (though still modest) predictive feature, consistent with the conversion-rate gap found above.

## 🛠️ Tech Stack

- **Python**: pandas, NumPy
- **Visualization**: Matplotlib, Seaborn, Plotly (interactive choropleth map)
- **Machine Learning**: scikit-learn, XGBoost
- **Explainability**: SHAP

## 📁 Repository Structure

```
├── FIFA_World_Cup_Analysis_1930_2026.ipynb   # Full analysis notebook
├── data/
│   ├── world_cup_matches.csv
│   ├── world_cup_2026_squads.csv
│   ├── team_summaries_2026.csv
│   ├── country_iso_mapping.csv
│   └── wc_penalty_shootouts.xlsx
└── README.md
```

## ▶️ How to Run

```bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn xgboost shap
jupyter notebook FIFA_World_Cup_Analysis_1930_2026.ipynb
```

The notebook expects the data files in a `data/` subfolder relative to itself (as structured above).

## 👤 Author

**Zohair Baloch** — Data Analyst, focused on remote-ready roles with international teams.

- 📊 Kaggle: [kaggle.com/zohairbaloch](https://www.kaggle.com/zohairbaloch)
- 💻 GitHub: [github.com/zohairbaloch-64](https://github.com/zohairbaloch-64)
- 🔗 LinkedIn: [linkedin.com/in/zohair-baloch-data-analyst](https://www.linkedin.com/in/zohair-baloch-data-analyst)

If this project was useful, an upvote on Kaggle or a star on GitHub is appreciated.
