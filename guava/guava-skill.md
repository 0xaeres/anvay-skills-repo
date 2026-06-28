---
name: guava-skill
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
  anvay_product: guava
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
    - Guava overview
  anvay_version: 1
  anvay_confidence: 0.7
  anvay_eval_status: passed
  anvay_eval_summary: Skill passed Anvay quality eval.
  anvay_eval_failures: []
  anvay_quality_score: 1.0
  anvay_signals_used: []
  anvay_applies_to:
    files: []
    contexts: []
  anvay_provenance:
    council_session: cs_20260628_153915_67f2a1
    validated_by: ''
    validated_at: '2026-06-28T15:53:48.034398+00:00'
    evidence_chunks:
    - 9176579b-0b71-5782-9ff2-b093f5ac09a8
    - 042375c2-69cd-59f8-a3b4-d5d263ef8ee1
    - 76829925-ae17-5a08-86b5-6b15fc2fbee0
    - 0621ab0c-242c-5117-9ae8-d52e0218cffa
    - 36c1ff8b-a73d-583b-8a14-aac71aff6d00
    - 4fb47bf5-e75a-5bae-836c-304f0832c7bb
    - 0aee30c9-e6c7-5030-a393-422179b35f0a
    - ccffd248-544c-55b1-8bac-2dc1da4d0fe2
    - d0434a2a-7c1e-5dc1-a53f-6da6c4cd76d5
    - 5e9d611e-3639-5ad9-a54f-0c8454338ae9
    - cc73ad5c-6da8-5b56-9a4d-f9586bb86193
    - 4a091978-d143-5686-8672-11c8c1bcf671
    - 09019201-74a7-56da-8c68-54f81b8f1bfc
    - ae1a7eee-cf1b-5036-bf88-05f24a2501b0
    - 20cababb-fa8b-5a2e-8965-95722117f21b
    - 434c277c-bbf1-5044-a005-26e50b04d0a0
    adversary_critique: null
    revision_count: 0
---

# guava-skill

## Use This Skill When
Use for product orientation, grounded development, review, debugging, and deciding when to query the
product knowledge base.

## Product Snapshot
Guava is a comprehensive, open-source Java library developed by Google that extends the Java
standard library with robust utilities for collections, caching, primitives, concurrency, I/O, and
more. It is primarily used by Java and Android developers to write cleaner, safer, and more
efficient code. The primary runtime is the JVM, targeting Java 8+ and Android API levels,
distributed as a single JAR or via Maven/Gradle. [file:
github:0xaeres/guava-fork/android/guava/src/com/google/common/base/JdkPattern.java:0]

## Product Language
- **ImmutableCollection**: A collection that cannot be modified after creation, ensuring
  thread-safety and preventing accidental state mutation. [file:
  github:0xaeres/guava-fork/android/guava-tests/test/com/google/common/collect/MultimapsTest.java:1]
- **ListenableFuture**: An extension of `java.util.concurrent.Future` that allows registering
  callbacks to be executed when the computation completes.
- **CacheBuilder**: A fluent builder for constructing `Cache` instances with configurable
  expiration, eviction, and loading policies.
- **Multimap**: A collection that maps keys to multiple values, generalizing the standard `Map<K,
  Collection<V>>` pattern.
- **Stopwatch**: A simple utility for measuring elapsed time, abstracting away `System.nanoTime()`
  calls.
- **Throwables**: A utility class for working with exceptions, providing methods to propagate,
  chain, and extract root causes.

## Capabilities And Workflows
1. Immutable Collections - Provides factory methods and builders to create unmodifiable collections
   that prevent runtime `UnsupportedOperationException` and ensure thread safety. [file:
   github:0xaeres/guava-fork/android/guava/src/com/google/common/base/Strings.java:246]
2. Advanced Caching - Offers a powerful, in-memory caching system with size-based eviction,
   time-based expiration, and custom value loading via `CacheLoader`.
3. Concurrency Utilities - Supplies `ListenableFuture`, `ServiceManager`, and thread pool utilities
   to simplify asynchronous programming and lifecycle management.
4. String and Primitive Utilities - Provides safe parsing, formatting, and comparison methods for
   strings, numbers, and characters that handle edge cases better than JDK defaults.

## System Map
- **com.google.common.base**: Core utilities including `Strings`, `Stopwatch`, and `Throwables`.
  [file: github:0xaeres/guava-fork/android/guava/src/com/google/common/base/Strings.java:246]
- **com.google.common.collect**: Collection extensions including `ImmutableCollection`, `Multimap`,
  and `MapMaker`. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/collect/ImmutableCollection.java:50]
- **com.google.common.util.concurrent**: Concurrency tools including `ListenableFuture` and
  `RateLimiter`. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/util/concurrent/ListenableFuture.java:31]
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

## Data Model
- **ImmutableCollection**: A read-only collection wrapper; invariants include that it cannot be
  modified after creation to ensure thread-safety. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/collect/ImmutableCollection.java:50]
- **Multimap**: A mapping of keys to multiple values; specialized as `ImmutableSetMultimap` or
  `ImmutableListMultimap` to provide well-defined `equals` semantics. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/collect/ImmutableMultimap.java:53]
- **Cache**: An in-memory key-value store managed by `CacheBuilder` with configurable eviction and
  expiration policies. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/cache/CacheBuilder.java:56]

## Interfaces And Contracts
- **ListenableFuture**: An extension of `java.util.concurrent.Future` that supports registering
  callbacks for completion. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/util/concurrent/ListenableFuture.java:31]
- **Converter**: A functional interface for converting values from one type to another. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/base/Converter.java:2]
- **RateLimiter**: A contract for controlling the rate of task execution (e.g., limiting to 2 tasks
  per second). [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/util/concurrent/RateLimiter.java:61]

## Invariants And Constraints
1. Immutable collections must not be modified after creation to prevent
   `UnsupportedOperationException` and ensure thread safety. [file:
   github:0xaeres/guava-fork/android/guava/src/com/google/common/collect/ImmutableCollection.java:50]
2. `ImmutableSet` and `ImmutableList` must maintain well-defined `equals` semantics to avoid bugs
   and confusion. [file:
   github:0xaeres/guava-fork/android/guava/src/com/google/common/collect/ImmutableCollection.java:50]
3. Building an immutable collection via a builder must not change the state of the builder, allowing
   it to be reused to build again. [file:
   github:0xaeres/guava-fork/android/guava/src/com/google/common/collect/ImmutableSet.java:454]

## How To Work In This Product
- **Development**: Target the JVM for Java 8+ or Android API levels. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/base/JdkPattern.java:0]
- **Testing**: Use the `guava-tests` module for verifying collection and utility behavior. [file:
  github:0xaeres/guava-fork/android/guava-tests/test/com/google/common/collect/MultimapsTest.java:1]
- **Debugging**: Use `FakeTimeLimiter` to swap out real time-limiters during debugging to avoid
  annoying timeouts. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/util/concurrent/FakeTimeLimiter.java:32]

## Security And Secrets
- **Privilege Checks**: Certain internal operations, such as those in `FinalizableReferenceQueue`,
  may throw `SecurityException` if appropriate privileges are missing. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/base/FinalizableReferenceQueue.java:283]
- **Reflection**: Use of reflection to load internal classes (e.g., `SharedSecrets`) is marked with
  `@J2ktIncompatible`. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/base/Throwables.java:449]

## Known Traps
- **EventBus Debugging**: Using `EventBus` makes cross-references between producers and subscribers
  harder to find, which can complicate debugging and lead to unintentional reentrant calls. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/eventbus/EventBus.java:62]
- **ASCII Assumptions**: Using `Ascii` utilities with arbitrary Unicode text can be unsafe; they are
  intended for known ASCII or simple debugging text. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/base/Ascii.java:534]

## Freshness And Evidence
- **Stable State**: The library is a mature, open-source project with a long history of stability
  (Copyrights dating back to 2007). [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/base/FinalizableReferenceQueue.java:2]
- **Verification**: Re-verify `ImmutableCollection` and `Multimap` subtypes when updating, as these
  are common sources of bugs if `equals` semantics are misunderstood. [file:
  github:0xaeres/guava-fork/android/guava/src/com/google/common/collect/ImmutableCollection.java:50]