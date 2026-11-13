# OpenSec

## Context

OpenSec is an asset manager. Its analysts spend about 3 hours reading each SEC filing by hand. The pilot is a tool that answers their questions in seconds, citing the filing for every claim.

- **Scope:** about 20 companies, 3 years of 10-K and 10-Q filings, from SEC EDGAR
- **Done when:** 90% or more of answers are accurate, every claim is cited, figures match XBRL, and the median answer takes under 15 seconds

## Start here

IMPORTANT: read these in full before you plan, build, change or answer anything:

1. `docs/SPEC.md`: the business need
2. `docs/TECH_STACK.md`: the tech choices
3. `docs/CODE_STANDARDS.md`: how to write code
4. `docs/PROCESS.md`: how to plan, build and check
5. `docs/BRAND.md`: the look
6. `docs/STATUS.md`: what's built and how to run it
7. `docs/PLAN.md`: the pilot plan. Later plans get their own file, such as `docs/PLAN_HARNESS.md`

## Your role

- `docs/` holds OpenSec's requirements. Treat them as the customer's.
- You are their coding agent. They direct and review; you plan, build and check, following `docs/PROCESS.md`.
- In each plan, say what each phase builds and why.
- Explain your work at the level they ask for.

## Rules

- Never invent figures. If the filings lack it, say "Not disclosed in the filings."
- Cite every claim. Figures must match XBRL.
- Do all math in Python, never in the LLM.
- Keep SEC EDGAR calls under 10 per second, with the User-Agent from `.env`.
- Never commit `.env` or keys.
- If `docs/` conflict or are silent, ask. Don't guess.
- A change is done when tests and lint pass.
- After each build, update `docs/STATUS.md`.

## Folders

| Folder      | Holds                                                |
| ----------- | ---------------------------------------------------- |
| `docs/`     | Product docs                                         |
| `frontend/` | Analyst web UI: chat and cited sources               |
| `ingest/`   | Offline pipeline: fetch, parse, chunk, embed, load   |
| `backend/`  | The one API (`/ask`); runs the agent; data access    |
| `agent/`    | LLM agent and its tools, used by the backend         |
| `e2e/`      | End-to-end tests                                     |
| `evals/`    | 50-question test set and scoring script              |
| `data/`     | OpenSec's data: tickers, cached filings, lab samples |
| `labs/`     | Notebooks and the experiments brief                  |
| `assets/`   | Images for the notebooks                             |
