# 📊 CISC7201 Data Science Programming — Final Project  
## Does Human Capital Efficiency Drive Market Valuation?  
### The Paradox of AI Boom and Mass Layoffs in Tech Stocks (2021–2024)

> An empirical analysis of workforce productivity, AI adoption, and stock performance across tech giants during a period of historic divergence.

---

## 🔍 A. Motivation & Team Background

### 💡 Why This Matters  
Between 2021 and 2024, the tech sector experienced unprecedented divergence: NVIDIA’s market cap exploded by **12x** to $4.3 trillion, while Intel’s fell by **25%**. Simultaneously, companies like Meta and Amazon laid off **over 100,000 workers**—yet saw their stock prices surge.  

This project investigates a critical paradox:  
> **Did mass layoffs genuinely improve human capital efficiency—or did the AI revolution simply mask underlying operational weaknesses?**

We ask:  
> **Can metrics like market cap per employee explain why NVIDIA thrived while others stagnated or collapsed?**

This question sits at the intersection of finance, labor economics, and technological disruption—making it ideal for an end-to-end data science investigation.

### 👥 Our Team  
| Name             | Role & Strength                                      | Contribution |
|------------------|------------------------------------------------------|--------------|
| Chen Yuewei      | Python Pipelines & Time Series                       | Sourced data through custom web scrapers from public sources. |
| Lei Weng I       | Statistical Modeling                                 | Delivered the project presentation and demo video, clearly communicating motivation, methodology, and key insights. |
| Ma Yining        | Financial Analysis & Domain Expertise                | Established the project theme and authored the technical README. |
| Situ Waner       | Statistical Analysis & Interactive Visualization     | Designed and implemented interactive, publication-ready visualizations using Plotly and Matplotlib. |
| Wu Suizhu        | Financial Domain Expertise                           | Prepared analysis-ready datasets through systematic data cleaning. |

Our diverse skills enabled a full-stack approach—from raw filings to visual insight.

---

## 🗃️ B. Data Collection (Original Sources Only)

We built three custom datasets—no benchmark or Kaggle defaults:

| Source               | Method                              | Coverage |
|----------------------|-------------------------------------|----------|
| Daily Stock Prices   | `yfinance` API                      | AAPL, MSFT, GOOGL, NVDA, META, AMZN, TSLA, AMD, INTC, JNJ (2021–2024) |
| Annual Fundamentals  | Manual extraction from SEC 10-Ks     | Revenue, Employees, Market Cap (2021–2024) |
| Layoff Events        | Curated news & press releases       | Binary flags + employee change % (2022–2023) |

✅ All data collected programmatically or via structured logging—fully reproducible.

---

## ⚙️ C. Data Engineering & Cleaning

### 🔧 Key Pipeline Steps

<img width="3445" height="1506" alt="tongyi-mermaid-2025-12-14-012249" src="https://github.com/user-attachments/assets/bbb29155-69dc-4dce-af12-d26780b06a5c" />


> _Diagram generated from the following Mermaid source (editable):_

```mermaid
graph LR
A[Raw CSV/API] --> B(Clean Dates & Types)
B --> C(Handle Missing/Outliers)
C --> D{Align Temporal Granularity}
D --> E[Annual Panel Dataset]
E --> F[Feature Engineering]
F --> G[Efficiency Metrics]
G --> H[Analysis-Ready Table]

### 🛠️ Feature Engineering Highlights
- `revenue_per_employee = TotalRevenue / Employees`
- `marketcap_per_employee = MarketCap / Employees`
- `annual_return = (YearEnd AdjClose / YearStart AdjClose) - 1`
- Event flags for AI milestones (e.g., Blackwell launch, ChatGPT integration)
- Sector-adjusted excess returns

We prioritized **economic interpretability** over model complexity.

---

## 📈 D. Analysis & Visualization

### 🔬 Core Insights  
- **NVDA’s 2023 leap**: 80%+ of market cap growth came from **efficiency gains**, not hiring (employees +53%, market cap per employee +8x).  
- **Layoff paradox**: META and AMZN saw **stock surges post-layoffs** (+394%, +167%), but only because they paired cuts with **AI transformation**. INTC cut staff yet declined—proof that **layoffs alone don’t drive value**.  
- **Structural bifurcation**: AI cohort (NVDA, MSFT, META, etc.) delivered **+300% avg returns (2023–2024)**; traditional tech averaged **–15%**. This is not cyclical—it’s **industrial realignment**.

### 🖼️ Visualization Approach  
| Chart Type                     | Purpose                                                                 | Tool         |
|-------------------------------|-------------------------------------------------------------------------|--------------|
| Calendar Heatmap              | Show daily return intensity during AI inflection points (e.g., May 2023) | Plotly       |
| Animated Bubble Plot          | Track efficiency (market cap/employee) vs. return over time             | Plotly       |
| Grouped Bar Chart             | Compare post-layoff vs. non-layoff firm performance                     | Matplotlib   |
| Scatter Plot                  | Employee change % vs. market cap growth                                 | Seaborn      |
| Annotated Time Series         | Highlight key events (layoffs, AI launches) on price trends             | Matplotlib   |
| Boxplot by Sector             | Statistically test divergence between AI and legacy tech                 | SciPy + Plotly |

All visuals built programmatically—no drag-and-drop tools.

---

## 🧭 E. Conclusion & Reflection

### ✅ Key Takeaways  
- **Human capital efficiency is a leading indicator** of long-term valuation—but **only when aligned with strategic innovation** (e.g., AI).  
- **"Doing more with less" works for AI leaders** (NVDA, MSFT), but **fails for laggards** (INTC) lacking new growth engines.  
- **Data fusion** (daily prices + annual fundamentals + event logs) reveals dynamics invisible to traditional financial analysis.

### ⚠️ Limitations  
- Limited to 4 years of fundamental data (2021–2024).  
- Employee counts are year-end snapshots; intra-year fluctuations are smoothed.  
- Layoff data relies on public announcements; actual timing may vary.

### 🌱 What We Learned  
> “This project taught us that clean, well-engineered data is more valuable than complex models—and that the biggest market shifts often hide in plain sight.”  
> — Team Reflection  

**Future work**: Integrate R&D spend, use NLP on earnings calls, or build a predictive "AI-readiness" score.

---

## 📦 Deliverables  
```text
project-root/
├── data/
│   ├── raw/              # Original downloads
│   └── processed/        # Clean panel dataset (2021–2024)
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_feature_engineering.ipynb
│   └── 03_visualization.ipynb
├── presentation/
│   ├── slides.pdf
│   └── demo.mp4
└── README.md ← You are here
```

---

## 🧰 Technical Stack  
| Purpose                | Tools & Libraries |
|------------------------|-------------------|
| Data Retrieval         | `yfinance`, manual curation, ethical web scraping |
| Data Processing        | `pandas`, `numpy` |
| Statistical Analysis   | `scipy.stats`, custom regression |
| Visualization          | `plotly` (interactive), `matplotlib`, `seaborn` |
| Reproducibility        | Git, Jupyter, documented workflows |

No AutoML or off-the-shelf pipelines — all code written from scratch.

---

> ℹ️ **Disclaimer**: For educational purposes only. Not investment advice.  
> © 2025 CISC7201 Team | University of Macau


