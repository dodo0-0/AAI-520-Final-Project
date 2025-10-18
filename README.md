# AAI-520 Investment Research Agent

## Project Overview
This repository contains the final project for AAI-520, an autonomous AI agent called **InvestmentResearchAgent** that conducts stock analysis. The agent fetches data, processes it using NLP, evaluates quality, and generates investment reports with recommendations. It demonstrates agent functions (planning, tool use, self-reflection, learning) and workflow patterns (prompt chaining, routing, evaluator-optimizer).

**Author**: Gaurav SS  
**Date**: September 28, 2025  
**Course**: AAI-520, University of Sandiego

## Objectives
- **Input**: A stock symbol (e.g., AAPL).
- **Output**: A JSON investment report with:
  - News sentiment analysis (e.g., NEGATIVE, keywords, summary).
  - Market trend analysis (e.g., Upward, based on 30-day moving average).
  - Financial metrics (e.g., Total Revenue).
  - Quality score and recommendation (e.g., "Hold" if score ≥ 80).
- **Features**:
  - **Agent Functions**: Planning (`plan_research`), dynamic tool use (`execute_tools`), self-reflection (`self_reflect`), and learning (`memory.json`).
  - **Workflow Patterns**: Prompt chaining (`process_news_chain`), routing (`route_tasks`), evaluator-optimizer (`evaluate_and_optimize`).
  - **Visualization**: Stock price and 30-day moving average chart.
- **Technologies**: Python, Jupyter Notebook, `yfinance`, `newsapi-python`, `transformers`, `nltk`, `matplotlib`.

## Dataset
- **Yahoo Finance (`yfinance`)**: Historical stock prices (1 year, ~252 variables: Open, Close, Volume, etc., ~1MB) and financial statements (e.g., Total Revenue, ~1MB).
- **NewsAPI**: Financial news articles (up to 10 per query, variables: description, title, ~5-10KB).
- **FRED API**: Placeholder for economic indicators (~50 variables, ~100KB, not implemented).
- Data is dynamically fetched, with no static files.

## Repository Structure
```
aai-520-investment-research-agent/
├── aai-520_project.ipynb  # Main Jupyter Notebook with code and documentation
├── memory.json            # Stores agent insights for learning
├── README.md              # This file
```

## Setup Instructions
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/aai-520-investment-research-agent.git
   cd aai-520-investment-research-agent
   ```

2. **Install Dependencies**:
   Ensure Python 3.8+ is installed, then run:
   ```bash
   pip install yfinance newsapi-python transformers torch nltk matplotlib
   ```

3. **Download NLTK Data**:
   In a Python environment, run:
   ```python
   import nltk
   nltk.download('punkt')
   nltk.download('stopwords')
   ```

4. **Obtain a NewsAPI Key**:
   - Sign up at [NewsAPI](https://newsapi.org/) to get an API key.
   - Replace `'925d94dc323f4bd9956fbc010367ed79'` in the notebook with your key.

5. **Run the Notebook**:
   - Open `aai-520_project.ipynb` in Jupyter Notebook or JupyterLab:
     ```bash
     jupyter notebook
     ```
   - Execute all cells to run the agent for AAPL (or modify for another stock, e.g., MSFT).

## Usage
1. **Run the Agent**:
   - The notebook initializes `InvestmentResearchAgent` with a stock symbol and NewsAPI key.
   - Example:
     ```python
     newsapi_key = 'your-newsapi-key'
     agent = InvestmentResearchAgent('AAPL', newsapi_key)
     results = agent.run_analysis()
     print(json.dumps(results['report'], indent=2, default=str))
     ```
   - Output: JSON report with sentiment, trends, revenue, and recommendation, plus a price chart.

2. **Expected Output** (e.g., for AAPL):
   ```json
   {
     "overall_recommendation": "Hold",
     "optimization_note": "No refinement needed—high quality.",
     "news_analysis": {
       "avg_sentiment": "NEGATIVE",
       "keywords": ["apple", "aapl", "stocks", ...],
       "summary": "Apple remains a key holding per Berkshire..."
     },
     "market_analysis": {
       "trend": "Upward",
       "last_close": 234.07,
       "ma30": 227.56
     },
     "earnings_analysis": {
       "latest_revenue": "1234567890"
     }
   }
   ```

3. **Visualization**:
   - A matplotlib chart displays the stock’s closing price and 30-day moving average.

## Project Development
Developed over four weeks (September 1-28, 2025):
- **Week 1**: Environment setup, planning, and data fetching (`plan_research`, `fetch_stock_data`, `fetch_news`, `execute_tools`).
- **Week 2**: Self-reflection and memory (`self_reflect`, `load_memory`, `save_memory`).
- **Week 3**: Prompt chaining and routing (`process_news_chain`, `route_tasks`).
- **Week 4**: Evaluator-optimizer, refinements (summarizer `max_length=40`, revenue extraction), and visualization (`evaluate_and_optimize`).

## Challenges and Solutions
- **Week 1**: API key issues and inconsistent financials data; resolved with error handling.
- **Week 2**: Memory update bugs; fixed with debug prints and file resets.
- **Week 3**: LLM model download delays and summarizer length warnings; noted for refinement.
- **Week 4**: Financials extraction and visualization setup; resolved by targeting `'Total Revenue'` and adding matplotlib.

## Future Improvements
- Integrate FRED API for economic indicators.
- Enhance financials analysis (e.g., additional metrics like EPS).
- Add interactive visualizations (e.g., Plotly).

## License
This project is for academic purposes under AAI-520 and is not licensed for commercial use.