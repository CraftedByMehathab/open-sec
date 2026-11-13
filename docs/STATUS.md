# Status

Phase 0 is done: LangGraph passed the lab and is now the agent framework. Next is Phase 1, ingest.

## What's built

- **Repo tooling:** uv, npm scripts, ruff, pyright, a pre-commit hook, `.env.example`, and Docker Compose with Postgres 16 + pgvector and MLflow.
- **`data/tickers.yaml`:** AMD and NVIDIA.
- **`data/labs/samples.yaml`:** 10 draft questions, a follow-up and 2 refusal checks, all `reviewed: false` until an analyst checks them.
- **`labs/langgraph_lab.ipynb`:** the Phase 0 lab (brief in `labs/BRIEF.md`).

## How to run it

```sh
uv sync && npm install      # installs everything and the pre-commit hook
cp .env.example .env        # then fill in the keys and SEC_USER_AGENT
docker compose up -d        # Postgres on 5432, MLflow on http://localhost:5001
npm run check               # ruff, ruff format, pyright
cd labs && uv run jupyter nbconvert --to notebook --execute --inplace langgraph_lab.ipynb
```

The notebook caches filings and embeddings in `data/filings/`, which git ignores. Reruns only call the model.

## Lab: LangGraph (Phase 0)

Run on 2026-11-13 with `gpt-6.1-terra` at medium reasoning and `text-embedding-3-large`, over 29 filings (15 AMD, 14 NVIDIA) and 3,888 passages.

| Check                                               | Result                   |
| --------------------------------------------------- | ------------------------ |
| Samples passing every check (12 plus the follow-up) | 13 of 13                 |
| Most EDGAR requests in any second                   | 9                        |
| Median latency                                      | 7.3 s (max 17.2 s, risk) |
| Median tokens per answer                            | 5,706                    |
| Answers with one MLflow trace and token counts      | 13 of 13                 |

**Decision:** LangGraph (`create_agent`, with a structured `Answer` output and a checkpointer) is the agent framework. `docs/TECH_STACK.md` is updated.

What the lab taught us, for Phases 1 and 2:

- **Fiscal labels:** companyfacts tags each value with the fiscal year of the filing that reported it, not of the period. Labels have to come from the filing that closes the period.
- **Revisions:** about 1,300 facts differ between filings. Most are reclassifications in older periods. A value whose sign alone flipped is a tagging change and isn't flagged.
- **Answer format:** the model sometimes skips the table or bullets. Rejecting the answer and retrying on the same thread fixes it.
- **Periods in the text:** the model must not write a period next to a figure, because Python already adds one.
- **Tracing:** each answer needs one parent trace, or its retries split into several traces (R-06).

## The last eval run

None yet. `npm run evals` scores the agent against `evals/` and reports each target in `docs/SPEC.md` (R-13).

## Decisions

- **Agent framework:** LangGraph, confirmed in Phase 0.
- **Models:** `gpt-6.1-terra` at medium reasoning effort, and OpenAI `text-embedding-3-large` for embeddings. Both replace the earlier Claude and Voyage AI choices.
- **Approved exceptions to `docs/CODE_STANDARDS.md` rule 10:** the agent's LangGraph checkpointer writes the `agent_state` schema, and `evals/` uses an LLM judge.

## Known gaps

- **Segment figures:** companyfacts has no dimensional (segment) facts, such as NVIDIA's Data Center revenue. Answering those from XBRL means parsing each filing's XBRL instance, which no phase covers yet.
- **pytest:** not yet in `npm run check`. It joins in Phase 1 with the first product code.
- **Cost:** not computed yet, because `PRICE_INPUT_PER_MTOK` and `PRICE_OUTPUT_PER_MTOK` are empty.
- **Companies:** the other 18 wait on SPEC open question 1.
- **Samples:** an analyst still has to check `data/labs/samples.yaml`. `evals/` has no questions yet.
