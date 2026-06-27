[Google Trends Scraper](https://apify.com/scrape.badger/google-trends-scraper?fpr=data)

## What does Google Trends Scraper do?

Pull [Google Trends](https://trends.google.com) data via the official internal API — interest over time, by region, related topics / queries, trending now, explore, and autocomplete. Seven modes, one actor.

## Why use Google Trends Scraper?

- **7 modes.** Interest Over Time / By Region / Related / Trending Now / Trending (legacy) / Explore / Autocomplete.
- **No consent-wall failures.** ScrapeBadger handles Google's recent consent redirect automatically.
- **GEO handled correctly.** Google's API rejects lowercase geo codes — we uppercase for you.
- **Time range, category, property filters.** Full Trends filter set exposed.
- **Dirt cheap.** $0.25 / 1k calls — ~17% under the official Apify actor.

## What data can Google Trends Scraper extract?

| Field | Type | Description |
| --- | --- | --- |
| mode | string | Which Trends endpoint produced this record |
| query | string | Source query |
| geo | string | ISO country code (uppercased) |
| date / timestamp | string / number | Time-series index point |
| value / extracted_value | number | Interest score 0-100 |
| keyword / topic | string | Related-mode payload |

## How to scrape Google Trends

1. Click **Try for free**.
2. Pick `mode`: Interest Over Time, Interest By Region, Related, Trending Now, Trending (legacy), Explore, or Autocomplete.
3. Fill in the required input for that mode (usually `q`).
4. Optional: `geo` (country), `hl` (language), `date` (time range), `cat` (category), `gprop` (property).
5. Click **Start** — data points stream into the dataset.

## How much will it cost?

**$0.00025 per call (≈ $0.25 per 1,000 calls).** One call per mode invocation. Trending Now with `max_pages: 5` = 5 calls = $0.00125.

### Competitor benchmark

| Actor | Author | Price | Notes |
| --- | --- | --- | --- |
| apify/google-trends-scraper | Apify | ~$0.30 / 1k results | Official |
| nexgendata/google-trends-scraper | nexgendata | ~$5 / 1k data points | Per-result pricing |
| consummate_mandala/google-trends-scraper | consummate_mandala | ~$0.75 / 1k results | Community |
| **scrape-badger/google-trends-scraper** | **ScrapeBadger** | **$0.25 / 1k calls** | **17% under official** |

## Input

Configure the run in the **Input** tab above, or pass a JSON object matching the fields below when calling the Actor via the Apify API.

| Field | Required | Description |
| --- | --- | --- |
| mode | ✅ | One of 7 modes (see above). |
| q | mode-dependent | Search term. |
| geo | — | ISO country code (auto-uppercased). |
| hl | — | Language code. |
| date | — | Google time range: `today 12-m`, `today 5-y`, `2023-01-01 2023-12-31`, etc. |
| cat | — | Google category ID. |
| gprop | — | Property: web / images / news / youtube / froogle. |
| max_pages | Trending Now only | Pagination budget. |

## Output

Every successful run streams records into the run's dataset. Download as JSON, CSV, XML, Excel, or HTML from the **Dataset** tab; consume programmatically via the Apify API or webhooks.

Example record:

```
{
  "mode": "Interest Over Time",
  "query": "machine learning",
  "geo": "US",
  "date": "Apr 20 \u2013 26, 2025",
  "timestamp": 1745107200,
  "value": 86,
  "extracted_value": 86
}
```

## Tips / Advanced options

- **Interest values are relative, not absolute.** Google normalises to 0-100 within the time range. Don't compare values across different queries in separate runs.
- **Use Explore for widget tokens.** Explore returns tokens that other modes need for advanced queries.
- **Category filters dramatically change results.** E.g. `'python'` in Category 31 (Programming) vs. unfiltered.
- **Schedule daily for trending-topic tracking.** Trending Now updates every hour on Google's side.

## FAQ, Disclaimers, Support

### Does this use the official Google Trends API?

Google Trends has no public official API — we use the same internal API their web UI calls, handled via ScrapeBadger's residential proxy pool to avoid rate limits.

### Why `geo` uppercasing?

Google's internal API returns 400 Bad Request for lowercase `us`; only `US` works. The actor handles that for you.

### What time ranges are supported?

All of Google Trends' presets: `today 1-H`, `today 4-H`, `today 1-d`, `today 7-d`, `today 1-m`, `today 3-m`, `today 12-m`, `today 5-y`, `all`. Custom ranges: `YYYY-MM-DD YYYY-MM-DD`.

### Can I compare multiple queries?

Yes — Interest Over Time accepts comma-separated queries (up to 5, matching Google's UI limit).

### Disclaimer

This Actor scrapes public Google data only. You're responsible for compliance with Google's Terms of Service and any applicable data-protection laws (GDPR, CCPA, etc.) in your jurisdiction. ScrapeBadger does not store the scraped results — they are delivered directly to your Apify dataset.

### Support

Something not working? Open a ticket in the **Issues** tab above — we triage within one business day. Full API reference: [docs.scrapebadger.com](https://docs.scrapebadger.com).

### Powered by

[ScrapeBadger](https://scrapebadger.com) — Google-optimised residential proxy pool + browser-farm fallback, 99.7% uptime, unmetered bandwidth. No CAPTCHAs reach you.