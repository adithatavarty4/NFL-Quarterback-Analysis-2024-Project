# NFL Quarterback Performance Index (2024)

This data science project analyzes NFL quarterback performance against contract valuation for the 2024 season. By developing a custom **QB Performance Index (QPI)** that blends traditional production metrics with a situational "clutch factor," this analysis identifies which quarterbacks over- or under-performed relative to their market value.

---

## Project Overview

While NFL franchises commit hundreds of millions of dollars to the quarterback position, contract values are historically driven by raw volume metrics (passing yards and touchdowns) rather than efficiency or situational success.

This project integrates play-by-play data, contract tracking, and historical game logs to evaluate player valuation. Our findings highlight a distinct disconnect between what franchises pay for (volume) and what correlates most heavily with winning (efficiency and high-leverage execution).

### Key Insights

- **Salary Drivers:** Multi-variable linear regression indicates that total passing yardage remains the primary driver of QB compensation, while situational/clutch performance is significantly undervalued in contract negotiations.
- **Quarterback Archetypes:** K-Means clustering identifies three distinct tiers of active QBs: backup/low-volume distributors, traditional pocket passers, and elite dual-threat franchise anchors.
- **Market Valuation:** The final QPI metrics successfully isolate undervalued assets (positive QPI) from overvalued contracts (negative QPI) after adjusting for cap hit.

---

## Project Structure

```text
QB-Performance-Index/
├── README.md
├── requirements.txt
├── notebooks/
│   └── quarterback_analysis.ipynb
├── visuals/
│   ├── qpi_rankings.png
│   ├── salary_distribution.png
│   └── kmeans_clusters.png
└── docs/
    ├── executive_summary.pdf
    └── final_presentation.pptx
```

---

## Data Sources

| Source | Description | Acquisition Method |
|---|---|---|
| NFL Savant | 2024 play-by-play tracking data | Local CSV import |
| Spotrac | Active QB contract and salary data | Web scraping (BeautifulSoup) |
| ESPN API | Individual player game logs & seasonal stats | REST API requests |

---

## Installation & Execution

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/QB-Performance-Index.git
cd QB-Performance-Index
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the Notebook

```bash
jupyter notebook notebooks/Phase\ III.ipynb
```

---

## Note on Data Pipelines

The underlying web scrapers require an active internet connection.

Execute the data collection functions sequentially within the notebook:

- `data_parser()`
- `web_parser1()`
- `web_parser2()`

This populates the local cache before running the analysis modules.

---

## Methodology & QPI Formula

To evaluate overall efficiency, all individual metrics are converted to standard scores ($z$-scores) relative to the 2024 active quarterback population.

The raw performance score is calculated using:

```math
\text{Performance Score} =
0.15(\text{Yds}_z)
+ 0.15(\text{Comp}\%_z)
+ 0.25(\text{TD}_z)
- 0.20(\text{INT}_z)
+ 0.05(\text{RushTD}_z)
+ 0.05(\text{RushYds}_z)
+ 0.15(\text{Clutch}_z)
```

The final QB Performance Index (QPI) applies a non-linear salary penalty:

```math
\text{QPI} =
\frac{\text{Performance Score}}
{\text{Salary Weight}}
```

This adjustment ensures that higher-paid quarterbacks must maintain elite efficiency to generate positive value scores.

---

## Tech Stack

### Core Data Pipeline
- Python
- pandas
- numpy
- requests
- BeautifulSoup

### Modeling & Machine Learning
- scikit-learn
  - Linear Regression
  - K-Means Clustering

### Visualization
- plotly
- matplotlib

---

## Authors

Georgia Institute of Technology — CS 2316 (Group 98)
