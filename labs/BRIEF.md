# Experiment: does LangGraph fit the OpenSec Analyst?

## Question

Does LangGraph give us tool calling, structured answers, follow-up memory and MLflow tracing for this agent, on real filings? Plan decision 1 has already chosen LangGraph. This lab confirms it works; it doesn't compare frameworks.

## Method

`labs/langgraph_lab.ipynb`, run top to bottom:

1. Fetch AMD's and NVIDIA's 10-Ks, 10-Qs and XBRL companyfacts for the window in plan decision 4, at no more than 9 requests a second, and cache them in `data/filings/`.
2. Split each filing by Item into chunks, embed them with OpenAI `text-embedding-3-large`, and search with vectors plus BM25, merged by reciprocal rank fusion. The index lives in memory.
3. Run a LangGraph agent (`create_agent` on `gpt-6.1-terra` at medium reasoning effort) with `search_passages`, `get_fact` and `compute` tools, a structured `Answer` output and an in-memory checkpointer.
4. Ask the samples in `data/labs/samples.yaml`. Log each run to MLflow, and score each answer in Python.

## Pass bar

- Every sample passes its checks: the reply is structured, citations pass, figures match XBRL, the "Not disclosed" sample is caught, the follow-up works, and refusals happen with no tool calls.
- Median latency is under 15 seconds.
- Every run has an MLflow trace with token counts.

## Decision

If the bar is met, LangGraph becomes the agent framework in `docs/TECH_STACK.md`. If not, stop and report. The result goes in `docs/STATUS.md`.
