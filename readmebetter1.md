# 📊 CISC7201 Data Science Programming — Final Project  
## Does Human Capital Efficiency Drive Market Valuation?  
### The Paradox of AI Boom and Mass Layoffs in Tech Stocks (2021–2024)

> An empirical analysis of workforce productivity, AI adoption, and stock performance across tech giants during a period of historic divergence.

---

## 🔍 A. Motivation & Team Background

### 💡 Why This Matters  
Between 2021 and 2024, the tech sector experienced unprecedented divergence:  
- NVIDIA’s market cap exploded by **12x** to $4.3 trillion  
- Intel’s fell by **25%**  
- Meta and Amazon laid off **over 100,000 workers**—yet saw stock prices surge  

This project investigates a critical paradox:  
> **Did mass layoffs genuinely improve human capital efficiency—or did the AI revolution simply mask underlying operational weaknesses?**

We aim to answer four core questions:  
1. How did return volatility and performance evolve over time (2021–2024)?  
2. Which firms emerged as “AI winners,” and how large was the cross-company divergence?  
3. Do fundamentals (profitability, efficiency) align with market valuations?  
4. Is there an **empirical association** between layoffs (and AI adoption) and subsequent stock outperformance?

This sits at the intersection of finance, labor economics, and technological disruption—making it ideal for an end-to-end data science investigation.

### 👥 Our Team  
| Name             | Role & Strength                                      | Contribution |
|------------------|------------------------------------------------------|--------------|
| Chen Yuewei      | Demonstrating exceptional capabilities in data acquisition and possessing extensive financial expertise, proficient in deploying code to extract relevant financial datasets.                       | Sourced data through custom web scrapers from public sources. |
| Lei Weng I       | Skilled in English public speaking, with a clear narrative logic; adept at using video format to condense the key points of reports, enhance information efficiency, and improve readability and visual impact.                                 | Delivered the project presentation and demo video, clearly communicating motivation, methodology, and key insights |
| Ma Yining        | Possesses extensive financial expertise and the ability to identify financial issues and develop analytical frameworks for addressing related problems                | Established the project theme and authored the technical README and PPT |
| Situ Waner       | Demonstrates extensive expertise in statistical analysis, data modeling, and front-end visualization architecture     | Designed and implemented interactive, publication-ready visualizations using Plotly and Matplotlib |
| Wu Suizhu        | Combine statistics and business logic to clean data, and achieve smooth collaboration with clear and reproducible code                           | Prepared analysis-ready datasets through systematic data cleaning |

Our diverse skills enabled a full-stack approach—from raw filings to visual insight.

---

## 🗃️ B. Data Collection (Original Sources Only)

We built three custom datasets—**no benchmark or Kaggle defaults**:

| Source | Method | Coverage |
|--------|--------|----------|
| Daily Stock Prices | `yfinance.download()` in `notebooks/00_data_fetch.py` | AAPL, MSFT, GOOGL, NVDA, META, AMZN, TSLA, AMD, INTC, JNJ (2021–2024) |
| Annual Fundamentals | Parsed from SEC EDGAR company facts API (`https://data.sec.gov`) using JSON traversal in `notebooks/00_data_fetch.py` | Revenue, Employees, Market Cap (2021–2024) |
| Layoff & AI Events | Manually curated from public news articles, press releases, and earnings call transcripts; logged in `data/events_log.csv` with source URLs and timestamps | Binary flags + employee change % (2022–2023); AI milestones (e.g., ChatGPT launch, Blackwell announcement) |

✅ Every source is traceable to a script (`notebooks/00_data_fetch.py`) or a versioned log (`data/events_log.csv`), enabling full end-to-end reproducibility.  
ℹ️ Event data required manual curation due to the lack of open, reliable APIs for tech layoff/AI announcements—each entry includes a verifiable source.

## ⚙️ C. Data Engineering & Cleaning

### 🔧 Key Pipeline Steps

Raw Data → Cleaning → Feature Engineering → Analysis

│            │              │

├─ yfinance  ├─ Forward-fill├─ marketcap_per_employee

├─ SEC 10-K  ├─ Deduplication├─ AI event flags

└─ Layoff logs└─ Year-end alignment└─ Sector-adjusted returns


### 🛠️ Feature Engineering Highlights
```python
revenue_per_employee = TotalRevenue / Employees  
marketcap_per_employee = MarketCap / Employees  
annual_return = (YearEnd AdjClose / YearStart AdjClose) - 1
```
- Event flags for AI milestones (Blackwell launch, ChatGPT integration)
- Sector-adjusted excess returns

### 🧹 Data Cleaning Summary 
- Missing employee counts filled via forward-fill from the most recent SEC 10-K filing (no interpolation or modeling)
- Duplicate stock price entries (from yfinance timestamp collisions) removed  
- All steps logged in `notebooks/01_data_cleaning.ipynb` for full reproducibility

We prioritized **economic interpretability** over model complexity.

---

## 📈 D. Analysis & Visualization

### 🔬 Core Insights  
- **NVDA’s 2023 leap**: 80%+ of market cap growth came from efficiency gains (employees +53%, market cap per_employee +8x) **(2023 only)**.  
- **Layoff paradox**: META and AMZN surged post-layoffs (+394%, +167% **from 2022Q4–2024**)—but only because cuts were paired with AI transformation. INTC cut staff yet declined.  
- **Structural bifurcation**: AI cohort (NVDA, MSFT, META) delivered +300% avg returns (**2023–2024**); traditional tech averaged –15% (**same period**). This is industrial realignment—not cyclicality.

### 🖼️ Data Visualization Approach

To deeply reveal the market dynamics behind the AI revolution and the layoff paradox, we designed the following 7 types of data visualizations, all programmatically generated (no GUI tools):

| Chart Type | Analysis Objective | Tool | Description |
|------------|--------------------|------|-------------|
| **Calendar Heatmap** | Show daily return intensity (2021–2024), highlighting AI event windows (e.g., NVDA Blackwell launch) | Plotly (for interactivity and hover tooltips) | Visualizes the temporal concentration of stock return volatility, with spikes aligned to major AI-related announcements. |
| **Animated Bubble Plot** | Track "market cap per employee" vs. "cumulative returns" over time | Plotly (supports smooth animation + responsive scaling) | Animates the evolution of human capital efficiency and market performance across firms from 2021 to 2024. |
| **Grouped Bar Chart** | Compare laying-off (META, AMZN, INTC) vs. non-laying-off firms (NVDA, MSFT) | Matplotlib (for precise layout control in publication-ready figures) | Compares post-2022 financial and efficiency metrics between firms that enacted large layoffs and those that did not. |
| **Scatter Plot** | Reveal nonlinear relationship: employee change rate vs. market value growth | Seaborn (for built-in regression trends and statistical aesthetics) | Examines whether reductions in workforce size correlate with increases in market valuation, including confidence intervals. |
| **Annotated Time Series** | Overlay key events (layoffs, AI launches) on price curves | Matplotlib (fine-grained control over annotations and axes) | Plots normalized stock prices with vertical markers and labels for verified layoff dates and AI milestone events. |
| **Boxplot by Sector** | Test return distribution differences: AI cohort vs. legacy tech | Plotly + SciPy (interactive boxplots with statistical test results) | Displays the distribution of annualized returns for AI-focused firms versus traditional semiconductor or hardware companies, annotated with p-values from t-tests. |
| **4-Year Trend Grid** | Visualize structural divergence across 10 companies | Matplotlib (subplots for consistent multi-company comparison) | Presents a 2×5 grid of standardized time series (e.g., market cap, employees, returns) to highlight divergent trajectories across the full sample. |

> 💡 **All charts are based on an integrated dataset**:  
> - Daily stock prices (from Yahoo Finance)  
> - Annual employee numbers & market values (SEC filings + company reports)  
> - Layoff event logs (public news + Layoffs.fyi)  
> - AI milestone events (product launches, earnings calls, model open-sourcing)

### 🌐 Interactive Narrative Layer (Frontend)
Rejecting drag-and-drop dashboards (e.g., Tableau, Power BI), we built a **fully code-based scroll-driven interactive website** (`index.html`) using:
- **d3.js v5** for dynamic visual encoding and DOM manipulation
- **Custom GridMap** (`gridmap.js`) for company tile mapping and state transitions
- **Scroll-linked sections** (`scroller.js`) to guide users through 11 analytical narratives  
Each section answers one question—from macro context (#2) to event timelines (#10)—creating a cohesive story that blends **quantitative rigor** with **human-centered design**, all implemented in raw HTML/CSS/JavaScript.

---

## 🧭 E. Conclusion & Reflection

### ✅ Key Takeaways
- Human capital efficiency is a leading indicator of long-term valuation—but **only when aligned with strategic innovation** (e.g., AI).
- "Doing more with less" works for AI leaders (NVDA, MSFT), but fails for laggards (INTC) lacking new growth engines.
- **Data fusion** (daily prices + annual fundamentals + event logs) reveals dynamics invisible to traditional financial analysis.

### ⚠️ Limitations  
- Limited to 4 years of fundamental data (2021–2024).  
- Employee counts are year-end snapshots; intra-year fluctuations are smoothed.  
- Layoff data relies on public announcements; actual timing may vary.

### 🌱 What We Learned  
> “This project taught us that writing robust data pipelines in code is more valuable than off-the-shelf dashboards—and that clean, well-engineered data reveals insights no black-box model can. The biggest market shifts often hide in plain sight.”

### 🔮 Future Work
Building on our current pipeline (`notebooks/02_feature_engineering.ipynb`), future work could include:
- Integrate R&D spend to measure innovation intensity  
- Apply NLP to earnings call transcripts for “AI commitment” scoring  
- Build a predictive “AI-readiness” index for tech firms

---

## 📦 Deliverables  

project-root/
├── data/
│   ├── raw/              # Original downloads (Yahoo Finance, SEC filings, layoff logs)
│   └── processed/        # Clean panel dataset (2021–2024)
├── notebooks/
│   ├── 01_data_cleaning.ipynb      # Forward-fill employees, remove yfinance duplicates
│   ├── 02_feature_engineering.ipynb # marketcap_per_employee, AI event flags
│   └── 03_visualization.ipynb      # Calendar heatmap, bubble plot, etc.
├── presentation/
│   ├── 7201GroupQ.pdf        # 10–12 minute presentation
│   └── demo.mp4          # Recorded walkthrough with live visualization demo
│   # └── Web Narrative: https://situwaner-q.github.io/tech-stock-analysis/  
└── README.md             # This document

### ▶️ Demo & Interactive Experience

- **[Project Presentation Slides](presentation/7201GroupQ.pdf)** – Summarizes our motivation, methodology, and key findings.
- **[Full Demo Video (MP4, 10 min)](presentation/demo.mp4)** – Walkthrough of data pipeline, visualizations, and insights with live demo.
- **[Interactive Web Narrative](https://situwaner-q.github.io/tech-stock-analysis/)**

📦 Final Deliverables 
- `notebooks/`: Full analysis pipeline (cleaning → features → visualization)
- `presentation/slides.pdf`: 10–12 minute presentation slides
- `presentation/demo.mp4`: Recorded video walkthrough (see requirements below)
- `README.md`: This document
- `data/raw/`: Original unmodified downloads: Yahoo Finance price CSVs, SEC 10-K PDF/text extracts (employee & market cap), and curated layoff event logs from news/Layoffs.fyi
- `data/processed/`: Cleaned and merged panel dataset (2021–2024)

---

🧰 Technical Stack
| Purpose | Tools & Libraries | Why / How |
|--------|------------------|----------|
| Data Retrieval | `yfinance`, ethical web scraping, manual curation | Download daily prices; extract employee/market cap from SEC filings |
| Data Processing | `pandas`, `numpy` | Handle missing values, merge multi-source data, compute per-employee metrics |
| Statistical Analysis | `scipy.stats`, custom regression | Test significance of return differences between AI vs legacy tech sectors |
| Visualization | `plotly` (interactive), `matplotlib`, `seaborn` | Generate publication-ready charts with hover interactivity |
| Interactive Web Narrative | `d3.js`, HTML/CSS/JS, scroll-driven storytelling | Deploy scroll-linked visual narrative at GitHub Pages |
| Reproducibility | Git, Jupyter, documented workflows | Notebooks run end-to-end with relative paths; all dependencies listed in comments |

🤖 **AI-Assisted Development**  
This project leveraged AI tools (e.g., Qwen, GitHub Copilot) for code debugging, directory optimization, and documentation drafting. All final logic was reviewed and validated by the team.

ℹ️ **Disclaimer**: For educational purposes only. Not investment advice.  
© 2025 CISC7201 Group Q | University of Macau
```








