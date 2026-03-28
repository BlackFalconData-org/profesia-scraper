# Profesia Scraper

Extract structured data from [profesia.sk](https://profesia.sk) — structured job listings from profesia.sk — Slovakia's largest job board. Get salary, contact info, company data, and more.

**[Run on Apify →](https://apify.com/blackfalcondata/profesia-scraper)**

---

## Key features

🔍 **Smart search with filters**

Search by keyword, location, and multiple filters. Smart input resolution ensures you always get results.

📄 **Detail enrichment**

Fetch full job descriptions, salary data, employer profiles, and contact information for each listing.

🔄 **Incremental mode**

Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

⚡ **Compact output for AI agents**

Core-fields-only mode optimized for MCP and AI agent workflows. Description truncation to control output size.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from profesia.sk on a schedule. Export to CSV, JSON, or directly to your database.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from profesia.sk.

**AI and LLM workflows**
Use compact mode and description truncation to feed data into AI agents, MCP servers, and LLM pipelines without exceeding token budgets.

---

## Quick start

```json
{
  "query": "software engineer",
  "location": "bratislavsky-kraj",
  "maxResults": 20,
  "details": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords (e.g. "programátor", "software engineer"). Use JSON array for multi-query. |
| `location` | string | — | Region slug (e.g. "bratislavsky-kraj", "kosicky-kraj"). Use JSON array for multi-location. |
| `category` | string | — | Category slug from profesia.sk URL path (e.g. "informacne-technologie", "ekonomika-financie"). |
| `startUrls` | array | — | Direct profesia.sk search or job detail URLs. |
| `remoteFilter` | enum | — | Filter by remote work type. |
| `jobType` | string | — | Employment type filter slug from profesia.sk (e.g. "plny-uvazok" for full-time, "brigada" for part-time). |
| `salaryMin` | integer | — | Minimum salary filter (EUR). Works with Salary Period. |
| `salaryPeriod` | enum | `"m"` | Monthly or hourly for the salary filter. |
| `maxResults` | integer | `50` | Maximum total job listings to return (0 = unlimited). |
| `maxPages` | integer | `5` | Maximum SERP pages to scrape per search source. |
| `includeDetails` | boolean | `true` | Fetch each job's detail page for full description, salary, contact info, and company data. |
| `includeCompanyProfile` | boolean | `false` | Enrich each listing with company profile data (description, employee range). |
| `descriptionMaxLength` | integer | `0` | Truncate description to this many characters. 0 = no truncation. |
| `compact` | boolean | `false` | Output only core fields (for AI-agent/MCP workflows). |
| `incrementalMode` | boolean | `false` | Track new/changed/removed jobs across runs. Requires stateKey. |
| `stateKey` | string | — | Stable identifier for the tracked search universe (e.g. "sk-it-bratislava"). |
| `emitUnchanged` | boolean | `false` | When incremental, also emit records that haven't changed. |
| `emitExpired` | boolean | `false` | When incremental, also emit records no longer found. |

---

## FAQ

<!-- WRITE: 4-6 Q&A pairs relevant to this product -->

**Is it legal to scrape profesia.sk?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->

---

## Related products by Black Falcon Data

| Product | Description |
|:--------|:------------|
| [StepStone Jobs API](https://github.com/BlackFalconData-org/stepstone-jobs-api) | Job listings from 18 European portals |
| [Company Jobs Tracker](https://github.com/BlackFalconData-org/company-jobs-tracker-api) | Track new/removed jobs per company |
| [Indeed Jobs Feed](https://github.com/BlackFalconData-org/indeed-jobs-feed) | Indeed job listings with salary data |
| [Glassdoor Jobs Feed](https://github.com/BlackFalconData-org/glassdoor-jobs-feed) | Glassdoor listings with company ratings |
| [Arbeitsagentur Jobs Feed](https://github.com/BlackFalconData-org/arbeitsagentur-jobs-feed) | Germany's federal job portal (1M+ listings) |
| [Naukri Jobs Feed](https://github.com/BlackFalconData-org/naukri-jobs-feed) | India's largest job portal |
| [Bilbasen Scraper](https://github.com/BlackFalconData-org/bilbasen-scraper) | Denmark's largest car marketplace |

---

*Last updated: 2026 03*
