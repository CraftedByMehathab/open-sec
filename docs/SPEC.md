# The filings pilot

From the head of research operations at OpenSec.

Our equity analysts read each 10-K and 10-Q by hand to find what changed and compare it with past filings and peers. That takes about 3 hours a filing, or 120 hours a quarter. We want an AI agent, the OpenSec Analyst, to answer their questions in seconds, with answers they trust without rereading the filing.

## What it does

- Answers facts, period changes, peer comparisons and risk questions. (R-01)
- Replies with a short summary, then a table or bullets, then caveats. (R-02)
- Cites every claim; the cited passage shows beside the answer, highlighted. (R-03)
- Keeps context for follow-ups, such as "and last year?" (R-04)
- Shows every figure with its unit and period, such as $1,250.0M in FY2025. (R-05)
- Lets us review any answer later: question, sources, steps and cost. (R-06)

## Rules

- Never estimate a figure. If the filings don't say, answer "Not disclosed in the filings." (R-07)
- Figures match the company's XBRL data exactly. (R-08)
- Label fiscal and calendar periods; flag restated figures. (R-09)
- No investment advice or stock prices; politely refuse anything outside the filings. (R-10)
- The agent never sees the test answers in `evals/`. (R-11)

## Data

The companies in `data/tickers.yaml`, with their 10-K and 10-Q filings from the last 3 fiscal years, from SEC EDGAR (a contact in each request, under 10 requests a second). New filings can be added on demand. (R-12)

## How we'll judge it

50 test questions answered by our analysts: 20 facts, 15 comparisons, 10 risk, 5 with no answer. Pass: 90% accurate, 95% of citations support their claim, every figure matches XBRL, 90% correct "Not disclosed", median answer under 15 seconds. (R-13)

## Not for now

8-K, Form 4 and proxy filings; more than about 20 companies; sign-in; exports.

## Open questions

1. Which sector and which 20 companies?
2. Who writes and checks the 50 test answers?