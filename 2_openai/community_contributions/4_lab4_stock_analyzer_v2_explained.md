# Stock Analyzer v2 Notebook: Explanation

This document explains the structure, workflow, and main components of the `4_lab4_stock_analyzer_v2.ipynb` notebook. The notebook demonstrates an agentic approach to deep stock analysis, combining multiple data sources and tools to generate a comprehensive report and email it to the user.

---

## 1. **Overview**

The notebook orchestrates a multi-agent workflow to:
- Gather the latest news for a stock ticker
- Analyze stock performance and generate visualizations
- Fetch enriched company information
- Synthesize all data into a detailed markdown report
- Email the report (with a performance chart) to the user

---

## 2. **Imports and Setup**

The notebook imports:
- Custom agent framework (`Agent`, `Runner`, etc.)
- Data science and plotting libraries (`yfinance`, `pandas`, `matplotlib`, `seaborn`)
- Email sending libraries (`brevo_python`)
- Utility libraries (`dotenv`, `os`, `requests`, etc.)

It loads environment variables (API keys) and initializes the Alpaca API for news retrieval.

---

## 3. **Helper Functions and Tools**

### a. **get_domain_from_ticker**
Extracts the company website domain from a ticker using `yfinance`.

### b. **@function_tool Decorators**
Defines tools that agents can use:
- `get_stock_news`: Fetches recent news for a ticker using Alpaca
- `get_stock_performance`: Gets price/volume data and summary stats using yfinance
- `get_company_info`: Fetches company info from the Abstract API using the domain

### c. **Plotting Functions**
- `create_performance_chart`: Shows a matplotlib chart in the notebook
- `create_chart_for_email`: Generates a base64-encoded PNG for embedding in emails

---

## 4. **Agent Definitions**

### a. **News Agent**
Summarizes the latest news for a ticker.

### b. **Performance Agent**
Analyzes stock price/volume data and returns summary statistics.

### c. **Company Info Agent**
Fetches and summarizes company-level data (industry, location, social links, etc.).

### d. **Analysis Agent**
Synthesizes all data (ticker, company info, news, performance) into a detailed markdown report, following a structured template (executive summary, news, technical analysis, risk, recommendation).

### e. **Email Agent**
Sends the final report as a styled HTML email, optionally including the performance chart.

---

## 5. **Orchestration Functions**

- `get_stock_news_data`: Runs the news agent
- `get_stock_performance_data`: Runs the performance agent
- `get_company_info_data`: Extracts the domain and runs the company info agent
- `write_stock_report`: Runs the analysis agent, passing all gathered data
- `send_stock_report`: Converts the markdown report to HTML, embeds the chart, and sends the email

---

## 6. **Main Workflow Cell**

The main cell demonstrates the full workflow:
1. **Set ticker and period** (e.g., `ticker = "AAPL"`, `period = "6mo"`)
2. **Run agents in parallel** to fetch news, performance, and company info
3. **Display the performance chart** in the notebook
4. **Generate the markdown report** using the analysis agent
5. **Send the report via email** (with the chart embedded)
6. **Display the markdown report** in the notebook

---

## 7. **Email Content**

- The email includes the full markdown report (converted to HTML), which contains:
  - Company info
  - Executive summary
  - News analysis
  - Technical performance analysis
  - Risk assessment
  - Investment recommendation
- The performance chart is embedded as an image in a dedicated section of the email.

---

## 8. **Extending the Notebook**

- **Add more agents** (e.g., for ESG data, insider trades, etc.)
- **Customize the report template** by editing the analysis agent's instructions
- **Change email recipients** or styling in `send_email_direct`
- **Improve chart placement** by inserting the image directly into the report HTML (see previous suggestions)

---

## 9. **Summary**

This notebook is a modular, extensible example of agentic financial research. Each agent is responsible for a specific data source or analysis, and the orchestration logic combines their outputs into a professional, actionable report delivered via email. 