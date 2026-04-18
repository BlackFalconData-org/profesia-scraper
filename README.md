# Profesia Scraper

Extract structured data from [profesia.sk](https://profesia.sk) — structured job listings from profesia.sk — Slovakia's largest job board. Get salary, contact info, company data, and more.

**[Profesia.sk Scraper - Slovakia Jobs on Apify →](https://apify.com/blackfalcondata/profesia-scraper?fpr=1h3gvi)**

---

## Key features





**Search with filters** — Search by keyword and location. Filter by remote work, salary period, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 5.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases





**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from profesia.sk on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from profesia.sk.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on profesia.sk to inform pricing decisions, hiring plans, or candidate negotiations.

**Lead generation**
Extract employer contact details alongside listings to build outreach lists for recruiters, staffing agencies, or B2B sales teams.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

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


## Output fields

Every listing returns the same 43-field schema. Missing values are `null` — never omitted.

- `jobId`
- `jobKey`
- `title`
- `company`
- `companyUrl`
- `companyId`
- `location`
- `remoteType`
- `description`
- `descriptionHtml`
- `descriptionLength`
- `salaryText`
- `salaryMin`
- `salaryMax`
- `salaryCurrency`
- `salaryType`
- `salaryGross`
- `employmentType`
- `postedDate`
- `validThrough`
- `startDate`
- `education`
- `benefits`
- `category`
- `positions`
- `contactName`
- `contactPhone`
- `contactEmail`
- `canonicalUrl`
- `applyUrl`
- `sourceUrl`
- `portalUrl`
- `sourceCountry`
- `sourceDomain`
- `searchQuery`
- `searchUrl`
- `isSponsored`
- `scrapedAt`
- `detailFetched`
- `contentQuality`
- `extractedEmails`
- `companyDescription`
- `companyEmployeeRange`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "7d4642914a31c15dac5a464b5caab429f7f6420c339963ec5c8bd3010ab1cea5",
  "jobKey": "5253969",
  "title": "FrontEnd Developer",
  "company": "Pro HR",
  "companyUrl": "https://www.profesia.sk/praca/pro-hr/C56404",
  "companyId": "56404",
  "location": "Práca z domu",
  "remoteType": "onsite",
  "description": null,
  "descriptionHtml": null,
  "descriptionLength": 0,
  "salaryText": "Od 3 700 EUR/mesiac"
}
```

*Truncated — full records contain 43 fields. See Output fields for the complete schema.*


**[Try Profesia.sk Scraper - Slovakia Jobs now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/profesia-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.002 |

See the [actor on Apify](https://apify.com/blackfalcondata/profesia-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data





- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal


## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---
---

*Last updated: 2026 03*
