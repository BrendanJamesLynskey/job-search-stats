# job-search-stats

Rolling time-series of UK job-market open-position counts in four target areas — Agentic AI / LLM, HW / Power / SI / PI, FPGA / RTL, DSP — split between UK-wide and Yorkshire + Greater Manchester windows of 7 days and 30 days.

Populated daily by a scheduled Claude Code remote agent that searches Indeed UK (with LinkedIn / Reed fallback), gap-fills missing cells from this history, and appends a fresh snapshot to `stats/history.csv` each morning. The same agent also drafts a separate top-5 job-match email.

## Data

`stats/history.csv` — one row per (date, area):

| Column | Description |
| --- | --- |
| `date` | ISO YYYY-MM-DD |
| `area` | One of `Agentic AI / LLM`, `HW / Power / SI / PI`, `FPGA / RTL`, `DSP` |
| `uk_7d` | Open postings UK-wide in last 7 days |
| `uk_30d` | Open postings UK-wide in last 30 days |
| `ym_7d` | Open postings in Yorkshire + Greater Manchester in last 7 days |
| `ym_30d` | Open postings in Yorkshire + Greater Manchester in last 30 days |
| `primary_query` | Search query string used for this row |
| `sources_used` | Comma-separated source labels (`indeed_uk`, `linkedin`, `reed`, `carry_forward`) |
| `notes` | Free-text annotations (carry-forward provenance, source failures) |

Empty numeric cells mean every live source AND history lookup failed for that cell on that day.
