# JW Meeting Scraper & Greek Translator

This Python script automatically scrapes the weekly meeting content from [JW.org](https://wol.jw.org), follows the links to the associated book and Bible references, and translates the relevant study notes into **Greek** using the `translate` library.

It’s useful for:
- Preparing for meetings in Greek
- Personal study
- Language learning

---

## 🔍 What It Does

- Scrapes the current JW weekly meeting page
- Follows links to the book reading and Bible verses
- Extracts study note sections
- Splits long paragraphs into manageable chunks
- Translates all text into Greek
- Displays a loading animation while translating

---

## ✅ Features

- Auto-fetches study material from JW.org
- Threaded loading animation
- Paragraph splitting for long texts
- Console-based output (future updates will save to file & run in background)

---

## 📦 Requirements

- Python 3.x
- `translate`
- `bs4` (BeautifulSoup)
- `urllib.request`

Install dependencies:

```bash
pip install translate beautifulsoup4
