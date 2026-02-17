# AI Backend Roadmap (16 Weeks)

## Rules for Every Week
1. End each sprint with demo + README update + changelog.
2. Each endpoint has tests: happy path + 2 edge cases.
3. Every LLM feature has timeout, retry, logging, token/cost tracking.
4. CI runs tests and linter on each PR.

## Week 1 - Project Base and LLM Client
- Deliverables: FastAPI skeleton, config system, LLM client abstraction.
- Definition of Done:
1. `GET /health` and `GET /ready` work.
2. LLM client is swappable (interface + implementation).
3. `.env.example` and local run instructions in README.

## Week 2 - Structured Gateway v1
- Deliverables: `POST /analyze`, Pydantic schema, strict JSON output.
- Definition of Done:
1. Response is validated by schema.
2. Retry policy exists for invalid model JSON.
3. Tests cover valid and invalid model outputs.

## Week 3 - Reliability and Cost (Gateway v2)
- Deliverables: idempotency-key, rate limiting, token/cost tracking.
- Definition of Done:
1. Same `Idempotency-Key` does not duplicate processing.
2. Logs include latency, tokens_in, tokens_out, estimated_cost.
3. Per-user or per-IP rate limiting works.

## Week 4 - Evals and Stage 1 Hardening
- Deliverables: mini eval dataset, regression checks, basic dashboards.
- Definition of Done:
1. At least 30 eval test cases.
2. Script compares quality before and after changes.
3. Note in docs: why LLM should not be called directly from controller.

## Week 5 - RAG Foundation
- Deliverables: PostgreSQL + pgvector, schema for docs/chunks/embeddings.
- Definition of Done:
1. Alembic migrations create required tables.
2. Document upload and metadata storage work.
3. Vector index exists and is used.

## Week 6 - Ingestion Pipeline
- Deliverables: chunking service, embedding generation, async indexing.
- Definition of Done:
1. `POST /documents` starts ingestion.
2. Chunking is configurable (`size`, `overlap`).
3. Re-upload is idempotent and does not break index.

## Week 7 - Retrieval and Answer Generation
- Deliverables: semantic search endpoint + LLM answer from context.
- Definition of Done:
1. `POST /search` returns top-k chunks with score.
2. `POST /chat` answers using retrieved context.
3. Context is limited by token budget.

## Week 8 - RAG Production Features
- Deliverables: cache, index versioning, pagination, zero-downtime reindex.
- Definition of Done:
1. Index version switch is atomic.
2. Search supports pagination.
3. Reindex runs in background while old index remains available.

## Week 9 - Tool-Calling Architecture
- Deliverables: tool registry, strict tool schemas, dispatcher.
- Definition of Done:
1. Tools are registered centrally.
2. Calls are allowed only from allowlist.
3. Each tool call writes an audit log entry.

## Week 10 - Agent Loop and Guardrails
- Deliverables: bounded agent loop, policy checks.
- Definition of Done:
1. Max depth/steps and total timeout are enforced.
2. Invalid tool args are blocked before execution.
3. Fallback response exists for tool failures.

## Week 11 - Multi-Tool Flows
- Deliverables: semantic search + calculator + external API + internal service.
- Definition of Done:
1. At least 5 end-to-end multi-tool scenarios.
2. Decision chain trace is stored.
3. Tool failures do not crash whole request flow.

## Week 12 - Agent Evals and Security
- Deliverables: red-team cases, prompt-injection checks, policy tests.
- Definition of Done:
1. Attack prompt set with expected behavior exists.
2. Tool misuse is blocked by tests.
3. Limits and residual risks are documented.

## Week 13 - Observability Upgrade
- Deliverables: OpenTelemetry tracing, structured logging, core metrics.
- Definition of Done:
1. Trace and spans are visible per request.
2. Metrics include p50/p95 latency, error rate, token usage, cost/request.
3. Logs correlate by `request_id` and `user_id`.

## Week 14 - Reliability Upgrade
- Deliverables: timeout/retry matrix, circuit breaker, queue hardening.
- Definition of Done:
1. Each external call has explicit timeout + retries.
2. Circuit breaker prevents cascading failures.
3. Celery jobs have retries and dead-letter strategy.

## Week 15 - SaaS MVP Core
- Deliverables: auth, chat history, usage limits, subscriptions skeleton.
- Definition of Done:
1. JWT auth with basic roles (`user`, `admin`).
2. Request limits and quotas are tracked correctly.
3. Chat history is stored and scoped to user.

## Week 16 - SaaS MVP Finish
- Deliverables: admin dashboard, billing hooks, Dockerized deploy, final polish.
- Definition of Done:
1. Full stack runs via one Docker Compose command.
2. Admin can view usage, cost, active users.
3. Final demo, CV-ready case study, architecture diagram.

## Portfolio Outcomes
1. Structured LLM Gateway.
2. RAG API with pgvector.
3. Tool-calling Agent Backend.
4. Production observability/reliability upgrade.
5. AI SaaS MVP.

## Evening Study Mode
1. Multiply each sprint duration by 1.5.
2. Keep stage order unchanged and do not skip eval or production blocks.
