---
name: nexus-engine-skill
description: Use for product orientation, grounded development, review, debugging,
  and deciding when to query the product knowledge base.
compatibility:
  agents:
  - codex
  - claude
  - cursor
  - continue
  format: agent-skills
metadata:
  nexus_product: nexus-engine
  nexus_tier: product_master
  nexus_parent: null
  nexus_related: []
  nexus_coverage:
    repos: []
    applications: []
    topics:
    - product
    - architecture
    - data model
    - interfaces
    - workflows
    - testing
    - security
    - knowledge base
    - Nexus-engine overview
  nexus_version: 1
  nexus_confidence: 0.6429
  nexus_eval_status: passed
  nexus_eval_summary: Skill passed Nexus quality eval.
  nexus_eval_failures: []
  nexus_quality_score: 1.0
  nexus_signals_used: []
  nexus_applies_to:
    files: []
    contexts: []
  nexus_provenance:
    council_session: cs_20260621_095611_e2ad42
    validated_by: ''
    validated_at: '2026-06-21T09:59:48.243345+00:00'
    evidence_chunks:
    - 96e09190-2b91-5dc6-bd48-86b1cf6cb06e
    - 25588adf-fa03-5025-80f2-3c234e02ef3f
    - 8a48c686-4965-5ab1-99ba-e4d3d280b59d
    - b921afda-62bc-5920-8d6b-48270c398c57
    - 5c865a41-3b4f-5b61-ae0c-1d1f1b7cf553
    - 16644c71-f312-5fe3-b7ba-07166a41475c
    - 5a5c3371-2154-5f3a-bc0e-f35e904eebb1
    - f380b8c4-882b-5c6d-be8e-2a824eecf04f
    - 1b2d2bd8-ca7d-5acc-87b5-ee7518c76deb
    adversary_critique: null
    revision_count: 0
---

# nexus-engine-skill

## Use This Skill When
Use this skill for product orientation, grounded development, review, debugging, and deciding when
to query the product knowledge base for the nexus-engine product. It provides the canonical overview
of purpose, language, system map, contracts, data model, workflow, security, traps, and KB use.

## Product Snapshot
Nexus-engine is a product-system intelligence platform that ingests codebases and documents into a
unified knowledge graph, enabling humans and AI agents to ask complex product questions with
source-level citations. It is used by developers and AI agents for architecture understanding, code
review, and debugging. The primary runtime is a Python FastAPI application with a SQLite registry
and FalkorDB graph index, deployed via uvicorn. [file:
github:0xaeres/nexus-ui/components/screens/LandingPage.tsx:8]

## Product Language
- **Product Mapper**: Extracts identity, domain vocabulary, entities, apps, services, repos, APIs,
  schemas, and boundaries from a product. [file: github:0xaeres/nexus-core/CONTRIBUTING.md:38]
- **Engineering Mapper**: Extracts commands, toolchain, tests/evals, code standards,
  security/secrets, debugging, and review signals.
- **Council**: The multi-agent workflow (planner → domain/quality experts → synthesizer → repair →
  skill_eval → finalizer) that generates product skills.
- **Chunk**: A unit of ingested content with context, stored and retrieved for RAG.
- **Skill**: A curated, versioned Markdown document providing product-specific guidance, generated
  by the Council.
- **Evidence**: Source-level citations (file paths with line numbers) that back factual claims in
  skills.
- **Graph Store**: A derived product-system topology index (FalkorDB) for services, modules, APIs,
  schemas, and dependencies.
- **MCP Server**: The Model Context Protocol server exposing Nexus tools to AI agents.

## Capabilities And Workflows
1. Ingestion Pipeline - Parses and stores codebases, documents, symbols, APIs, and metadata into a
   unified knowledge graph. [file: github:0xaeres/nexus-ui/components/screens/LandingPage.tsx:8]
2. Retrieval Pipeline - Answers complex product questions with context-aware responses backed by
   explicit source-level citations.
3. Council Skill Generation - Orchestrates a multi-agent workflow to produce curated, validated
   product skills from fresh evidence.
4. MCP Tool Exposure - Serves retrieval and skill tools to AI agents via the Model Context Protocol.
5. Code Retrieval Evaluation - Runs automated evals to measure retrieval quality and faithfulness of
   generated answers.

## System Map
- **nexus/api/**: FastAPI application exposing REST endpoints; entrypoint via `nexus/api/app.py`
  called by uvicorn. [file: github:0xaeres/nexus-core/CONTRIBUTING.md:4]
- **nexus/mcp_server/**: MCP server implementation exposing Nexus tools to AI agents.
- **nexus/registry.py**: SQLite-based source manifest and sync source of truth.
- **nexus/ingest/**: Ingestion pipeline including chunker (`nexus/ingest/chunker.py`) and models
  (`nexus/ingest/models.py`).
- **nexus/council/**: Multi-agent Council workflow for skill generation; agents in
  `nexus/council/agents/`.
- **nexus/graph/**: Graph store and retrieval logic, including `GraphRAGAnswer` model.
- **evals/**: Evaluation harness and suites (`evals/harness.py`, `evals/run_code_eval.py`).
- **FalkorDB**: Required derived graph index for multi-hop topology queries.

## Data Model
- **Chunk**: Represents an ingested content unit with context; stored in the graph store; used for
  retrieval. [file: github:0xaeres/nexus-ui/components/screens/LandingPage.tsx:8]
- **GraphRAGAnswer**: Pydantic model for structured RAG responses with citations.
- **Skill**: Markdown document with required sections (Data Model, Interfaces and Contracts,
  Invariants and Constraints, etc.); validated for completeness and citation faithfulness.
- **EvidenceChunk**: Internal representation of a cited source with file path and line range.
- **Source Manifest**: SQLite registry tracking ingested codebases and documents.

## Interfaces And Contracts
- `nexus/api/routes/`: REST API contracts for querying and managing the knowledge graph. [file:
  github:0xaeres/nexus-core/ENGINEERING.md:4]
- MCP tools: Exposed via `nexus/mcp_server/` for AI agent consumption; includes retrieval and skill
  tools. [file: github:0xaeres/nexus-core/ENGINEERING.md:4]
- `evals/harness.py`: Unified CLI entrypoint for running retrieval, RAG answer, and code retrieval
  eval suites. [file: github:0xaeres/nexus-core/evals/harness.py:1]

## Invariants And Constraints
1. SQLite is the sync source of truth; FalkorDB is a required derived graph index and must be
   available at runtime. [file:
   github:0xaeres/nexus-core/docs/product-system-intelligence-architecture.md:12]
2. Product skills must include locked sections: Data Model, Interfaces and Contracts, Invariants and
   Constraints, with citations for all factual claims.
3. The Council workflow must perform fresh retrieval at each expert node so the Synthesizer sees
   more than the planner's initial chunk pool.
4. Skill validation rejects unknown legacy shapes and requires anchored citations for factual
   sections.
5. Evidence citations must reference real file paths and line numbers; fabricated citations are
   replaced before evaluation.

## How To Use The Knowledge Base
Query the product knowledge base when you need fresh, source-level evidence beyond this skill's
static snapshot. Use `find_skills` to locate curated guidance for specific topics. Use
`query_code_context` for symbol, definition, or implementation lookups. Use `hybrid_search_corpus`
for open-ended semantic search across the entire ingested corpus. This skill alone is sufficient for
high-level orientation and stable architectural facts. Always retrieve fresh evidence when working
on PRs, debugging, or verifying claims that may have changed since this skill was generated.

## How To Work In This Product
1. Clone the repo and install dependencies as described in the project README. [file:
   github:0xaeres/nexus-core/evals/harness.py:1]
2. Run the API locally with `uvicorn nexus.api.app:app` (or via the configured entrypoint).
3. Ensure FalkorDB is running alongside SQLite for full graph capabilities.
4. Follow the contribution guidelines in `CONTRIBUTING.md` for PRs and code standards.
5. Use the eval harness (`python -m evals.harness`) to run test suites before submitting changes.
6. When adding or modifying skills, adhere to the required section structure and citation rules
   enforced by the skill validator.

## Security And Secrets
- `NEXUS_TOKEN_KEY` is constrained by `nexus/auth/token_cipher.py` and must be kept secret. [file:
  github:0xaeres/nexus-core/README.md:0]
- Security patterns are extracted by the Engineering Mapper during skill generation. [file:
  github:0xaeres/nexus-core/nexus/council/agents/pack.py:77]

## Known Traps
- **Trap**: Assuming the skill's static content is always up-to-date. The Council regenerates skills
  periodically, but code changes may outpace regeneration. Always verify with fresh retrieval for
  critical work. [file: github:0xaeres/nexus-core/nexus/council/agents/pack.py:898]
- **Trap**: Violating the SQLite-as-source-of-truth invariant by treating FalkorDB as the primary
  store. FalkorDB is a derived index and may be rebuilt; SQLite holds the canonical state.
- **Trap**: Omitting citations for factual claims in product skills. The validator will reject
  skills with uncited factual sections, and the repair loop will attempt to anchor them.

## Freshness And Evidence
- Last-known stable state: The Council workflow and skill validation tests are actively maintained;
  see `tests/test_drafter_faithfulness.py` and `tests/test_product_skill_validation.py` for the
  latest constraints. [file: github:0xaeres/nexus-core/nexus/council/agents/pack.py:898]
- Files that change most often: Council agents (`nexus/council/agents/`), skill parser
  (`nexus/council/skill_parser.py`), and eval harness (`evals/harness.py`).
- Before relying on this skill, re-verify the ingestion pipeline, retrieval pipeline, and Council
  workflow by checking `ENGINEERING.md` and the latest test outcomes.