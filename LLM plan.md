# GenAI / LLM Engineer Preparation Plan

A structured 8-week plan to prepare for a GenAI/LLM Engineering role covering Python, RAG, APIs, cloud, and LLMOps.

---

## 0. How to Use This Plan

- Treat it as a checklist, not a rigid schedule — compress or stretch weeks based on your current level.
- Each week has: **Concepts**, **Hands-on Build**, and **Checkpoint** (something you should be able to explain or demo).
- Keep one running GitHub repo called `genai-prep-portfolio` and commit each week's project to it — this becomes your interview talking-point + portfolio.

---

## Week 1: Python Fundamentals & OOP Refresher

**Concepts**
- Core Python: data structures, comprehensions, generators, decorators, context managers
- OOP: classes, inheritance, composition, abstract base classes, dataclasses
- Typing: `typing` module, `pydantic` models
- Error handling & logging best practices
- Writing testable code: `pytest`, mocking

**Hands-on Build**
- Refactor a small script into a clean OOP design (e.g., a `DocumentLoader` → `Chunker` → `Embedder` pipeline skeleton, no LLM yet)
- Add unit tests with `pytest` and logging with the `logging` module

**Checkpoint**
- Can you explain SOLID principles with a Python example?
- Can you write a pydantic model with validators?

---

## Week 2: FastAPI / Flask — Building & Serving APIs

**Concepts**
- REST basics: routes, request/response models, status codes
- FastAPI: path/query params, pydantic request/response schemas, dependency injection, async endpoints
- Middleware, exception handlers, CORS
- API docs via Swagger/OpenAPI (auto-generated in FastAPI)
- Basic auth: API keys, JWT

**Hands-on Build**
- Build a FastAPI service with:
  - `/health` endpoint
  - `/chat` endpoint that calls an LLM (start with OpenAI or Anthropic API) and returns a structured response
  - Request/response logging middleware
  - Dockerize it (`Dockerfile` + `docker-compose.yml`)

**Checkpoint**
- Can you explain sync vs async endpoints in FastAPI and when async matters for LLM calls?
- Can you demo the Swagger UI for your API?

---

## Week 3: LLM Fundamentals & Prompt Engineering

**Concepts**
- LLM basics: tokens, context windows, temperature, top_p, system vs user prompts
- Prompt engineering patterns: zero/few-shot, chain-of-thought, structured output (JSON mode), function/tool calling
- Prompt versioning and testing (treat prompts like code)
- Cost/latency tradeoffs across models (OpenAI, Azure OpenAI, Anthropic, Gemini, open-source)

**Hands-on Build**
- Build a small **prompt testing harness**: a script/notebook that runs the same task across multiple prompt variants and logs outputs, tokens used, and latency
- Implement structured output parsing (JSON schema + pydantic validation of LLM output)

**Checkpoint**
- Can you explain the difference between prompt engineering and fine-tuning, and when to use each?
- Can you show a before/after example where prompt tuning improved output quality?

---

## Week 4: RAG Pipeline — Core Build

**Concepts**
- RAG architecture: ingestion → chunking → embeddings → vector search → prompt assembly → generation
- Chunking strategies: fixed-size, recursive, semantic chunking; overlap tradeoffs
- Embedding models: OpenAI embeddings, sentence-transformers, Azure OpenAI embeddings
- Vector databases: FAISS (local), Chroma (local/dev), Pinecone/Qdrant/Weaviate (managed/prod)
- Metadata filtering and hybrid search (keyword + vector)

**Hands-on Build**
- Build an end-to-end RAG app:
  1. Ingest a set of PDFs/docs
  2. Chunk + embed + store in Chroma or FAISS
  3. Retrieve top-k chunks with metadata filters
  4. Assemble prompt with retrieved context
  5. Generate answer with citations back to source chunks
- Wrap it behind the FastAPI service from Week 2 as a `/ask` endpoint

**Checkpoint**
- Can you explain why chunk size/overlap affects retrieval quality?
- Can you explain hybrid search and when pure vector search fails?

---

## Week 5: Frameworks & Advanced Retrieval

**Concepts**
- LangChain / LlamaIndex: chains, agents, retrievers, memory
- LangGraph: stateful multi-step agent workflows
- Semantic Kernel (if Azure-focused role)
- Retrieval tuning: re-ranking (cross-encoders), query rewriting, multi-query retrieval, parent-child chunking

**Hands-on Build**
- Rebuild (or extend) your RAG app using LangChain or LlamaIndex to compare with your manual implementation
- Add a re-ranking step and a query-rewriting step; measure retrieval quality improvement

**Checkpoint**
- Can you justify why you'd choose LangChain/LlamaIndex vs. a custom pipeline for a given use case?
- Can you explain agentic workflows vs. simple RAG?

---

## Week 6: Evaluation, Safety & Governance

**Concepts**
- RAG evaluation: faithfulness, answer relevance, context precision/recall
- Tools: RAGAS, TruLens, DeepEval, custom eval harnesses with LLM-as-judge
- Safety/governance: PII redaction (Presidio), content filtering, prompt-injection mitigation, access control patterns
- Observability: logging, token usage tracking, latency tracking, tracing (LangSmith / OpenTelemetry)

**Hands-on Build**
- Add an evaluation harness (RAGAS or DeepEval) to your RAG app — run it against a small labeled Q&A set
- Add PII redaction (Presidio) as a pre-processing step and a basic content-safety filter on outputs
- Add structured logging with token usage + latency per request

**Checkpoint**
- Can you explain the difference between faithfulness and answer relevance metrics?
- Can you describe a prompt-injection attack and one mitigation for it?

---

## Week 7: ML Engineering & Cloud Deployment

**Concepts**
- Classical ML/NLP: scikit-learn pipelines, basic classification/forecasting, when to use ML vs. LLM
- Cloud deployment paths:
  - **AWS**: SageMaker (training/hosting), Lambda (serverless inference), ECS (containers)
  - **Azure**: Azure ML, Azure App Services, AKS
- CI/CD: GitHub Actions (build/test/deploy pipeline), Docker image publishing
- Basic data pipelines: Airflow/Prefect for scheduled ingestion refresh

**Hands-on Build**
- Deploy your Dockerized FastAPI RAG app to one cloud (pick AWS **or** Azure based on the role):
  - AWS: ECS Fargate or Lambda + API Gateway
  - Azure: App Service or AKS
- Add a GitHub Actions workflow: lint → test → build image → deploy
- (Optional) Add a scheduled Airflow/Prefect job that refreshes embeddings when source docs change

**Checkpoint**
- Can you walk through your CI/CD pipeline end-to-end?
- Can you explain the cost/scaling tradeoffs between serverless (Lambda) and container (ECS/AKS) deployment for an LLM API?

---

## Week 8: Integration, Mock Interviews & Portfolio Polish

**Concepts**
- End-to-end system design for a GenAI application (be ready to whiteboard this)
- Common interview themes: RAG vs fine-tuning, hallucination mitigation, latency/cost optimization, scaling vector search, multi-tenant data isolation

**Hands-on Build**
- Polish the portfolio repo: clean README, architecture diagram, setup instructions
- Write a 1-page **system design doc** for your RAG app: architecture, data flow, failure modes, scaling plan
- Do 2–3 mock interviews (behavioral + system design + live coding)

**Checkpoint**
- Can you whiteboard your RAG architecture from memory in under 5 minutes?
- Can you answer "how would you scale this to 10M documents / 1000 QPS?"

---

## Core Topics Cheat-Sheet (Quick Reference)

| Area | Must-Know Tools/Concepts |
|---|---|
| Language | Python (OOP, typing, async, testing) |
| API framework | FastAPI (preferred), Flask |
| LLM providers | OpenAI, Azure OpenAI, Anthropic, Gemini, open-source (Llama, Mistral) |
| RAG frameworks | LangChain, LlamaIndex, LangGraph, Semantic Kernel |
| Vector DBs | FAISS, Chroma, Pinecone, Qdrant, Weaviate |
| Evaluation | RAGAS, TruLens, DeepEval |
| Safety | Presidio (PII), content-safety filters, prompt-injection mitigation |
| Containerization | Docker (Kubernetes optional) |
| CI/CD | GitHub Actions, Azure DevOps, Jenkins |
| Data pipelines | Airflow, Prefect, Databricks |
| Cloud (AWS) | SageMaker, ECS, Lambda |
| Cloud (Azure) | Azure ML, AKS, App Services |

---

## Suggested Practice Projects (Pick 2–3 to Build Fully)

1. **Document Q&A Assistant** — Upload PDFs, ask questions, get cited answers (core RAG).
2. **Support Copilot** — Ingest a knowledge base + past tickets, suggest draft responses with confidence scores.
3. **Summarization Service** — Batch summarize long documents/meeting transcripts, exposed via FastAPI + async job queue.
4. **Hybrid Search Comparison Tool** — Same query set run through pure vector search vs hybrid (BM25 + vector) vs re-ranked, with an evaluation report.

---

## Interview Prep Angles to Rehearse

- **Explain RAG end-to-end** in 2 minutes, including failure modes (stale index, poor chunking, retrieval mismatch).
- **Prompt engineering vs fine-tuning vs RAG** — when each is the right tool.
- **Debugging a "hallucinating" RAG app** — walk through your diagnostic steps (check retrieval first, then prompt, then model).
- **Cost/latency optimization** — caching, smaller models for simple tasks, batching, streaming responses.
- **Security** — prompt injection, data leakage through embeddings, access control on retrieved data per user/tenant.
- **A time you improved response quality** — have a concrete before/after metric ready (even from a personal project).

---

## Weekly Time Budget (Suggested)

| Days | Focus |
|---|---|
| Mon–Fri (1–1.5 hrs/day) | Concepts + guided tutorials |
| Sat (3–4 hrs) | Hands-on build for the week |
| Sun (1 hr) | Review, write notes, update portfolio README |

---

## Final Pre-Interview Checklist

- [ ] Portfolio repo with 2–3 working GenAI projects, each with a README and architecture diagram
- [ ] One project deployed live on AWS or Azure (even a small demo)
- [ ] Can explain RAG, evaluation, and safety concepts without notes
- [ ] Comfortable writing a FastAPI endpoint and Dockerfile from scratch live
- [ ] Prepared 3–4 STAR-format stories for behavioral questions
- [ ] Reviewed the job description once more and mapped each bullet to a project or story you can reference
