[Google Trends Scraper](https://apify.com/khadinakbar/google-trends-scraper?fpr=data)

Extract all 5 types of Google Trends data in a single run — no API key, no browser required. Compare up to 5 keywords, drill into regional breakdowns, discover rising queries, and pull daily trending searches from any country. Output is structured JSON ready for AI pipelines, spreadsheets, or business intelligence dashboards.

## What This Actor Does

Google Trends Scraper hits the unofficial Google Trends JSON API directly, using session-based requests to retrieve clean, structured data without Playwright or a headless browser. This makes it fast (typically 20–60 seconds per run), low-cost, and highly reliable. It supports all five of Google Trends' core data surfaces:

- **Interest Over Time** — weekly or daily relative interest scores (0–100) for your keywords, across any timeframe from the past hour to all time since 2004.
- **Interest by Region** — which countries, states, or cities show the most interest in your keyword. Great for geo-targeting and market sizing.
- **Related Queries** — what other searches are rising or consistently popular alongside your keyword. The "rising" ones are early trend signals.
- **Related Topics** — Knowledge Graph entities related to your keyword, with entity IDs (MIDs) for structured data and entity linking.
- **Trending Searches** — today's hottest searches in any country. Includes search volume estimates, related queries, and linked news articles.

You can request any combination of these five data types in a single run.

## Features

- **No API key required** — works entirely through Google's unofficial JSON endpoints
- **Compare up to 5 keywords** — same as the Google Trends UI, side by side in the same dataset
- **All 5 data types in one run** — no need to run multiple actors or make multiple API calls
- **Custom date ranges** — use preset timeframes or specify your own `YYYY-MM-DD YYYY-MM-DD` range
- **All Google properties** — Web Search, Google News, Google Images, YouTube Search, Google Shopping
- **Category filtering** — filter trends by any of Google's 1,000+ topic categories
- **RSS fallback for trending searches** — if the JSON API is blocked, falls back to Google's Trending RSS feed automatically
- **PAY_PER_EVENT pricing** — you only pay for actual results returned, not compute time
- **MCP-ready output** — flat JSON with semantic field names, ready for Claude, GPT-4, and other LLM pipelines via Apify MCP

## Use Cases

**Content Marketing & SEO** — Track keyword interest trends over time to time your content publishing. Find rising related queries before your competitors target them. Identify which regions are most interested in your niche for geo-targeted campaigns.

**Market Research** — Validate product ideas by measuring search interest growth. Compare competitor brand searches to see who's gaining momentum. Use interest by region to prioritize market expansion decisions.

**News & Media Monitoring** — Pull daily trending searches in any country to know what topics are capturing public attention right now. Get linked news articles and search volume estimates for each trend.

**AI & LLM Pipelines** — Feed structured trends data directly into Claude, GPT-4, or other AI agents via the Apify MCP server. The flat output format with semantic field names is optimized for LLM comprehension without hallucination risk.

**Investment Research** — Track search interest for company names, products, or technologies as a leading indicator of consumer demand. Rising queries signal emerging opportunities before traditional data sources pick them up.

## Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `keywords` | array | `[]` | 1–5 search terms to analyze. Leave empty for trending_searches only. |
| `geo` | string | `"US"` | Two-letter country code. Leave blank for worldwide. |
| `timeframe` | string | `"today 12-m"` | Preset range or custom. See options below. |
| `dataTypes` | array | `["interest_over_time","related_queries"]` | Which of the 5 data types to extract. |
| `trendingSearchesGeo` | string | same as geo | Country for trending searches (separate from keyword geo). |
| `maxResults` | number | `500` | Cap on total records returned. Controls cost. |
| `customTimeRange` | string | — | Overrides timeframe. Format: `"2023-01-01 2024-01-01"`. |
| `outputFormat` | string | `"flat"` | `flat` = one record per data point. `summary` = logged summary. |

**Timeframe options:** `now 1-H` (1 hour), `now 4-H` (4 hours), `now 1-d` (1 day), `now 7-d` (7 days), `today 1-m` (30 days), `today 3-m` (90 days), `today 12-m` (12 months), `today 5-y` (5 years), `all` (2004–present).

## Output Fields

Every record has a `type` field indicating which data surface it came from. Fields are populated based on type:

| Field | Type | Present In | Description |
| --- | --- | --- | --- |
| `type` | string | All | interest_over_time, interest_by_region, related_query, related_topic, or trending_search |
| `keyword` | string | All except trending_search | The search keyword this data belongs to |
| `value` | number | interest_over_time, interest_by_region, related_* | Relative interest score 0–100 |
| `date` | string | interest_over_time, trending_search | Human-readable date label |
| `period` | string | interest_over_time | Chart axis period label e.g. "Mar 17–23, 2024" |
| `is_partial` | boolean | interest_over_time | True if the period hasn't ended yet |
| `geo` | string | Most types | Country code or "worldwide" |
| `geo_code` | string | interest_by_region | ISO subdivision code e.g. "US-CA" |
| `geo_name` | string | interest_by_region | Human-readable region name e.g. "California" |
| `related_query` | string | related_query | The related search term |
| `is_rising` | boolean | related_query, related_topic | true = rising trend, false = top/sustained trend |
| `formatted_value` | string | related_query, related_topic | "Breakout" or "+950%" for rising queries |
| `topic_title` | string | related_topic | Knowledge Graph entity display name |
| `topic_type` | string | related_topic | Entity category e.g. "Software", "Person", "Topic" |
| `topic_mid` | string | related_topic | Google Knowledge Graph MID for entity linking |
| `title` | string | trending_search | The trending search query |
| `traffic` | string | trending_search | Estimated search volume e.g. "2M+" |
| `traffic_value` | number | trending_search | Raw numeric traffic estimate |
| `related_queries` | array | trending_search | List of related search strings |
| `articles` | array | trending_search | Up to 3 news articles (title, url, source, snippet) |
| `image_url` | string | trending_search | Representative image URL |
| `scraped_at` | string | All | ISO 8601 timestamp of extraction |
| `source_url` | string | All | Google Trends URL for verification |

## Example Output

**Interest Over Time record:**

```
{
  "type": "interest_over_time",
  "keyword": "ChatGPT",
  "date": "Mar 24, 2024",
  "period": "Mar 17 – 23, 2024",
  "value": 87,
  "is_partial": false,
  "geo": "US",
  "timeframe": "today 12-m",
  "scraped_at": "2024-03-31T14:22:00.000Z",
  "source_url": "https://trends.google.com/trends/explore?q=ChatGPT&geo=US&date=today%2012-m"
}
```

**Related Query record:**

```
{
  "type": "related_query",
  "keyword": "ChatGPT",
  "related_query": "chatgpt login",
  "value": 100,
  "formatted_value": "100",
  "is_rising": false,
  "geo": "US",
  "timeframe": "today 12-m",
  "scraped_at": "2024-03-31T14:22:00.000Z"
}
```

**Trending Search record:**

```
{
  "type": "trending_search",
  "title": "Super Bowl",
  "traffic": "2M+",
  "traffic_value": 2000000,
  "geo": "US",
  "date": "Feb 11, 2024",
  "related_queries": ["Super Bowl 2024", "Super Bowl halftime show"],
  "articles": [
    {
      "title": "Super Bowl LVIII: Everything you need to know",
      "url": "https://espn.com/nfl/story/_/id/...",
      "source": "ESPN",
      "snippet": "Everything fans need to know heading into the big game..."
    }
  ],
  "image_url": "https://t2.gstatic.com/images?q=tbn:...",
  "scraped_at": "2024-02-11T20:00:00.000Z"
}
```

## Cost & Performance

Pricing is **PAY_PER_EVENT** at **$0.005 per result record**. You only pay for actual data returned — not compute time, not failed runs.

| Run Type | Approx. Records | Approx. Cost |
| --- | --- | --- |
| Interest over time, 1 keyword, 12 months | ~52 | $0.26 |
| Interest by region, 1 keyword, worldwide | ~200 | $1.00 |
| Related queries + topics, 1 keyword | ~50 | $0.25 |
| Trending searches, 1 country | ~20–25 | $0.10–$0.13 |
| Full 5-keyword run, all 5 data types | ~500–700 | $2.50–$3.50 |

Typical run time is **20–60 seconds** depending on which data types you select.

## Limitations

- Google Trends enforces a **5-keyword maximum** per comparison — this is a Google platform limit, not an actor limit.
- Interest scores are **relative, not absolute** — 100 means peak popularity within the selected timeframe, not a specific search volume. Values for different keywords are only comparable within the same run.
- The `trending_searches` JSON endpoint may occasionally be blocked by Google's anti-bot detection. The actor automatically falls back to Google's public Trending RSS feed in this case.
- Very short timeframes (past hour, 4 hours) return fewer data points than longer ranges.
- Historical data before 2004 is unavailable through Google Trends.

## No Login Required

This actor works entirely through Google's unofficial JSON API and public RSS feeds. No Google account, cookies, OAuth tokens, or browser automation required. Data is extracted via direct HTTP requests with session management.

## Support & Troubleshooting

**Empty results for trending searches** — Try a well-supported country code: `US`, `GB`, `IN`, `AU`, `CA`, `DE`, `FR`, `BR`, `JP`. Not all countries have sufficient data.

**"No keywords provided" error** — Keywords are only required for `interest_over_time`, `interest_by_region`, `related_queries`, and `related_topics`. For `trending_searches` only, leave the keywords array empty.

**Rate limited or blocked** — Enable Apify residential proxies in the actor's proxy configuration. Free shared datacenter IPs are more likely to be blocked by Google.

**Value is 0 for all data points** — This may mean the keyword had very low interest in the selected region/timeframe. Try broadening the geo to worldwide or extending the timeframe.

If you encounter bugs or want to request features, use the **Issues** tab on this actor's Apify Store page.

## Changelog

**v1.0.0** — Initial release. All 5 Google Trends data types supported. PAY_PER_EVENT pricing ($0.005/record). Automatic RSS fallback for trending searches. Compare up to 5 keywords. Custom date ranges supported.