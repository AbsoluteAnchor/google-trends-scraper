[Google Trends Scraper](https://apify.com/joyouscam35875/google-trends-scraper?fpr=data)

# 📈 Google Trends Scraper

Scrape **Google Trends** data at scale — interest over time, related queries, rising topics, and regional interest. Built for SEO professionals, content strategists, and market researchers.

## 💰 3x Cheaper Than Competitors

| Actor | Price per keyword |
| --- | --- |
| Other Google Trends scrapers | $0.005–$0.010 |
| **This actor** | **$0.002** |

Pay-per-event pricing — you only pay for what you scrape.

## 🎯 What You Get

For each keyword, the actor returns:

- **Interest Over Time** — Daily/weekly/monthly search interest (0–100 scale)
- **Related Queries** — Top and rising related search terms
- **Related Topics** — Top and rising related topics with categories
- **Interest by Region** — Geographic breakdown by country or sub-region

## 🚀 Use Cases

### SEO & Content Strategy

- Find trending keywords before your competitors
- Identify seasonal search patterns for content planning
- Discover related queries to expand your keyword clusters

### Market Research

- Compare brand awareness across regions
- Track industry trend shifts over time
- Identify emerging markets for product launches

### Competitive Intelligence

- Monitor competitor brand search trends
- Compare multiple products or technologies
- Track market share shifts via search interest

### Academic & Data Journalism

- Study public interest in events, policies, or phenomena
- Build datasets for research papers
- Visualize trend data for articles and reports

## 📥 Input

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `keywords` | `string[]` | *required* | Keywords to scrape (max 5) |
| `timeRange` | `string` | `"today 12-m"` | Time range for data |
| `geo` | `string` | `""` (worldwide) | Country code (US, FR, GB, etc.) |
| `category` | `integer` | `0` | Google Trends category ID |

### Time Range Options

| Value | Description |
| --- | --- |
| `now 1-H` | Past hour |
| `now 4-H` | Past 4 hours |
| `now 1-d` | Past day |
| `now 7-d` | Past 7 days |
| `today 1-m` | Past month |
| `today 3-m` | Past 3 months |
| `today 12-m` | Past 12 months |
| `today 5-y` | Past 5 years |
| `all` | All time (2004–present) |

### Example Input

```
{
    "keywords": ["artificial intelligence", "machine learning", "deep learning"],
    "timeRange": "today 12-m",
    "geo": "US",
    "category": 0
}
```

## 📤 Output

Each keyword produces one dataset item:

```
{
    "keyword": "artificial intelligence",
    "timeRange": "today 12-m",
    "geo": "US",
    "scrapedAt": "2026-03-28T21:00:00.000Z",
    "interestOverTime": [
        { "date": "Mar 31 – Apr 6, 2025", "value": 71 },
        { "date": "Apr 7 – Apr 13, 2025", "value": 68 },
        { "date": "Apr 14 – Apr 20, 2025", "value": 75 },
        "..."
    ],
    "relatedQueries": {
        "top": [
            { "query": "ai artificial intelligence", "value": "100" },
            { "query": "chatgpt", "value": "85" },
            { "query": "openai", "value": "62" }
        ],
        "rising": [
            { "query": "claude ai", "value": "+4,500%" },
            { "query": "gemini ai", "value": "+2,800%" }
        ]
    },
    "relatedTopics": {
        "top": [
            { "topic": "Artificial intelligence", "value": "100", "type": "Technology" },
            { "topic": "ChatGPT", "value": "78", "type": "Software" }
        ],
        "rising": [
            { "topic": "Claude", "value": "+3,200%", "type": "Software" }
        ]
    },
    "interestByRegion": [
        { "geoName": "District of Columbia", "value": 100 },
        { "geoName": "Washington", "value": 89 },
        { "geoName": "California", "value": 85 },
        { "geoName": "Massachusetts", "value": 82 }
    ]
}
```

## ⚙️ How It Works

1. Fetches widget tokens from Google Trends explore API
2. Uses tokens to request each data type (time series, geo, related searches)
3. Parses and normalizes the response data
4. Random delays (1–3s) between requests to respect rate limits
5. Exponential backoff on rate limiting (HTTP 429)

## 🔧 Technical Details

- **HTTP/2** for faster, more efficient connections
- **Session cookies** for proper authentication
- **Exponential backoff** with jitter on rate limits
- **Graceful error handling** — partial results are still saved

## 💡 Tips

- **Max 5 keywords per run** — this is a Google Trends limitation for comparison data
- **Use country codes** (ISO 3166-1 alpha-2) for regional filtering
- **Longer time ranges** return weekly/monthly aggregates; shorter ranges give hourly/daily data
- **Category filtering** narrows results — find category IDs on Google Trends
- **Schedule runs** to track trends over time and build historical datasets

## 📊 Integrations

Export your data to:

- Google Sheets / Excel for visualization
- BigQuery / Snowflake for analytics pipelines
- Slack / Email via Apify webhooks for alerts on trending topics
- Custom dashboards via the Apify API

## 🏷️ Tags

`google-trends` `seo` `keyword-research` `market-research` `trending` `search-trends` `content-strategy` `competitive-intelligence`

## 🔗 Quick Integration

### Python

```
from apify_client import ApifyClient
client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("joyouscam35875/google-trends-scraper").call(run_input={...})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### Node.js

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });
const run = await client.actor('joyouscam35875/google-trends-scraper').call({...});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
```

### No-code: Make / Zapier / n8n

Search for this actor in the Apify connector. No code needed.

---

## 🔗 More Scrapers by Ken Digital

| Scraper | What it does | Price |
| --- | --- | --- |
| [YouTube Channel Scraper](https://apify.com/joyouscam35875/youtube-channel-scraper) | Videos, stats, metadata via official API | $0.001/video |
| [France Job Scraper](https://apify.com/joyouscam35875/france-job-scraper) | WTTJ + France Travail + Hellowork | $0.005/job |
| [France Real Estate Scraper](https://apify.com/joyouscam35875/france-real-estate-scraper) | 5 sources + DVF price analysis | $0.008/listing |
| [Website Content Crawler](https://apify.com/joyouscam35875/website-content-crawler) | HTML to Markdown for AI/RAG | $0.001/page |
| [Google Trends Scraper](https://apify.com/joyouscam35875/google-trends-scraper) | Keywords, regions, related queries | $0.002/keyword |
| [GitHub Repo Scraper](https://apify.com/joyouscam35875/github-repo-scraper) | Stars, forks, languages, topics | $0.002/repo |
| [RSS News Aggregator](https://apify.com/joyouscam35875/rss-news-aggregator) | Multi-source feed parsing | $0.0005/article |
| [Instagram Profile Scraper](https://apify.com/joyouscam35875/instagram-profile-scraper) | Followers, bio, posts | $0.0015/profile |
| [Google Maps Scraper](https://apify.com/joyouscam35875/google-maps-scraper) | Businesses, reviews, contacts | $0.002/result |
| [TikTok Scraper](https://apify.com/joyouscam35875/tiktok-scraper) | Videos, likes, shares | $0.001/video |
| [Google SERP Scraper](https://apify.com/joyouscam35875/google-serp-scraper) | Search results, PAA, snippets | $0.003/search |
| [Trustpilot Scraper](https://apify.com/joyouscam35875/trustpilot-scraper) | Reviews, ratings, sentiment | $0.001/review |

👉 [View all scrapers](https://apify.com/joyouscam35875)