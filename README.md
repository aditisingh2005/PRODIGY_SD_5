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
web scraping (file://DESKTOP-JJVVK3I/Users/admin/Desktop/web%20scraping)

code:
 import requests
from bs4 import BeautifulSoup
import pandas as pd
import sqlite3
import time

# Base URL
BASE_URL = "http://books.toscrape.com/catalogue/page-{}.html"

# Store all scraped data
books_data = []

def get_star_rating(tag):
    classes = tag.get("class", [])
    for cls in classes:
        if cls in ["One", "Two", "Three", "Four", "Five"]:
            return cls
    return "Unknown"

# Loop through pages
for page in range(1, 51):  # There are 50 pages
    print(f"Scraping page {page}...")
    url = BASE_URL.format(page)
    response = requests.get(url)
    
    if response.status_code != 200:
        print(f"Failed to fetch page {page}")
        break
    
    soup = BeautifulSoup(response.content, "html.parser")
    books = soup.find_all("article", class_="product_pod")
    
    if not books:
        print("No more books found.")
        break

    for book in books:
        title = book.h3.a["title"]
        price = book.find("p", class_="price_color").text.strip()
        rating = get_star_rating(book.p)
        
        books_data.append({
            "Title": title,
            "Price": price,
            "Rating": rating
        })
    
    time.sleep(1)  # Be polite to the server

# Convert to DataFrame
df = pd.DataFrame(books_data)

# Save to CSV
df.to_csv("books.csv", index=False)
print("Data saved to books.csv")

# Save to SQLite
conn = sqlite3.connect("books.db")
df.to_sql("books", conn, if_exists="replace", index=False)
conn.close()
print("Data saved to books.db (SQLite)")


