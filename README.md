# Cyber API Daily Feed

A Google Apps Script that aggregates daily cybersecurity intelligence from
multiple live sources and compiles everything into a formatted Google Doc,
ready for NotebookLM or manual review.

## Data Sources

| Source | Content |
|---|---|
| NIST NVD | Latest CVEs with CVSS severity scoring |
| CISA KEV | Known Exploited Vulnerabilities catalogue |
| GDELT | Global cybersecurity news events |
| Google News RSS | Curated cybersecurity headlines |
| arXiv | Latest cybersecurity and infosec research papers |
| MediaStack | Cybersecurity news API feed |
| YouTube | AI and cybersecurity video content |
| MITRE ATT&CK | Threat technique and tactic reference |
| Hacker News | Top cybersecurity community stories |

## Setup

1. Open [Google Apps Script](https://script.google.com) and create a new project
2. Paste the contents of `Code.js`
3. Set your API keys in **Project Settings → Script Properties**:
   - `GOOGLE_API_KEY` — YouTube Data API v3 key from Google Cloud Console
   - `MEDIASTACK_KEY` — from [mediastack.com](https://mediastack.com)
4. Run `runCyberSecAggregator()` to generate your first report

## Configuration

```js
const CONFIG = {
  MAX_CVE_RESULTS:     20,   // CVEs fetched per run
  MAX_YOUTUBE_RESULTS: 12,   // YouTube videos fetched
  CVE_LOOKBACK_DAYS:   7,    // CVE history window
  NEWS_LOOKBACK_DAYS:  3,    // News lookback window
};
```

## API Key Security

Keys are **not stored in this file**. Set them via:

**Apps Script → Project Settings → Script Properties**

```js
const API_KEY = PropertiesService.getScriptProperties().getProperty("GOOGLE_API_KEY");
```

## Automation

Run `createDailyTrigger()` once to schedule the report every day at 6am Sydney time.

## Test Mode

Swap the function call inside `testSingleSection()` to test any individual
data source in isolation before running the full aggregator.
