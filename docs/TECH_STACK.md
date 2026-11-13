# Tech stack

| Layer           | Choice                                                                      |
| --------------- | --------------------------------------------------------------------------- |
| Language        | Python 3.12 with uv, one root `pyproject.toml`                              |
| API             | FastAPI, Pydantic                                                           |
| Database        | Postgres 16 with pgvector; SQLAlchemy 2, Alembic                            |
| Search          | pgvector plus Postgres full-text                                            |
| SEC data        | `httpx`                                                                     |
| Parsing         | BeautifulSoup, lxml                                                         |
| Embeddings      | OpenAI `text-embedding-3-large`                                             |
| LLM             | `gpt-6.1-terra` at medium reasoning effort by default, or `MODEL_NAME`      |
| Agent framework | LangGraph (`create_agent`), confirmed in the Phase 0 lab                   |
| Frontend        | Vite, React, TypeScript, shadcn/ui (preset `b1uGaJrhQ`); Node (current LTS) |
| Observability   | MLflow tracing; logs via `structlog`                                        |
| Experiments     | Jupyter, tracked in MLflow                                                  |
| Quality         | `ruff`, `pyright`, `pytest`; ESLint, Prettier, vitest; Playwright           |
| Local run       | Docker Compose: Postgres, MLflow                                            |
| Secrets         | `.env`, with every key listed in `.env.example`                             |
