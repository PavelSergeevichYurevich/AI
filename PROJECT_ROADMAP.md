# Project Roadmap

## Project Overview
AI backend service (FastAPI) for apps and bots.

What it does for users:
- accepts a request for text/data analysis,
- calls an LLM provider via a unified gateway,
- returns a structured, predictable response,
- is built to scale into RAG, tools, queues, and production patterns.

## How We Work
- Iterative cycle:
1. task,
2. implementation by user,
3. review,
4. fixes,
5. next step.
- Response format:
1. short theory first (`what / why / purpose`),
2. practical task second (`what we do / for what`),
3. no implementation details unless explicitly requested.

## Scope (What It Means)
Scope = boundaries of the current iteration:
- what is included now,
- what is explicitly postponed.

## Week 1 Scope
In scope:
- FastAPI project skeleton,
- `GET /health` and `GET /ready`,
- config system + `.env.example`,
- LLM client abstraction (interface + one provider),
- README with local run instructions,
- base tests for `health/ready`.

Out of scope:
- `POST /analyze`,
- RAG/embeddings/pgvector,
- queues/background workers,
- advanced observability,
- billing/subscriptions.

## Week 1 Plan (1-2 Evenings)

### 1) Define Week 1 Scope
- What we do: fix boundaries in README/sprint note.
- For what: avoid scope creep and close iteration in "done".
- Done criteria: clear `In scope / Out of scope`.

### 2) Build Project Skeleton
- What we do: create base structure and entrypoint.
- For what: predictable growth without "all-in-one-file" chaos.
- Done criteria: clear layered structure.

### 3) Add `GET /health`
- What we do: endpoint that confirms process is alive.
- For what: basic operational check.
- Done criteria: stable quick response, independent from externals.

### 4) Add `GET /ready`
- What we do: endpoint that confirms service readiness.
- For what: deploy/runtime readiness control.
- Done criteria: signals not-ready on critical init/config failure.

### 5) Add Config + `.env.example`
- What we do: centralized settings and env template.
- For what: reproducible launch across dev/test/prod.
- Done criteria: no secret hardcoding, clear required vars.

### 6) Add LLM Abstraction
- What we do: interface + one provider implementation.
- For what: provider swap and easier testing/mocking.
- Done criteria: API/service layer does not depend on provider SDK details.

### 7) Update README
- What we do: project goal, run steps, env vars, endpoint checks.
- For what: fast onboarding and portfolio clarity.
- Done criteria: project can be launched by README only.

### 8) Add Week 1 Tests
- What we do: tests for `health/ready` (happy path + edge cases).
- For what: baseline regression safety.
- Done criteria: green tests and meaningful failures on regressions.

### 9) Iteration Finish
- What we do: short changelog + demo note.
- For what: visible progress and clean handoff to Week 2.
- Done criteria: explicit "done / not done / why".

## Suggested Base Structure
```text
ai-backend/
  app/
    api/
    core/
    llm/
    services/
    schemas/
    main.py
  tests/
  alembic/
  .env.example
  README.md
```
