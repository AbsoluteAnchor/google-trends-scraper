[Google Trends Scraper](https://apify.com/nexgendata/google-trends-scraper?fpr=data)

# Google Trends Scraper by nexgendata

Extract search interest data from Google Trends for any keyword or set of keywords. This actor uses the Google Trends platform to retrieve interest-over-time data, related queries, rising search terms, and regional interest breakdowns. Compare up to five keywords simultaneously, filter by country, and select time ranges from the past hour to the past five years. Built for SEO professionals, market researchers, content strategists, and anyone who needs quantified search demand data.

Google Trends is the only public source for relative search volume data across Google's search engine, which processes over 8.5 billion searches daily. The interest scores Google provides (scaled 0-100) reveal how search demand for any topic changes over time and varies by geography. This data drives decisions about content timing, market entry, product naming, ad spend allocation, and competitive positioning. This actor packages that data into structured JSON so you can analyze trends programmatically instead of manually reading charts on the Google Trends website.

## How It Works

Provide up to five keywords and the actor queries Google Trends for comparative interest data. The results include three data types. Interest over time gives you a time series showing how search interest for each keyword has changed across your selected time range, with each data point containing the date, keyword, and interest score (0-100 where 100 is peak popularity). Related queries show what other searches people perform alongside your keywords, split into top queries (consistently popular) and rising queries (experiencing rapid growth). Regional interest breaks down search popularity by state, country, or metro area depending on your geographic scope.

Time range options span from the past hour (for real-time trend monitoring) to the past five years (for long-term market analysis). Country filtering lets you focus on a specific market or compare global patterns. When you provide multiple keywords, Google Trends normalizes the data so you can directly compare relative search interest between terms — essential for keyword prioritization and competitive analysis.

## Who Uses This

SEO professionals use Google Trends data to prioritize keywords by actual search demand, identify seasonal patterns in search behavior, and discover emerging search terms before they become competitive. A content team deciding between two article topics can compare their Google Trends data to choose the one with growing search interest rather than declining demand.

Market researchers track Google Trends data to measure brand awareness relative to competitors, identify emerging consumer interests, and validate market size assumptions. When Google searches for "electric bikes" triple in a specific region, that signals a concrete demand shift that retail, manufacturing, and logistics businesses need to know about. Product teams use trend data to time launches, name features, and identify geographic markets where demand is strongest.

Media buyers and advertising teams align campaign timing with search interest patterns. Running ads for "tax software" in January when search interest begins climbing gets better results than flat spending across the year. Content publishers schedule articles to coincide with rising search trends rather than publishing into declining interest.

## Pricing

This actor costs $5 per 1,000 data points. A single keyword analysis over 12 months (52 weekly data points plus related queries and regional data) typically generates 100-200 data points, costing about $0.50-1.00. A comprehensive competitive analysis comparing 5 keywords with all data types runs roughly $2-3. Monthly monitoring of 20 keyword sets costs approximately $15-25/month depending on the breadth of related queries returned.

---

 

## 💻 Code Example — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("nexgendata/google-trends-scraper").call(run_input={
    # Fill in the input shape from the actor's input_schema
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

## 🌐 Code Example — cURL

```
curl -X POST "https://api.apify.com/v2/acts/nexgendata~google-trends-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{ /* input schema */ }'
```

## ❓ FAQ

**Q: How do I get started?**
Sign up at [apify.com](https://www.apify.com/?fpr=2ayu9b), grab your API token from Settings → Integrations, and run the actor via the Apify console, API, Python SDK, or any integration (Zapier, Make.com, n8n).

**Q: What's the typical cost per run?**
See the pricing section below. Most runs finish under $0.10 for typical batches.

**Q: Is this actor maintained?**
Yes. NexGenData maintains 165+ Apify actors and ships updates regularly. Bug reports via the Apify console issues tab get responses within 24 hours.

**Q: Can I use the output commercially?**
Yes — you own the output data. Check the target site's Terms of Service for any usage restrictions on the scraped content itself.

**Q: How do I handle rate limits?**
Apify manages concurrency and retries automatically. For very large batches (10K+ items), run multiple smaller jobs in parallel instead of one mega-job for better reliability.

## 💰 Pricing

Pay-per-event pricing — you only pay for what you actually extract.

- **Actor Start:** $0.0001
- **result:** $0.0050

## 🔗 Related NexGenData Actors

- [Facebook Ads Library Scraper](https://apify.com/nexgendata/facebook-ads-library-scraper?fpr=2ayu9b)
- [SaaS Pricing Tracker](https://apify.com/nexgendata/saas-pricing-tracker?fpr=2ayu9b)

## 🚀 Apify Affiliate Program

New to Apify? Sign up with our [referral link](https://www.apify.com/?fpr=2ayu9b) — you get free platform credits on signup, and you help fund the maintenance of this actor fleet.

## 📚 More From NexGenData

Explore the full catalog, tutorials, Gumroad data packs, and newsletter at **[thenextgennexus.com](https://thenextgennexus.com)** — the brand home for everything we ship.

- 📖 Tutorials & how-to guides
- 🗂️ Full actor catalog with usage examples
- 📦 Gumroad data packs (one-time purchases)
- 📬 Newsletter — monthly drops of new actors and revenue experiments

---

*Built and maintained by [NexGenData](https://apify.com/nexgendata?fpr=2ayu9b) — 165+ actors covering scraping, enrichment, MCP servers, and automation.*
🏠 Home: [thenextgennexus.com](https://thenextgennexus.com)