# Stock Market Data Analysis: Which Tech Stock Was the Best Investment?

A beginner-friendly data analysis project in Python that compares four big technology stocks (Apple, Amazon, Google and Microsoft) on **risk, profit, crash days, trends and seasonality**, and turns the results into an interactive HTML dashboard.

![Python](https://img.shields.io/badge/Python-3.x-blue) ![pandas](https://img.shields.io/badge/pandas-data%20analysis-150458) ![Plotly](https://img.shields.io/badge/Plotly-charts-3F4F75) ![Jupyter](https://img.shields.io/badge/Jupyter-notebook-F37626)

---

## Project Overview

Imagine you could travel back a few years and invest in one of four tech companies. Which one would have been the safest? Which one would have made the most money? And what would a 1 million dollar investment look like today?

This project answers those questions using real daily stock prices (2013 to early 2018). I built it as a fresher data analyst to practise the full workflow: loading data, cleaning it, creating new metrics, making charts and explaining the results in plain words.

## Questions This Project Answers

1. Which stock was the **safest** (most stable)?
2. Which stock made the **most money**?
3. What would **1 million dollars** invested in the best stock have grown to?
4. What were the **worst crash days**, and how deep were the falls?
5. What is the **long-term trend** of each stock (moving averages)?
6. Do some **months** perform better than others?
7. Do these stocks **move together**? (This matters for diversification.)

## Dashboard

Running the notebook creates `visuals/dashboard.html`, one interactive page with the key numbers, key findings, all 9 charts and a scorecard table. You can hover over the charts, zoom in and click the legend to hide a stock.

> GitHub shows HTML files as plain code. To use the dashboard, **download `visuals/dashboard.html` and open it in your browser**, or run the notebook yourself and it will be created for you.

## Charts

**Growth of 1 dollar invested in each stock**
![Growth of 1 dollar](visuals/02_growth_of_one_dollar.png)

**Risk: daily volatility of each stock**
![Risk](visuals/01_risk_volatility.png)

**Risk vs return**
![Risk vs return](visuals/04_risk_vs_return.png)

**The 5 worst crash days of each stock**
![Crash days](visuals/06_crash_days.png)

**Closing price with 20-day and 50-day moving averages**
![Moving averages](visuals/07_moving_averages.png)

**Do the stocks move together? (correlation)**
![Correlation heatmap](visuals/09_correlation_heatmap.png)

More charts (final value, the 1 million dollar simulation and monthly seasonality) are in the [`visuals`](visuals) folder and in the dashboard.

## Key Findings

<!-- After running the notebook, copy the "Key findings" list printed in Part 11.2 and paste it here. -->

**Scorecard**

<!-- After running the notebook, copy the scorecard table from Part 11.1 and paste it here as a Markdown table. -->

## An Important Data Note

The dataset has one CSV file per company. While checking the data, I noticed that the four companies do **not** have the same history: the combined data had 4,752 rows instead of the 5,036 expected from four companies with 1,259 trading days each. One company (Google's GOOG) starts later than the others.

Comparing stocks over different time periods is unfair, because a stock with a shorter history had fewer chances to grow and fewer chances to crash. So by default the notebook keeps only the dates where **all four companies have data**. You can switch this off with `USE_COMMON_WINDOW = False` in the settings cell to use each company's full history instead.

## Methods Used

| Step | What I did | Main tools |
|---|---|---|
| Load and combine | Read four CSV files and stacked them into one table | `pd.read_csv`, `pd.concat` |
| Clean and check | Fixed the date type, checked missing values, duplicates, invalid volume and invalid prices, sorted by company and date | `pd.to_datetime`, `isnull`, `duplicated` |
| Daily returns and risk | Percentage change of the closing price; risk measured as the standard deviation of daily returns | `groupby`, `pct_change`, `std` |
| Profit | Compounded daily returns into a cumulative return (value of 1 dollar invested) | `cumprod` |
| Crash days and drawdown | Found the 5 worst days per stock and the biggest fall from a previous high | `nsmallest`, `cummax` |
| Trend | 20-day and 50-day moving averages | `rolling().mean()` |
| Seasonality | Average daily return per calendar month | `dt.month_name()`, `groupby` |
| Diversification | Correlation of daily returns between stocks | `pivot`, `corr` |
| Charts and dashboard | Interactive charts saved as PNG images and combined into one HTML page | Plotly |

## Project Structure

```
stock-market-data-analysis/
├── data/                  # not included in the repo, see "Dataset" below
│   └── individual_stocks_5yr/
├── notebooks/
│   └── stock_market_data_analysis.ipynb
├── visuals/               # created automatically when you run the notebook
│   ├── 01_risk_volatility.png
│   ├── 02_growth_of_one_dollar.png
│   ├── ... (9 charts in total)
│   └── dashboard.html
├── .gitignore
├── LICENSE
└── README.md
```

## Dataset

- **Name:** S&P 500 Stock Data (by Cam Nugent)
- **Source:** [Kaggle](https://www.kaggle.com/datasets/camnugent/sandp500)
- **Content:** daily `open`, `high`, `low`, `close` and `volume` for S&P 500 companies, one CSV file per company
- **Used here:** AAPL (Apple), AMZN (Amazon), GOOG (Google), MSFT (Microsoft)

## How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/ualiurrahat/stock-market-data-analysis.git
   cd stock-market-data-analysis
   ```

2. **Download the dataset** from the Kaggle link above. Unzip it and place the `individual_stocks_5yr` folder inside a new `data` folder in the project root.

3. **Install the libraries**
   ```bash
   pip install pandas numpy plotly kaleido jupyter
   ```

4. **Open the notebook** `notebooks/stock_market_data_analysis.ipynb` in Jupyter or VS Code and use **Run All**.

5. **Open the results.** A `visuals` folder is created with the chart images and `dashboard.html`.

> **Note:** saving the PNG images needs Google Chrome installed (Plotly's image tool, Kaleido, uses it). If Chrome is missing, the notebook prints a message, and the charts and the dashboard still work. You can install Chrome, or run `plotly_get_chrome` in a terminal, and run the notebook again.

## Limitations

- The data covers only a few years and ends in early 2018, so it does not describe today's market.
- Only four large US technology companies were analysed. They are not a fair picture of the whole stock market.
- Volatility is just one way to measure risk, and the dataset does not include dividends, fees or taxes.
- The data shows **when** a crash happened, but not **why**.
- Monthly patterns are based on only a few years, so they are interesting to explore but not a reliable investing rule.
- Past performance does not predict future performance. This is a learning project and **not financial advice**.

## What I Learned

- Combining many files and checking data quality before trusting the numbers
- Working with dates and time series in pandas
- Calculating results per group with `groupby`, `pct_change`, `cumprod`, `cummax` and `rolling`
- Reshaping data with `melt` and `pivot`
- Building clear, interactive charts with Plotly and saving them automatically
- Turning a notebook into a simple dashboard that anyone can open in a browser

## Ideas for Next Steps

- Repeat the analysis with newer data and companies from different industries
- Compare the stocks with the S&P 500 index as a benchmark
- Rebuild the dashboard in a tool such as Power BI or Tableau

## License

This project is licensed under the terms of the [LICENSE](LICENSE) file.

## Author

**Md. Ualiur Rahman Rahat**
GitHub: [@ualiurrahat](https://github.com/ualiurrahat)
