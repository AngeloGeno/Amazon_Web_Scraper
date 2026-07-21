 Amazon_Web_Scraper
A Python web scraper that collects instant coffee product data from Amazon using Playwright for browser automation and BeautifulSoup for HTML parsing.
---

## Features

- Crawls Amazon search results across multiple pages
- Extracts name, brand, price, weight, rating, review count, and stock status per product
- ASIN-based deduplication (no duplicate products)
- Anti-detection: stealth JS patches, randomised user agents, randomised delays
- CAPTCHA detection with automatic retry and back-off
- Outputs clean CSV ready for analysis

---

## Requirements

- Python 3.10+
- Google Chrome installed
- Miniconda or virtualenv (recommended)

---

## Installation

```bash
# 1. Create and activate environment
conda create -n scraping_env python=3.11
conda activate scraping_env

# 2. Install Python dependencies
pip install playwright beautifulsoup4 nest_asyncio

# 3. Install Playwright's Chrome driver
playwright install chrome
```

---

## Usage

```bash
python amazon_scraper.py
```

A Chrome window will open automatically. The scraper will:

1. Search Amazon for "instant coffee"
2. Collect product URLs across up to 3 pages
3. Visit each product page and extract data
4. Save results to `amazon_instant_coffee.csv`

---

## Configuration

Edit the constants at the top of `amazon_scraper.py`:

| Variable | Default | Description |
|---|---|---|
| `SEARCH_URL` | Amazon instant coffee search | Starting URL |
| `MAX_PAGES` | `3` | Number of search result pages to crawl |
| `OUTPUT_FILE` | `amazon_instant_coffee.csv` | Output filename |
| `CONCURRENCY` | `2` | Parallel product page requests |
| `RETRY_LIMIT` | `3` | Retries per page on failure |
| `HEADLESS` | `False` | Run browser visibly (recommended) |

---

## Output

The CSV contains one row per product with these columns:

| Column | Description |
|---|---|
| `asin` | Amazon Standard Identification Number |
| `name` | Full product title |
| `brand` | Brand name |
| `price_usd` | Price in USD (numeric only) |
| `weight` | Weight or size from product details |
| `rating` | Star rating (e.g. `4.5`) |
| `review_count` | Number of customer reviews |
| `stock` | `In Stock`, `Out of Stock`, or `Unknown` |
| `url` | Direct product URL |
| `scraped_at` | Timestamp of scrape |

---

## Notes

- Keep `HEADLESS = False` — visible Chrome is significantly harder for Amazon to detect than headless
- Keep `CONCURRENCY` at 2 or lower — higher values trigger Amazon's rate limiting
- If you see CAPTCHA prompts in the browser window, solve them manually and the scraper will continue
- Do not use this scraper in ways that violate Amazon's Terms of Service

---

## Project Structure

```
amazon_scraper.py       # Main scraper script
amazon_instant_coffee.csv  # Output (generated after run)
README.md               # This file
```
## Screenshots 
<img width="805" height="517" alt="image" src="https://github.com/user-attachments/assets/f50668b7-ca37-4452-ac83-7f69dfe8beba" />

<img width="1582" height="836" alt="image" src="https://github.com/user-attachments/assets/f571c03b-0c24-40d0-8757-dbbc6e98d5fa" />

<img width="788" height="838" alt="image" src="https://github.com/user-attachments/assets/6504a925-f58a-4940-b7e3-39fcce0fe6d8" />
<img width="1910" height="1038" alt="image" src="https://github.com/user-attachments/assets/31393657-9d5e-4afd-ba1c-571f33bdb8f8" />


