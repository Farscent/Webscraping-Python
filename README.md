# Historical Stock Price Web Scraping

A small Python project that turns historical Netflix and Amazon stock-price tables into clean datasets. I built this to practice web scraping, working with HTML, and checking data before using it for analysis.

## What it does

- Downloads two saved HTML pages with Requests, using timeouts and HTTP error checks.
- Finds the historical-price table by its headers and extracts rows with BeautifulSoup.
- Converts dates, prices, and volume into useful data types and checks data quality.
- Compares the result with `pandas.read_html` using the same source table.
- Summarizes the available date range and closing prices, then exports one CSV per company.

## Run locally

Use Python 3.10 or later. From this repository's directory:

```bash
python -m venv .venv
```

Activate the environment with `.venv\Scripts\activate` on Windows or `source .venv/bin/activate` on macOS/Linux, then run:

```bash
python -m pip install -r requirements.txt
jupyter lab stock_price_scraping.ipynb
```

Choose **Run > Run All Cells**. Internet access is required to download the source pages. Successful execution displays previews, parser-agreement messages, and a summary table. It writes `data/netflix_historical_prices.csv` and `data/amazon_historical_prices.csv`; generated files are excluded from Git.

## Files

| File | Purpose |
| --- | --- |
| `stock_price_scraping.ipynb` | Full scraping, cleaning, comparison, and export workflow |
| `requirements.txt` | Runtime and notebook dependencies |
| `.gitignore` | Excludes environments, notebook checkpoints, and generated data |

## Data and limitations

The inputs are static Yahoo Finance HTML snapshots hosted by IBM Skills Network, not live quotes:

- [Netflix snapshot](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/netflix_data_webpage.html)
- [Amazon snapshot](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/amazon_data_webpage.html)

The tables contain monthly historical observations. The scraper expects the current seven-column layout and English dates. Non-price event rows are counted and skipped; unexpected values fail validation. Agreement between parsers checks extraction consistency, not source accuracy. This project is for learning data collection and does not provide investment advice.

## Validation

The extraction and cleaning logic was checked offline against the Netflix HTML retained in the original notebook and against a small synthetic table with an event row. A fresh two-page download could not be tested in the preparation environment because outbound network connections were restricted. The notebook therefore ships with cleared outputs; running all cells locally performs the full source-data checks.

## Acknowledgments

The initial material and supplied snapshots come from IBM Skills Network, with original material by Joseph Santarcangelo, Azim Hirjani, and Akansha Yadav (IBM Corporation, 2020). This repository presents a reorganized personal project with shared scraping functions, explicit cleaning, validation, and CSV exports.
