[Google Trends Scraper](https://apify.com/sovereigntaylor/google-trends-scraper?fpr=data)

# Google Trends Scraper

Extract comprehensive data from Google Trends — interest over time, related queries, related topics, trending searches, and geographic breakdowns. Compare up to 5 keywords simultaneously with full historical data.

## What does Google Trends Scraper do?

This actor scrapes Google Trends to extract keyword trend data that marketers, SEO professionals, content creators, and researchers use for data-driven decision making. It uses multiple scraping strategies (API endpoints + HTML parsing) for maximum reliability.

### Key Features

- **Interest Over Time** — Get the full timeline of search interest (0–100 scale) for any keyword, with granularity from minute-level to monthly depending on time range
- **Multi-Keyword Comparison** — Compare up to 5 keywords side by side to see which terms dominate and how they trend relative to each other
- **Related Queries** — Discover "Top" queries (highest volume) and "Rising" queries (fastest growing) related to your keywords — goldmine for SEO keyword research
- **Related Topics** — Find broader topic associations including entity types (Person, Place, Company, etc.) for content strategy planning
- **Daily Trending Searches** — See what's trending right now in any country with traffic estimates and related news articles
- **Real-Time Trending Stories** — Get breaking trend stories with associated entities and news coverage
- **Interest by Region** — Geographic breakdown showing where keywords are most popular (state/province level)
- **Seasonality Detection** — Automatic analysis of seasonal patterns with peak/low months and strength score
- **Trend Direction Analysis** — Automated rising/declining/stable classification with percentage change calculations

### Use Cases

| Use Case | How This Actor Helps |
| --- | --- |
| **SEO Keyword Research** | Find rising search terms before competitors. Discover related keywords you haven't targeted yet. Prioritize keywords by actual search trend data. |
| **Content Strategy** | Identify trending topics for blog posts, videos, and social media. Time content publication to match seasonal search peaks. |
| **Market Research** | Track brand awareness over time. Compare competitor brand search interest. Identify emerging markets and consumer interests. |
| **Product Development** | Validate product ideas by checking search demand trends. Spot declining vs. growing product categories. |
| **Academic Research** | Study public interest in topics over time. Analyze geographic variation in topic popularity. Export clean datasets for analysis. |
| **Competitive Analysis** | Compare your brand vs. competitors in search interest. Identify geographic markets where competitors are stronger. |
| **Investment Research** | Track consumer interest in companies, products, and sectors. Identify breakout trends before they go mainstream. |
| **News & Media Monitoring** | Real-time trending stories with traffic estimates. Daily trending searches by country. |

## Input Configuration

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `searchTerms` | string[] | *required* | Keywords to look up (e.g., `["AI", "machine learning"]`) |
| `geo` | string | `"US"` | Country code (ISO 3166-1 alpha-2). Empty = worldwide |
| `timeRange` | enum | `"past_year"` | Time period: `past_hour`, `past_day`, `past_week`, `past_month`, `past_year`, `past_5_years` |
| `category` | integer | `0` | Google Trends category ID (0 = all). See [category list](https://trends.google.com/trends/explore) |
| `maxResults` | integer | `100` | Max keywords to process from list |
| `includeRelatedQueries` | boolean | `true` | Extract top + rising related queries |
| `includeRelatedTopics` | boolean | `true` | Extract top + rising related topics |
| `includeTrendingSearches` | boolean | `false` | Scrape daily + real-time trending searches |
| `includeInterestByRegion` | boolean | `false` | Geographic interest breakdown |
| `outputFormat` | enum | `"summary"` | `summary` (one record/keyword) or `flat` (one record/datapoint) |
| `proxyConfiguration` | object | — | Apify proxy config (residential recommended) |
| `maxConcurrency` | integer | `2` | Concurrent requests (keep low: 1–3) |
| `customTimeRange` | string | `""` | Custom date range: `"2024-01-01 2024-12-31"` |

### Example Input

```
{
    "searchTerms": ["artificial intelligence", "machine learning", "deep learning"],
    "geo": "US",
    "timeRange": "past_year",
    "category": 0,
    "includeRelatedQueries": true,
    "includeRelatedTopics": true,
    "includeTrendingSearches": false,
    "outputFormat": "summary",
    "proxyConfiguration": {
        "useApifyProxy": true,
        "apifyProxyGroups": ["RESIDENTIAL"]
    }
}
```

## Output

### Summary Format (default)

Each keyword produces one record with all data nested:

```
{
    "keyword": "artificial intelligence",
    "geo": "US",
    "timeRange": "past_year",
    "category": "All Categories",
    "averageInterest": 72,
    "peakInterest": 100,
    "peakDate": "2025-11-15T00:00:00.000Z",
    "troughInterest": 45,
    "trend": "rising",
    "trendChangePercent": 23.5,
    "volatility": 12.3,
    "dataPoints": 52,
    "seasonality": {
        "hasSeasonality": false,
        "peakMonth": "November",
        "lowMonth": "July",
        "seasonalityStrength": 18
    },
    "interestOverTime": [
        {
            "date": "2025-03-09T00:00:00.000Z",
            "interest": 65,
            "isPartial": false
        }
    ],
    "relatedQueries": {
        "top": [
            { "query": "ai tools", "value": 100 },
            { "query": "chatgpt", "value": 95 }
        ],
        "rising": [
            { "query": "claude ai", "value": 5000, "formattedValue": "Breakout" },
            { "query": "ai agents", "value": 2400, "formattedValue": "+2,400%" }
        ]
    },
    "relatedTopics": {
        "top": [
            { "title": "ChatGPT", "type": "Software", "value": 100 }
        ],
        "rising": [
            { "title": "Claude", "type": "AI assistant", "value": 5000, "formattedValue": "Breakout" }
        ]
    },
    "relatedQueriesCount": 45,
    "relatedTopicsCount": 30,
    "scrapedAt": "2026-03-01T12:00:00.000Z"
}
```

### Flat Format

One record per data point — ideal for CSV export and spreadsheet analysis:

```
{
    "keyword": "artificial intelligence",
    "dataType": "interest_over_time",
    "geo": "US",
    "date": "2025-03-09T00:00:00.000Z",
    "interest": 65,
    "averageInterest": 72,
    "trend": "rising"
}
```

### Trending Searches Output

```
{
    "dataType": "daily_trending",
    "title": "Super Bowl",
    "formattedTraffic": "5M+",
    "date": "2026-02-08",
    "geo": "US",
    "articlesCount": 12,
    "articles": [
        {
            "title": "Super Bowl 2026: Everything You Need to Know",
            "url": "https://...",
            "source": "ESPN"
        }
    ]
}
```

## Pricing

This actor uses **Pay Per Event** pricing:

| Event | Price | Description |
| --- | --- | --- |
| `trend-scraped` | $0.005 | Charged per keyword trend successfully extracted |

Example costs:

- 10 keywords, summary format: ~$0.05
- 100 keywords, summary format: ~$0.50
- 10 keywords with trending searches: ~$0.06

## Tips for Best Results

1. **Use residential proxies** — Google Trends aggressively blocks datacenter IPs. Residential proxies dramatically improve success rates.
2. **Keep concurrency low** — Set `maxConcurrency` to 1 or 2. Google rate-limits aggressive scraping.
3. **Batch your keywords** — The actor automatically batches keywords into groups of 5 (Google's comparison limit). Larger keyword lists take proportionally longer.
4. **Choose the right time range** — Shorter ranges (past_hour, past_day) give finer granularity but less historical context. `past_year` (weekly data) is the best balance for most SEO use cases.
5. **Use custom date ranges** — For precise historical analysis, use the `customTimeRange` field with format `"2024-01-01 2024-12-31"`.
6. **Category filtering** — Narrow results with category IDs to avoid ambiguous keywords. "Python" in "Programming" (184) vs "All" gives very different results.
7. **Flat format for analysis** — Use `outputFormat: "flat"` when exporting to spreadsheets, databases, or data visualization tools.

## Limitations

- Google Trends interest values are relative (0–100 scale), not absolute search volumes
- Maximum 5 keywords per comparison (the actor handles batching automatically)
- Real-time trending data is not available for all countries
- Very new or low-volume keywords may return no data
- Google may change their API format — the actor uses multiple fallback strategies to stay resilient

## Changelog

### v1.0 (2026-03-01)

- Initial release
- Multi-strategy scraping (API + HTML fallback)
- Interest over time, related queries, related topics
- Daily and real-time trending searches
- Interest by region (geographic breakdown)
- Seasonality detection and trend analysis
- Summary and flat output formats
- PPE billing at $0.005/keyword

## Integration — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("sovereigntaylor/google-trends-scraper").call(run_input={
    "searchTerm": "google trends",
    "maxResults": 50
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item.get('title', item.get('name', 'N/A'))}")
```

## Integration — JavaScript

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('sovereigntaylor/google-trends-scraper').call({
    searchTerm: 'google trends',
    maxResults: 50
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => console.log(item.title || item.name || 'N/A'));
```