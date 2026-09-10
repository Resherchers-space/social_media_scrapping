# social_media_scrapping
A Python project to scrape YouTube comments using multiple methods and compare their performance. The project extracts comments, replies, usernames, saves the data into CSV for further data analysis.

Project Objective

The goal of this project is to:

Extract YouTube comments automatically

Compare different scraping methods

Save structured comment data into CSV

Prepare data for Data Analysis / Sentiment Analysis projects

Methods Used

Method

	

Description




YouTube Data API v3

	

Official Google API for extracting comments




yt-dlp

	

Fast extraction without API quota issues




Playwright

	

Browser automation based scraping




youtube-comment-downloader

	

Scrapes public comments directly

Tech Stack

Python

Pandas

Google API Client

yt-dlp

Playwright

youtube-comment-downloader

Output

The extracted CSV contains fields such as:

Author Name

Comment

Likes

Reply Count

Published Date

How to Run

Install dependencies

pip install pandas google-api-python-client yt-dlp youtube-comment-downloader playwright
playwright install chromium

Add your YouTube API Key (for API method)

API_KEY = "YOUR_API_KEY"
VIDEO_ID = "VIDEO_ID"

Run the notebook and the comments will be exported as:

comments.csv
comments_ytdlp.csv
Use Cases

Sentiment Analysis

Political Opinion Mining

Social Media Analytics

NLP Projects

Data Visualization

Findings
Performance Comparison

Method

	

Comments Extracted

	

Time




Official YouTube API

	

10,843

	

44.6 sec




yt-dlp

	

10,843

	

131.38 sec




youtube-comment-downloader

	

10,843

	

226 sec

Key Findings

The Official YouTube API was the fastest method, completing extraction in 44.6 seconds.

yt-dlp successfully extracted all 10,843 comments without relying on API quotas.

youtube-comment-downloader also extracted the complete dataset but was the slowest.

All successful methods produced the same total number of comments, making them suitable for downstream analysis.

CSV export time was negligible (~0.08 sec) compared to scraping time.


Conclusion

For projects requiring speed and reliability, the YouTube Data API v3 is the best choice. If API quota or authentication is a limitation, yt-dlp provides a strong alternative while still extracting the complete comment dataset.
