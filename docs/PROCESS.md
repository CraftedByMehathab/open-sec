# Process

`uv sync` and `npm install` at the repo root install everything, including a git pre-commit hook. `docker compose up -d` starts Postgres and MLflow. `npm run dev` starts the backend and the frontend.

`npm run check` runs every check:

- Python: ruff (lint and format), pyright, and pytest with 80% coverage
- TypeScript: ESLint, Prettier, tsc, and vitest with 80% coverage
- Playwright end-to-end tests

The pre-commit hook runs the format, lint, type and unit test checks on every commit. `npm run evals` scores the agent on the test set with a real model; run it only when asked or at the end of a plan.

## Planning

When asked to plan, as in "Please plan the pilot", write the plan to `docs/PLAN.md` and write no code.

- Split the work into phases, usually 5 or 6, each building on the last. Name the requirement ids from `docs/SPEC.md` that each phase covers.
- Give each phase success criteria you can verify yourself: tests that pass, commands and their output, API calls and their responses, and pages checked in the browser with the Playwright MCP server. Write each as a checkbox.
- Then stop and wait until you are asked to implement the plan.

## Implementing

When asked to implement the plan, build every phase in order without stopping. For each phase:

1. Write tests from the requirements, then build until they pass.
2. Check every success criterion and fix whatever fails.
3. Tick off its criteria in `docs/PLAN.md` and update `docs/STATUS.md`.
4. Commit, naming the requirement ids. If the hook fails, fix it and commit again.

When the last phase is done, run `npm run check` and `npm run evals`, and report both.

## Labs

When asked to run an experiment, write its brief in `labs/`, use the fixed samples in `data/labs/`, log each run to MLflow, and record the result and decision in `docs/STATUS.md`. No product code imports from `labs/`.

## Rules

- Tests never call a model; use a stub model.
- Outside a plan, commit each change once you have checked it.
- Run `npm run check` before you hand work over.
- Never use `git commit --no-verify`.
- Never lower a threshold, turn off a rule or exclude a file to get a green run. If a rule looks wrong, stop and ask.
- Never push.
- Don't open the answers in `evals/` unless you're asked to.
