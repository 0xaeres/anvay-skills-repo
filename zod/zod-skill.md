---
name: zod-skill
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
  anvay_product: zod
  anvay_tier: product_master
  anvay_parent: null
  anvay_related: []
  anvay_coverage:
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
    - Zod overview
  anvay_version: 1
  anvay_confidence: 0.4118
  anvay_eval_status: passed
  anvay_eval_summary: Skill passed Anvay quality eval.
  anvay_eval_failures: []
  anvay_quality_score: 1.0
  anvay_signals_used: []
  anvay_applies_to:
    files: []
    contexts: []
  anvay_provenance:
    council_session: cs_20260628_164720_ba1e85
    validated_by: ''
    validated_at: '2026-06-28T16:50:45.262914+00:00'
    evidence_chunks:
    - 222099de-3730-56cd-996f-6a22d2173919
    - a266ce52-2fa3-5897-8f8e-eba1375d52f0
    - f1f4fc05-3f94-5830-9bc9-4b6e044c29a2
    - 427b0c43-aebf-555e-838e-83f8d92d1726
    - 2c61f189-0983-5312-8e3a-2431ad2a6225
    - 5725d9b4-8b91-57f4-bd08-2ba08aa59e80
    - b83db33a-61d1-5d29-9146-648b50b90f80
    adversary_critique: null
    revision_count: 0
---

# zod-skill

## Use This Skill When
Use for product orientation, grounded development, review, debugging, and deciding when to query the
product knowledge base.

## Product Snapshot
Zod is a TypeScript-first schema declaration and validation library that enables runtime type
checking and compile-time type inference. It is primarily used by frontend and backend developers to
validate user input, API payloads, and configuration files. The runtime executes in Node.js and
browser environments, built on TypeScript with a modular package structure supporting both classic
and mini variants. [github:colinhacks/zod/packages/docs-v3/home.md:604] [file:
github:colinhacks/zod/packages/docs-v3/home.md:510]

## Product Language
- **ZodType**: The base interface/class representing a validated schema type in the classic/v3 API.
  [github:colinhacks/zod/packages/docs/content/v4/versioning.mdx:71] [file:
  github:colinhacks/zod/packages/zod/src/v4/classic/schemas.ts:926]
- **ZodMini**: A lightweight, functional-variant of Zod designed for strict bundle size constraints
  and tree-shaking. [github:colinhacks/zod/packages/docs/content/v4/index.mdx:400]
- **$ZodBase64Internals**: Internal schema definition interface extending string format internals
  for base64 validation. [colinhacks/zod/packages/zod/src/v4/core/schemas.ts:928]
- **ZodFailure**: Internal error class used in benchmarks and validation failure states, identified
  by a unique symbol key. [colinhacks/zod/packages/bench/instanceof.ts:6]
- **parse**: The core synchronous validation function that throws on invalid input and returns the
  inferred type. [github:colinhacks/zod/packages/docs/content/v4/index.mdx:0]

## Capabilities And Workflows
1. Runtime Schema Validation - Validates untyped data against declarative schemas at runtime,
   throwing or returning structured errors.
   [github:colinhacks/zod/packages/docs/content/index.mdx:151] [file:
   github:colinhacks/zod/packages/docs-v3/home.md:510]
2. Compile-Time Type Inference - Automatically derives TypeScript types from schema definitions for
   end-to-end type safety. [github:colinhacks/zod/packages/docs/content/index.mdx:151]
3. Bundle Optimization via Mini Variant - Provides a tree-shakeable, functional API subset for
   environments with strict size limits.
   [github:colinhacks/zod/packages/docs/content/v4/index.mdx:400]
4. JSON Schema Interop - Converts Zod schemas to JSON Schema and vice versa, with explicit error
   handling for unsupported features.
   [github:colinhacks/zod/packages/docs/content/json-schema.mdx:207]

## System Map
- **zod/v4/core**: The foundational runtime engine implementing base schema types and parsing logic.
  [github:colinhacks/zod/packages/docs/content/v4/index.mdx:0] [file:
  github:colinhacks/zod/packages/docs/content/v4/index.mdx:2]
- **zod/v4/mini**: The lightweight, functional API layer optimized for bundlers and tree-shaking.
  [github:colinhacks/zod/packages/zod/src/v4/mini/schemas.ts:4]
- **zod

v4/classic**: The standard, class-based API layer providing the full feature set and backward
compatibility with v3.
- **bench**: Internal benchmarking suite measuring object creation, instanceof checks, and safe
  parsing performance.
- **docs**: Documentation site and content repository hosting migration guides, API references, and
  ecosystem integrations.

## Data Model
- **ZodObject**: Represents object schemas with defined keys, required/optional fields, and
  passthrough/strict modes. [file: github:colinhacks/zod/packages/docs-v3/MIGRATION.md:31]
- **ZodString**: Represents string schemas with format constraints like email, url, uuid, and
  base64.
- **ZodIssueBase**: Internal error structure tracking validation failures, including path, code, and
  message.
- **ZodCoercedBigInt**: Specialized schema type for coercing string inputs into BigInt values during
  parsing.

## Interfaces And Contracts
- `parse(input, schema)`: Synchronous validation function that returns the parsed value or throws a
  ZodError. [file: github:colinhacks/zod/packages/docs-v3/home.md:2205]
- `safeParse(input, schema)`: Returns a result object `{ success: true, data } | { success: false,
  error }` without throwing.
- `z.object({...})`: Schema builder method defining object structures with key-value validators.
- `z.coerce.string()`: Schema builder that applies `String()` transformation before validation.

## Invariants And Constraints
1. A Zod 3 `ZodType` is not assignable to a Zod 4 `ZodType`, requiring explicit migration for
   library authors. [file: github:colinhacks/zod/packages/docs/content/json-schema.mdx:207]
2. JSON Schema conversion throws an error by default if the schema contains features not
   representable in JSON Schema.
3. The `parse` function is strictly synchronous and will throw immediately on the first validation
   failure encountered.

## How To Use The Knowledge Base
This skill is a map, not the territory. Trust it for orientation — product purpose, the system map,
contracts, invariants, and where things live. For anything you are about to change, read, or assert
as current, treat the knowledge base as source of truth and query it: code moves faster than this
skill.

Query the KB over MCP. Pick the tool by question shape:

- **Orientation / "which skill applies"** — `find_skills` then `get_skill`.
Start here to load product context before deeper retrieval.
- **General "how does X work" / open-ended evidence** — `evidence_search_corpus`.
Multi-channel retrieval (hybrid + grep + repo-map + graph-local + summaries), coverage-assessed. The
default for most questions.
- **Relational / "what calls what", "what depends on this", impact** —
`ask_product_graph`. Walks the per-product knowledge graph and synthesizes a cited answer. Use when
the question is about connections, not a single file.
- **Exact symbol / constant / string lookup** — `grep_corpus`. Deterministic
match against indexed chunks when you already know the token.
- **Symbol definition / signature lookup** — `query_code_context`.
- **Semantic / paraphrased search of code + docs** — `hybrid_search_corpus`
(dense + BM25 + rerank) when you want the low-level retrieval directly.

Rules of thumb:
- Cite file:line from retrieved evidence, not from this skill, when you make a
concrete claim about current code.
- If this skill and the KB disagree, the KB wins and this skill is stale —
report it via `report_outcome` so it gets re-validated.
- Prefer `ask_product_graph` for "why/how are these connected" and
`evidence_search_corpus` for "show me the relevant code".
## How To Work In This Product
1. Clone the monorepo and install dependencies using `pnpm install` in the root directory. [file:
   github:colinhacks/zod/packages/docs-v3/home.md:510]
2. Run the test suite with `pnpm test` to verify schema behavior across classic, mini, and core
   packages.
3. Build the packages using `pnpm build` to generate type definitions and transpiled JavaScript.
4. Run benchmarks located in `packages/bench` to validate performance changes before submitting PRs.
5. Follow standard TypeScript contribution guidelines, ensuring all new schemas include
   comprehensive type inference tests.

## Security And Secrets
- Do not rely on Zod for sanitizing untrusted input destined for SQL or HTML contexts; it validates
  types, not security policies. [file: github:colinhacks/zod/packages/docs-v3/home.md:510]
- Use `z.safeParse()` in production API routes to prevent unhandled exceptions from crashing the
  server.
- Avoid exposing internal error structures (`ZodIssueBase`) directly to end-users without filtering
  sensitive path information.

## Known Traps
- **Trap**: Assuming `z.coerce` applies transformations before validation; it actually transforms
  the input value, which can mask type errors if the coercion succeeds unexpectedly. [file:
  github:colinhacks/zod/packages/docs-v3/home.md:510]
- **Trap**: Using JSON Schema conversion on schemas with custom refinements or non-standard formats;
  Zod explicitly throws when encountering features unsound for JSON Schema.
- **Trap**: Mixing Zod v3 and v4 schemas in the same codebase; the type systems are incompatible and
  will cause TypeScript assignment errors.

## Freshness And Evidence
- Last-known stable state: Zod v4 is the current major version, with v3 released in 2021 and
  maintained for legacy support. [file:
  github:colinhacks/zod/packages/docs-v3/blog/clerk-fellowship.md:17]
- Files that change most often: `packages/zod/src/v4/core/schemas.ts` and
  `packages/zod/src/v4/mini/schemas.ts` contain the core validation logic.
- Re-verify migration guides and versioning docs before adopting v4 features, as internal APIs and
  breaking changes affect library authors.