# YouTube Comments Scraper — Political News Videos

This notebook explores different ways to **extract comments from YouTube videos** (focused on political news videos), and compares how fast/reliable each method is. It's part of a college data-extraction project.

**Test video used:** [`https://www.youtube.com/watch?v=yCX5rj9Tmxs`](https://www.youtube.com/watch?v=yCX5rj9Tmxs) — this is the video most of the methods (yt-dlp, Playwright, youtube-comment-downloader, and the later API runs) were actually tested on. It ended up having **10,000+ comments**, which is why it's a good stress-test for comparing speed.

## What this notebook actually does

It is not one single script — it's a collection of **4 different approaches** to get YouTube comments, tried one after another so they can be compared:

| # | Method | How it works | Needs |
|---|--------|---------------|-------|
| 1 | **YouTube Data API v3** | Uses Google's official API to fetch comments + replies for a video ID | A free YouTube API key |
| 2 | **yt-dlp** | A video-download tool that can also pull comments without using the official API | Just the library, no key |
| 3 | **Playwright (browser automation)** | Opens the YouTube page in a real (headless) browser and scrolls down, reading comments straight from the page | Playwright + Chromium |
| 4 | **youtube-comment-downloader** | A ready-made Python package built specifically for scraping comments | Just the library, no key |

For each method, the notebook:
1. Takes a YouTube video ID or URL
2. Fetches all top-level comments (and replies, where supported)
3. Saves everything into a `.csv` file (author, comment text, likes, date, etc.)

## Speed comparison (from the notebook's own test run)

| Method | Time taken |
|---|---|
| Official API | 44.6 sec |
| yt-dlp | 131.4 sec |
| youtube-comment-downloader | 226 sec |

👉 **The official API was the fastest** of the three that were timed. (Playwright wasn't included in this timing test.)

## Problems faced with each method

- **Official API** — Worked cleanly and was the fastest overall. Only real limitation: it runs on a daily API quota, so scraping many videos (especially ones with 10,000+ comments like the test video) can burn through quota fast.
- **yt-dlp** — Installing it triggered a **dependency conflict warning**: Colab needs `pandas==2.2.3`, but installing yt-dlp pulled in `pandas 3.0.5`, which pip flagged as incompatible. It still worked for scraping, but this kind of version clash can silently break other cells in the same notebook that rely on pandas.
- **youtube-comment-downloader** — No errors, but it was clearly the **slowest** (226 sec vs. 44.6 sec for the API and 131 sec for yt-dlp) despite fetching the most comments (10,843) of the three that completed.

<img width="660" height="565" alt="image" src="https://github.com/user-attachments/assets/c8678413-ca80-45b1-9826-108c88ce7912" />

## How to run it

1. Open the notebook in Google Colab or Jupyter.
2. Pick whichever method's section you want to try (they're separated by markdown headings like "API", "yt-dlp", etc.).
3. Replace `VIDEO_ID` or `VIDEO_URL` with the video you want to scrape.
4. Run the cells in that section top to bottom.
5. Find the output as a `.csv` file in the same folder.

## ⚠️ Important note

The notebook currently has a **YouTube API key hardcoded directly in the code** (in the cells that use the Official API method). Before sharing or uploading this notebook anywhere public (like GitHub), that key should be removed and loaded from an environment variable or a config file instead — otherwise anyone with the notebook can use (and exhaust) your API quota.
