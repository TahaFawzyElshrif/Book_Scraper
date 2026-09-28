# Books Scraping & SQL Analysis

## Task Definition

The goal of this task is to scrape the first 100 books from [Books to Scrape](https://books.toscrape.com/) and analyze basic book information, including:

* Title
* Price
* Rating
* Stock availability
* Book URL

The scraped data is stored in `books.csv` and then loaded into SQLite for analysis.

---

## Frameworks & Tools

* **Python 3**
* **BeautifulSoup4** — HTML parsing and data extraction
* **Requests** — HTTP requests
* **SQLite** — Data storage and SQL analysis

---

## 1. Web Scraping

I used Python with BeautifulSoup4 to scrape the website and extract the required book information.

The extracted data is temporarily stored in `books.csv` with the following schema:

```text
title, price, rating, in_stock, url
```

For understanding the website's HTML structure and verifying the appropriate selectors, I used AI assistance to help me write the initial scraping implementation and to identify the relevant HTML structure and BeautifulSoup selectors. I reviewed the generated code, tested it against the website, and made sure I understood how each part of the solution works.

The scraper collects pages **1–5**, resulting in the first **100 books**.

---

## 2. SQL Analysis

### Database Choice

SQLite was used because it is sufficient for the scope of this task. Using MySQL or SQL Server would require additional database server or local setup, adding complexity without providing a meaningful benefit for this dataset.

### Loading the Data

The CSV data is loaded into a SQLite database (`books.db`) before running the required queries.

### Query 1 — Average Price for Each Rating

```text
[
    (1, 35.51954545454545),
    (2, 35.909473684210525),
    (3, 36.83909090909091),
    (4, 33.98166666666666),
    (5, 30.012105263157896)
]
```

### Query 2 — Five Most Expensive Books Rated 4 or 5

```text
[
    ('The Death of Humanity: and the Case for Life', 4, 58.11),
    ('The Past Never Ends', 4, 56.5),
    ('Sapiens: A Brief History of Humankind', 5, 54.23),
    ("Scott Pilgrim's Precious Little Life (Scott Pilgrim #1)", 5, 52.29),
    ('Behind Closed Doors', 4, 52.22)
]
```

### Query 3 — Number of Out-of-Stock Books per Rating

```text
[]
```

The result is an empty list, which means that no books matched the condition `in_stock = false`.

I checked the website again and confirmed that all of the first 100 books are listed as **"In stock"**. Therefore, the empty result is expected for this dataset.

---

## 3. Notes & Handling Potential Blocking

### What broke, or took longer than expected?

Nothing broke, and both the scraping and SQL parts were straightforward.

One unexpected result was that the out-of-stock query returned an empty list (`[]`).

I checked the website again and confirmed that all of the first 100 books are listed as **"In stock"**. Therefore, the empty result is expected for this dataset.

### If the site started blocking requests after 50 requests, what would you change?

If the site started blocking requests, I would first check its policies and rate limits.

I would then:

* Add a delay between requests to reduce the request rate.
* Store or cache already downloaded pages so that the same page is not requested again.
* Avoid making unnecessary requests.

---

## Future Work

This website is specifically designed for scraping practice. Real-world websites can be more complex and may require additional considerations.

Possible improvements include:

* Check the website's `robots.txt` and scraping policies before collecting data.
* Handle websites with more complex or dynamic structures.
* Use more flexible extraction logic when the HTML structure is inconsistent.
* Prefer an official API when one is available and appropriate.
* Handle cases where information needs to be collected from multiple websites.
* Implement proper rate-limit handling, delays, caching, and retries.
* For a production-scale application, consider using a production database such as **SQL Server** or **MySQL**, depending on the application's requirements.

---

## Project Structure

```text
.
├── code.ipynp
├── books.csv
├── books.db
└── README.md
```

## Result

The scraper successfully collected **100 books** from pages 1–5, stored the results in CSV format, loaded them into SQLite, and executed the requested SQL queries.
