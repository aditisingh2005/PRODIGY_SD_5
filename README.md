# web-scraper-project
# 📚 Web Scraper: Books to Scrape

This project is a complete Python-based web scraper that extracts book data from [Books to Scrape](http://books.toscrape.com), a website designed for web scraping practice.

It automatically scrapes all book titles, prices, and ratings from all 50 pages of the catalog and saves the data in two formats:

- `books.csv` — for spreadsheets or data analysis
- `books.db` — SQLite database for querying with SQL

---

## 🚀 Features

- 🔄 Multi-page scraping (pagination handled automatically)
- 📊 Saves clean data to **CSV**
- 🗃️ Stores data in **SQLite database**
- 🧹 Uses **BeautifulSoup**, **Pandas**, and **SQLite**
- 🧠 Clean and beginner-friendly Python code

---

## 🔧 Requirements

Install dependencies:

```bash
pip install -r requirements.txt
