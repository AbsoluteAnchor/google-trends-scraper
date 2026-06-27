[Google Trends Scraper](https://apify.com/inexhaustible_glass/google-trends-scraper?fpr=data)

# Google Trends Scraper - Keyword Research & SEO Analysis Tool

**The most complete Google Trends scraper on Apify.** Analyze keyword trends, compare search interest, discover rising queries, track trending topics, and get regional data. Free Google Trends API alternative for SEO, keyword research, and market analysis.

## 🎯 What this Google Trends scraper does

This **Google Trends API alternative** / **keyword research tool** / **SEO analysis scraper** gives you:

- 📈 **Interest over time** — historical search interest graph data
- 🌍 **Interest by region** — country/state/city breakdown
- 🔍 **Related queries** — top and rising related searches
- 💡 **Related topics** — top and rising topic suggestions
- 🔥 **Trending searches** — today's trending searches by country
- 📊 **Bulk keyword comparison** — compare 100+ keywords
- 🗓️ **Custom timeframes** — past hour to all-time (2004-present)
- 🌐 **100+ countries** — regional trend data
- 🏷️ **Category filtering** — narrow by topic (News, Sports, Tech, etc.)

## 💼 Perfect for

- **SEO specialists** — find trending keywords to target, track seasonal patterns
- **Content marketers** — identify hot topics for blog posts, videos, newsletters
- **Keyword research** — validate keyword demand before creating content
- **Market research** — analyze consumer interest trends over time
- **Product managers** — track product/category demand and seasonality
- **Trend analysts** — spot emerging trends before they peak
- **Brand monitoring** — track brand mention trends vs competitors
- **E-commerce** — seasonal product planning, trending product discovery
- **News & journalism** — find trending topics and stories
- **Academic research** — study consumer behavior and search patterns
- **Stock/crypto trading** — sentiment indicators from search interest
- **YouTube creators** — find trending video topics
- **Agency reporting** — client dashboards with trend data

## 🔑 Features

- ✅ **Bulk keyword analysis** — up to 100+ keywords per run (Google compares 5 at a time internally)
- ✅ **Interest over time** — daily, weekly, or monthly data points
- ✅ **Regional breakdown** — interest by country, state, metro area
- ✅ **Related queries** — top (most searched) and rising (fastest growing)
- ✅ **Related topics** — semantic topic suggestions
- ✅ **Trending now** — today's trending searches by country
- ✅ **Custom timeframes** — 1 hour, 4 hours, 1 day, 7 days, 30 days, 90 days, 12 months, 5 years, all-time, or custom date range
- ✅ **Country targeting** — 100+ countries supported (US, IN, GB, DE, FR, JP, BR, AU, CA, and more)
- ✅ **Category filtering** — 30+ categories (News, Sports, Tech, Food, Finance, etc.)
- ✅ **JSON output** — clean structured data
- ✅ **Free plan compatible** — runs on 512 MB memory

## 📋 Input

| Field | Type | Description |
| --- | --- | --- |
| `keywords` | Array of strings | Keywords to analyze (up to 100+) |
| `timeframe` | String | Time range: `today 1-m`, `today 3-m`, `today 12-m`, `today 5-y`, `all`, or custom `2024-01-01 2024-12-31` |
| `geo` | String | Country code: `US`, `IN`, `GB`, `DE`, `FR`, `JP`, etc. Empty = worldwide |
| `category` | Integer | Category ID. 0 = all. 13 = News, 71 = Food, 174 = Sports |
| `includeTrending` | Boolean | Also fetch today's trending searches |
| `trendingCountry` | String | Country for trending: `united_states`, `india`, `united_kingdom`, etc. |

### Example input

```
{
  "keywords": ["AI", "ChatGPT", "Claude", "Gemini"],
  "timeframe": "today 3-m",
  "geo": "US",
  "category": 0,
  "includeTrending": true,
  "trendingCountry": "united_states"
}
```

## 📤 Output (per keyword)

```
{
  "keyword": "ChatGPT",
  "success": true,
  "timeframe": "today 3-m",
  "geo": "US",
  "interest_over_time": {
    "dates": ["2026-01-05", "2026-01-12", "..."],
    "values": [90, 85, 78, "..."]
  },
  "interest_by_region": [
    { "region": "California", "value": 100 },
    { "region": "New York", "value": 92 }
  ],
  "related_queries": {
    "top": [{ "query": "chatgpt login", "value": 100 }],
    "rising": [{ "query": "chatgpt 5", "value": "Breakout" }]
  },
  "related_topics": {
    "top": [...],
    "rising": [...]
  },
  "summary": {
    "avg_interest": 72,
    "peak_interest": 100,
    "trend_direction": "rising"
  }
}
```

## 💡 Use cases

### 1. SEO keyword research

Find keywords with rising search interest before your competitors target them. Spot seasonal patterns to plan content calendar.

### 2. Content topic generation

Get `related_queries.rising` for your niche — these are the exact questions people are newly searching for.

### 3. Product trend analysis

Track product category demand over time. "Air fryer" trending up? "Kombucha" declining? Plan inventory and marketing accordingly.

### 4. Competitive brand tracking

Compare your brand name vs competitors in Google Trends to measure share of search over time.

### 5. Seasonal planning

See exactly when "Halloween costumes" or "Christmas gifts" start trending each year to time your campaigns.

### 6. Geographic targeting

Find which states/countries search for your keywords most to prioritize ad spend and localization.

### 7. Stock and crypto sentiment

Search interest often leads price movement — track "Bitcoin", "Tesla", etc. as a sentiment indicator.

## ❓ FAQ

**Q: Is this a Google Trends API?**
A: Google doesn't offer an official public API. This scraper provides equivalent data by scraping Google Trends directly.

**Q: How is this different from pytrends?**
A: pytrends is a Python library that often breaks due to IP blocks and rate limits. This hosted Apify scraper handles infrastructure for you — no setup.

**Q: Can I compare 10+ keywords at once?**
A: Yes. Google internally compares 5 at a time, but this scraper automatically handles batching so you can input 100+ keywords.

**Q: What timeframes are supported?**
A: Past hour (`now 1-H`), past 4 hours (`now 4-H`), past day (`now 1-d`), 7 days, 30 days (`today 1-m`), 90 days (`today 3-m`), 12 months (`today 12-m`), 5 years (`today 5-y`), all-time (`all`), or custom range.

**Q: Does it include trending searches?**
A: Yes, set `includeTrending: true` and specify `trendingCountry`.

**Q: Can I use this on Apify free plan?**
A: Yes — optimized to run on 512 MB memory, so your $5/month free credits cover many runs.

## 🔖 Keywords

google trends scraper, google trends api, keyword research tool, seo keyword finder, trending keywords, search trends api, google trends data, keyword trend analysis, seo tools, trending topics, rising queries, google trends bulk, keyword comparison tool, search volume api, keyword research api, google trends python alternative, pytrends alternative, trend analysis tool, seo research, keyword discovery, content ideas tool, trending searches, google search trends, search interest tracker, keyword popularity, seasonal trends, market trends analysis, trending topics api, google trends export, google trends csv, related queries finder, rising topics finder, seo analytics tool, content marketing tool, trend forecasting, keyword validation

## 📞 Support

Found a bug or have a feature request? Contact the author on Apify.