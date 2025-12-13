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
| Chen Yuewei      | Demonstrating exceptional capabilities in data acquisition and possessing extensive financial expertise, proficient in deploying code to extract relevant financial datasets.                       | Sourced data through custom web scrapers from public sources. |
| Lei Weng I       | Skilled in English public speaking, with a clear narrative logic; adept at using video format to condense the key points of reports, enhance information efficiency, and improve readability and visual impact.                                 | Delivered the project presentation and demo video, clearly communicating motivation, methodology, and key insights |
| Ma Yining        | Possesses extensive financial expertise and the ability to identify financial issues and develop analytical frameworks for addressing related problems                | Established the project theme and authored the technical README |
| Situ Waner       | Demonstrates extensive expertise in statistical analysis, data modeling, and front-end visualization architecture     | Designed and implemented interactive, publication-ready visualizations using Plotly and Matplotlib |
| Wu Suizhu        | Combine statistics and business logic to clean data, and achieve smooth collaboration with clear and reproducible code                           | Prepared analysis-ready datasets through systematic data cleaning |

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


### 🛠️ Feature Engineering Highlights
- `revenue_per_employee = TotalRevenue / Employees`
- `marketcap_per_employee = MarketCap / Employees`
- `annual_return = (YearEnd AdjClose / YearStart AdjClose) - 1`
- Event flags for AI milestones (e.g., Blackwell launch, ChatGPT integration)
- Sector-adjusted excess returns

🧹 **Data Cleaning Summary**  
- Missing employee counts imputed via forward-fill from latest SEC 10-K filing  
- Duplicate stock price entries (from yfinance timestamp collisions) removed  
- All steps logged in `notebooks/01_data_cleaning.ipynb` for full reproducibility

We prioritized **economic interpretability** over model complexity.

---

## 📈 D. Analysis & Visualization

### 🔬 Core Insights  
- **NVDA’s 2023 leap**: 80%+ of market cap growth came from **efficiency gains**, not hiring (employees +53%, market cap per employee +8x).  
- **Layoff paradox**: META and AMZN saw **stock surges post-layoffs** (+394%, +167%), but only because they paired cuts with **AI transformation**. INTC cut staff yet declined—proof that **layoffs alone don’t drive value**.  
- **Structural bifurcation**: AI cohort (NVDA, MSFT, META, etc.) delivered **+300% avg returns (2023–2024)**; traditional tech averaged **–15%**. This is not cyclical—it’s **industrial realignment**.

### 🖼️ Visualization Approach 

To deeply reveal the market dynamics behind the AI revolution and the layoff paradox, we have designed the following 7 types of data visualizations, all programmatically generated through code (using Plotly / Matplotlib / Seaborn) to ensure reproducibility and depth of analysis:

| Chart Type | Analysis Objective | Tool | Output Sample |
|------------|--------------------|------|---------------|
| **Calendar Heatmap** | Show daily return intensity from 2021–2024, highlighting key AI event windows (e.g., NVDA Blackwell launch in May 2023) | Plotly | [Calendar Heatmap](images/calendar_heatmap.png) |
| **Animated Bubble Plot** | Dynamically track the evolution of "market value per capita" vs. "cumulative returns" over time, emphasizing NVDA's efficiency leap and INTC's stagnation | Plotly | [Animated Bubble Plot](images/animated_bubble.gif) |
| **Grouped Bar Chart** | Compare performance differences between "laying-off companies" (META, AMZN, INTC) and "non-laying-off companies" (NVDA, MSFT) from 2022–2024 | Matplotlib | [Grouped Bar Chart](images/grouped_bar.png) |
| **Scatter Plot** | Reveal the nonlinear relationship between "employee change rate" and "market value growth rate", validating that "efficiency ≠ layoffs" | Seaborn | [Scatter Plot](images/scatter_efficiency.png) |
| **Annotated Time Series** | Annotate stock price curves with key events: layoff announcements, AI model launches, earnings days, explaining market reactions | Matplotlib | [Annotated Time Series](images/annotated_timeline.png) |
| **Boxplot by Sector** | Statistically test for significant differences in earnings distribution between the "AI camp" (NVDA, MSFT, META, etc.) and "traditional tech" (INTC, IBM, etc.) from 2023–2024 | SciPy + Plotly | [Boxplot by Sector](images/sector_boxplot.png) |
| **4-Year Trend Grid** | Present stock price trends of 10 companies from 2021–2024 in a grid format, visually demonstrating structural divergence | Matplotlib | [4-Year Trend Grid](images/four_year_grid.png) |

> 💡 **All charts are based on an integrated dataset**:  
> - Daily stock prices (from Yahoo Finance)  
> - Annual employee numbers & market values (SEC filings + company reports)  
> - Layoff event logs (public news + Layoffs.fyi)  
> - AI milestone events (product launches, earnings calls, model open-sourcing)


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
<img width="2680" height="1130" alt="tongyi-mermaid-2025-12-14-042353" src="https://github.com/user-attachments/assets/eb5e84aa-78a1-4b43-92af-4d1f2771bf7f" />

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
| Data Retrieval         | `yfinance`,Jupyter, manual curation, ethical web scraping |
| Data Processing        | `pandas`, `numpy` |
| Statistical Analysis   | `scipy.stats`, custom regression |
| Visualization          | `plotly` (interactive), `matplotlib`, `seaborn` |
| Reproducibility        | Git, Jupyter, documented workflows |


## 🤖 AI-Assisted Development

This project leveraged AI tools (e.g., Qwen, GitHub Copilot) for:
- Code debugging and error resolution (e.g., Git authentication, Mermaid syntax)
- Directory structure optimization
- README documentation drafting and formatting
- Workflow automation suggestions

All final code, logic, and decisions were reviewed, validated, and refined by the authors.


---

> ℹ️ **Disclaimer**: For educational purposes only. Not investment advice.  
> © 2025 CISC7201 Group Q | University of Macau








