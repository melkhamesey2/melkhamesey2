# Real-Time Market Intelligence Platform

## Scope

A private, production-oriented engineering project for ingesting, reconciling, analyzing, and presenting live Egyptian Exchange market data. This public case study describes the architecture and verified development evidence without publishing proprietary source code, credentials, vendor internals, or trading logic.

## System architecture

```text
DFN Desktop JVM (32-bit)
-> Java instrumentation and capture callbacks
-> bounded quote coalescing / execution FIFO
-> authenticated framed TCP with signed UDP fallback
-> Go ingestion and canonical state engine
-> technical analysis and ranking services
-> WebSocket / SSE delta delivery
-> incremental browser rendering
-> asynchronous SQLite operational persistence
```

## Core engineering decisions

### Canonical state ownership

- Quote cumulative fields own official session volume and turnover.
- A complete-identity execution ledger owns trades, corrections, cancellations, and participant flows.
- One canonical state writer controls mutation.
- Persistence, network serialization, analytics, and logging remain outside the critical state lock.

### Event-driven delivery

- One bootstrap snapshot is followed by sequence-controlled deltas.
- WebSocket is primary; SSE is an event-driven fallback.
- Shared serialized deltas avoid per-client re-serialization.
- Slow clients are isolated and resynchronized.
- Browser rendering patches only dirty rows/cells on the next animation frame.

### Reliability and recovery

- bounded queues and replay protection
- full-identity deduplication
- source-date preservation across recovery
- explicit readiness and completeness gates
- transactional SQLite schema migration and integrity checks
- fail-closed release locks and artifact hashing
- current-session operational persistence rather than uncontrolled historical growth

### Security boundary

- HMAC-authenticated framed TCP collector
- signed UDP fallback with anti-replay controls
- loopback-only engine, collector, Order Book, admin, and MCP services
- invite-required viewer sessions
- Origin validation, secure cookies, rate limits, capacity limits, and audit logging

## Verified development evidence

A recovery and reconciliation run demonstrated:

- 279 stock rows
- 241,511 execution rows
- 954 participant-flow rows
- 0 invalid rows
- zero scoped sequence gaps
- zero out-of-order events
- zero queue drops
- exact sampled trade-count and volume parity
- source-date preservation across a later runtime session

One sampled instrument reconciled exactly at 4,479 trades and 1,458,342 volume. The system also retained signed participant liquidity and exposed the bounded rounding difference between ledger aggregation and row-level source totals.

These numbers represent verified development evidence, not a claim of final production acceptance. The project maintains explicit build, security, packaged-smoke, latency, and first-live-session gates before a production label can be granted.

## Performance design

The current architecture uses separate coalescing boundaries for local WebSocket, viewer delivery, and SSE fallback. Market publication is mutation-driven; no one-second polling ticker is used for live market updates. The critical path excludes database writes, full technical scans, full snapshots, and synchronous client I/O.

## What this project demonstrates

- Go backend and concurrent state design
- Java runtime instrumentation
- real-time protocols and streaming UI delivery
- data reconciliation and correction semantics
- WebSocket/SSE client synchronization
- SQLite operational persistence
- observability and release verification
- secure local ingestion and controlled external viewing
- production-readiness discipline with explicit rejection gates

## Public boundary

The source remains private because it integrates licensed market software and contains proprietary extraction, reconciliation, and trading-analysis logic. Public materials are restricted to sanitized architecture, engineering decisions, and reproducible evidence summaries.
