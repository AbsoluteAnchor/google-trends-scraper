[Google Trends Scraper](https://apify.com/scraperpro/google-trends-scraper?fpr=data)

# 📈 Google Trends Scraper

An Apify Actor that retrieves data from Google Trends: realtime trending searches, interest over time, interest by region, and related queries/topics.

### 🚀 Quickstart (no input required)

Want to get started in a flash? ⚡️ The actor has smart defaults, so you can run it immediately and get the latest realtime trending searches for the US.

- **In the Apify UI:** Just click **Run**.

---

### 🔍 What you can fetch

- **Trending now (realtime):** ⏰ Find out what's rapidly rising in searches in the last few hours.
- **Interest over time:** 📊 Get a timeline of search interest for one or more keywords.
- **Interest by region:** 🗺️ Discover where your keywords are searched the most.
- **Related queries/topics:** 💡 Explore new queries and topics related to your main keyword.

---

### 💰 Pricing (rental)

- $12/month
- Recommended for ongoing tracking and monitoring workflows.
- You can configure inputs freely; heavy configurations (very long timeframes, CITY/DMA resolution, inc_low_vol) may take longer.

### ⚙️ Input (overview)

The actor's UI is dynamically generated from the `.actor/INPUT_SCHEMA.json` file. Here are the key fields you'll interact with:

- **`scrape_type`** (select, default: `trending_now`)
- **`keywords`** (array, optional for `trending_now`; required for other types)
- **`gprop`** (select: `web`/`images`/`news`/`shopping`/`youtube`)
- **`timeframe_type`** (select: `predefined` or `custom`, default: `predefined`)
- **`predefined_timeframe`** (select, default: `today 12-m`)
- **`custom_timeframe`** (string, e.g. "2023-01-01 2023-06-30")
- **`geo_selection_type`** (select, default: `Common Countries`)
- **`common_geo`** (string country code, default: `US`)
- **`custom_geo_code`** (string for regions like `US-CA`)
- **`geo_resolution`** (`COUNTRY`/`REGION`/`DMA`/`CITY`; for `interest_by_region`)
- **`inc_low_vol`** (boolean; include low-volume regions; **Pro** recommended)
- **`trending_language`** (string, default: `en`)
- **`trending_hours`** (integer 1-191, default: `24`)

---

### 📋 Example Inputs

Here are some common use cases to get you started!

1. **Realtime trending (US, 24 hours)**

```
{
  "scrape_type": "trending_now",
  "common_geo": "US",
  "trending_hours": 24,
  "trending_language": "en"
}
```
2. **Interest over time for multiple keywords (US)**

```
{
  "scrape_type": "interest_over_time",
  "keywords": ["data science", "machine learning"],
  "timeframe_type": "predefined",
  "predefined_timeframe": "today 12-m",
  "geo_selection_type": "Common Countries",
  "common_geo": "US"
}
```
3. **Related queries for a single keyword (global)**

```
{
  "scrape_type": "related_queries",
  "keywords": ["python"],
  "timeframe_type": "predefined",
  "predefined_timeframe": "today 12-m"
}
```

---

### 💾 Output & Output tab UI

The actor writes exactly one item to the dataset per run, with fields:

- scrape_type
- data (the full results for the chosen type)
- error (boolean)
- error_message (string or null)
- input_summary (geo, timeframe, resolution, gprop, etc.)

Output tab UI

- The default view is All results and shows the full data JSON right away (no need to switch tabs).
- Extra views:

- Trending now (table): A flattened table when scrape_type is trending_now
- Summary: A quick summary of inputs and error status

Notes on data structures

- interest_over_time / interest_by_region: data is an array of objects (rows), similar to a table
- related_queries / related_topics: data is an array containing keyed lists like { "top": [...], "rising": [...] }
- trending_now: data is a list of trending keyword objects (keyword, geo, volume, topic_names, timestamps)

---

### ⚠️ Reliability & Troubleshooting

Encounter common issues? Check this guide:

| Error Type | Symptom | Solution |
| --- | --- | --- |
| **User Confusion** | "My results don't match my keywords!" | Check **Scrape Type**. If it's set to `Trending now`, it ignores keywords. Switch to `Interest over time`. |
| **Proxy Error** | `ProxyError`, `Connection refused` | Google blocked the IP. Enable **Apify Proxy** (Residential recommended) or rotate custom proxies. |
| **Rate Limit** | `429 Too Many Requests` | You are scraping too fast. Slow down, use more proxies, or verify your proxy configuration. |
| **Timeout** | `TimeoutError`, Actor hangs | The request took too long. Try a shorter **Timeframe**, lower **Geo Resolution**, or faster proxies. |
| **No Data** | `AttributeError`, Empty results | Keyword might be too niche for the selected region/timeframe. Try broadening the search (e.g., "Past 5 years"). |
| **Invalid URL** | `ValueError: Invalid Input` | You entered a non-Google Trends URL in keywords. Please enter search terms only. |

---

### 🧰 Runtime defaults & limits

- Memory: 1024 MB (default)
- Timeout: 30 minutes (default)
- CPU: 1 (default)
- Dataset writes: The actor always writes at least one item per run. If no data is found, it pushes an informative item with input summary.

---

## ❓ FAQ & Common Mistakes

### Why is my result showing general trending topics instead of my keywords?

You likely left the **Scrape Type** set to default (`Trending now`).

- **Trending now:** Shows what is popular in the world right now (ignores your keywords).
- **Interest over time:** Shows data specific to **your** keywords.

**Fix:** Change the **Scrape Type** dropdown at the top of the input to `Interest over time` or `Related queries`.

### Why am I getting "No data returned"?

1. **Check your Timeframe:** Very short timeframes (e.g., "Past hour") often have no data for niche keywords. Try `Past 12 months`.
2. **Check your Spelling:** Google Trends is sensitive to spelling.
3. **Geo Mismatch:** Searching for a local keyword (e.g., a specific German store) while Geo is set to "US" will return zero results.

### 📄 Notes

- **Smart Logic:** The actor now detects if you provide keywords but select the wrong scrape type and will warn you in the logs.
- **Alias support:** You can use `"trending_searches"` as a supported alias for `"trending_now"`.

---

## Changelog

### Version 0.2 (Major Update)

- **Enhanced UI/UX**: Grouped input fields for better clarity and added "Smart Logic" to warn about mismatched configurations (e.g., providing keywords for "Trending Now").
- **Smart Logic & Error Handling**:

- Automatically validates URLs in keywords.
- Fixes `400 Bad Request` issues by auto-switching to `REGION` resolution when a specific country is selected.
- Implemented specific error messages for Proxy Errors, Timeouts, and Rate Limits.
- The actor now exits with a proper error code on fatal failures to prevent hanging.
- **Documentation**: Added comprehensive troubleshooting guide and updated FAQ.