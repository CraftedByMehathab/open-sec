# Code standards

1. Keep it simple, do not overcomplicate. This wins over every rule below.
2. Readable over clever. Small files (split past about 200 lines) and short functions.
3. Meaningful names that say what a thing is or does. No `utils.py`, `helpers.py` or unclear abbreviations.
4. Comments only when necessary.
5. Be concise: a short README and no emojis. Use Mermaid diagrams where a flow or structure is clearer as a picture.
6. IMPORTANT: avoid overly defensive code. Handle exceptions only when necessary.
7. Use uv: ALWAYS `uv run`, NEVER `python3`.
8. Python: type hints, `ruff` and `pyright` clean. TypeScript: strict mode, never `any`.
9. Spec-driven: no code without a need in `docs/SPEC.md` and a phase in `docs/PLAN.md`. Tests come from the phase's success criteria.
10. Separation of concerns: one module, one job; logic in pure functions, I/O at the edges. Calls flow one way: `frontend/` → `backend/` routes → `agent/` → data access → database. Routes stay thin; only `agent/` calls the LLM; only `ingest/` writes the database.
11. SOLID: extend by adding modules, not editing them; keep SEC EDGAR, the LLM and embeddings behind small swappable interfaces. Add an abstraction only when there are two real uses.
12. Backend API operations have an `operation_id`, a one-line docstring and no optional inputs.
13. Test behavior, not internals; mock only external services.
