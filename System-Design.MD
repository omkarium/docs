# 1. Databases & Data Systems

## Data Models & Paradigms
* Relational (Structured, ACID, strict schema)
* Key-Value (O(1) access, simple caching/sessions)
* Document (Semi-structured, aggregate-oriented, flexible schema)
* Wide-Column (High write throughput, column-families, time-series/IoT)
* Graph (Nodes, edges, properties, optimized for deep joins)
* Vector (Embeddings, semantic similarity search)

## Scaling & Partitioning (Sharding)
* Partitioning Strategies
  * Hash-Based (Uniform distribution, hard to range-query)
  * Range-Based (Good for range queries, risk of hotspots)
  * Directory-Based (Lookup table, decoupling, extra hop)
* Sharding Challenges
  * Celebrity/Hotspot Problem (Uneven traffic)
  * Resharding/Rebalancing (Moving data without downtime)
  * Cross-Shard Joins (Requires application-level joins or denormalization)
* Consistent Hashing (Minimizes data movement to 1/N during node changes)

## Replication & Consistency
* Replication Topologies
  * Single-Leader (Read scalability, SPOF on write)
  * Multi-Leader (Geographic distribution, conflict resolution required)
  * Leaderless (High availability, Dynamo-style, uses Quorums)
* Quorum Consensus (W + R > N for strong consistency)
* Conflict Resolution (Last Write Wins/LWW, Version Vectors)
* Consistency Models
  * Linearizability (Strong, reads reflect latest write)
  * Causal Consistency (Preserves ordering of related events)
  * Eventual Consistency (High availability, eventual convergence)

## Storage Internals & Indexing
* B-Trees / B+ Trees
  * Leaf nodes contain data/pointers, optimized for read/range queries
* LSM-Trees (Log-Structured Merge-Trees)
  * MemTable (In-memory tree) -> WAL -> SSTable (Immutable disk segments) -> Compaction
* Inverted Indexes (Tokenization, mapping words to document IDs)

## Concurrency Control
* Locks: Shared (Read) vs. Exclusive (Write)
* Pessimistic (Lock upfront, high contention) vs. Optimistic (Check on commit, rollback if changed)
* MVCC (Snapshots based on transaction IDs, writers don't block readers)

---

# 2. Cache

## Topologies & Internals
* Local/In-Memory (Fastest, stateful server issues)
* Distributed (Scalable, single source of truth for cached data)
* LRU Implementation (Hash Map + Doubly Linked List for O(1) eviction/updates)

## Strategies & Eviction
* Write-Through (Safe, higher write latency)
* Write-Around (Reduces cache churn for rarely read data)
* Write-Back (Async disk writes, risks data loss on crash)

## Common Failures & Mitigations
* Cache Penetration (Querying non-existent data -> Mitigation: Bloom Filters)
* Cache Stampede (Key expires, massive DB hit -> Mitigation: Mutex/Distributed Locks, Probabilistic early expiration)
* Cache Avalanche (Multiple keys expire at once -> Mitigation: TTL Jitter/Randomization)

---

# 3. CDN (Content Delivery Network)

## Core Concepts
* Push CDN (Content uploaded proactively, good for small/static sites)
* Pull CDN (CDN fetches from origin on cache miss, good for heavy traffic)
* Cache Invalidation (Time-to-Live/TTL, Purge APIs, Versioning/Cache-busting via URLs)

---

# 4. Load Balancers

## Types & Mechanics
* Layer 4 (Transport: TCP/UDP, fast, unaware of content, NAT-based)
* Layer 7 (Application: HTTP/HTTPS, inspects headers/cookies, CPU-heavy)
* Health Checks (Active/Probing vs. Passive/Observing traffic)

---

# 5. Rate Limiters

## Algorithms & Trade-offs
* Token Bucket (Memory efficient, allows sudden bursts)
* Leaky Bucket (Smooths out traffic to a constant rate, queues requests)
* Fixed Window Counter (Simple, suffers from edge-of-window bursts)
* Sliding Window Log (Exact but memory-heavy, stores timestamps)
* Sliding Window Counter (Hybrid, memory efficient, probabilistic smoothing)

## Distributed Challenges
* Race Conditions (Mitigation: Redis Lua Scripts, Sorted Sets)
* Synchronization (Mitigation: Centralized datastore vs. Gossip protocol)

---

# 6. API & Communication Protocols

## RESTful Architecture
* Richardson Maturity Model
  * Level 0: One URI, One Method (RPC via HTTP)
  * Level 1: Distinct URIs for Resources
  * Level 2: Standard HTTP Methods (GET, POST, PUT, DELETE)
  * Level 3: HATEOAS (Discoverability via links)
* Idempotency (Crucial for retries, safe vs. unsafe methods)

## API Paradigms & Data
* GraphQL (Solves N+1 problem and Over/Under-fetching, requires complex backend resolvers)
* gRPC (Binary, HTTP/2 multiplexed, strictly typed via Protobuf, low latency)
* Pagination (Offset: slow for deep pages vs. Cursor: fast, requires sequential ID)

## Real-Time & Streaming
* WebSockets (Stateful, persistent bidirectional, requires heartbeat/keep-alive)
* SSE (Server-to-Client only, standard HTTP)
* Long Polling (Client holds request open until server has data, fallback mechanism)

---

# 7. Microservices Architecture & Patterns

## Decomposition & Routing
* Domain-Driven Design (Bounded Contexts define service boundaries)
* API Gateway (Auth, rate limiting, protocol translation, single entry point)
* BFF / Backend for Frontend (Tailored APIs for Web vs. Mobile)

## Data & State Management
* CQRS (Separating Write/Command models from Read/Query models, async sync)
* Event Sourcing (Storing state as a sequence of immutable events)
* Saga Pattern (Distributed Transactions without 2PC)
  * Choreography (Services publish/subscribe to events autonomously)
  * Orchestration (Central coordinator tells services what to do)
  * Compensating Transactions (Undoing a step if a subsequent step fails)

## Resiliency Patterns
* Circuit Breaker (States: Closed [Traffic flows] -> Open [Failing, traffic blocked] -> Half-Open [Testing recovery])
* Retry with Exponential Backoff & Jitter (Prevents thundering herds during recovery)
* Bulkhead Pattern (Isolating resources/thread pools to contain failures)

---

# 8. Asynchronous & Data Processing

## Message Brokers & Event Streams
* Queues vs. Streams
  * Queues (Point-to-point, message deleted after ack, load balancing workers)
  * Streams (Append-only log, multiple consumer groups can read same data, replayable)
* Stream Partitioning (Ordering guaranteed only within a partition/shard)
* Consumer Offsets (Tracking which messages have been read)
* Delivery Semantics (At-Most-Once, At-Least-Once, Exactly-Once via Idempotency)

---

# 9. Distributed System Theory & Coordination

## Clocks & Ordering
* Clock Drift (Physical NTP clocks are never perfectly synced)
* Logical Clocks (Lamport Timestamps: counters to track causal order)
* Vector Clocks (Detecting concurrent updates/conflicts)

## Failure & Coordination
* Split-Brain Problem (Network partition causes nodes to elect multiple leaders)
* Gossip Protocol (Epidemic state dissemination, nodes share state with random peers)
* Leader Election (Requires consensus, e.g., Raft: Leader, Follower, Candidate states)

---

# 10. Monitoring, Observability, and Proxies

## Observability Pillars
* Metrics (Aggregated data over time, alerting triggers)
* Logging (Discrete events, requires structured JSON for indexing)
* Distributed Tracing (Correlation IDs passed through headers across microservices)

---

# 11. Security

## Identity & Access
* Authentication (Who you are) vs. Authorization (What you can do)
* OAuth 2.0 Grant Types
  * Authorization Code (For end-users/web apps)
  * Client Credentials (Machine-to-Machine, e.g., MuleSoft backend integrations)
* JWT Structure (Header, Payload, Signature - stateless, hard to revoke without blocklists)

## Security Mechanisms
* CORS (Preflight OPTIONS request for cross-domain browser security)
* TLS/SSL Handshake (Asymmetric encryption for key exchange -> Symmetric for data payload)

---

# 12. Classic Interview System Archetypes (Core Challenges)

## Global Systems
* Unique ID Generator (Sorting by time, avoiding collisions, clock rollback issues)
* URL Shortener (Base62 encoding logic, collision handling, DB read/write ratios)
* Web Crawler (URL Frontier prioritizing, cycle detection via Hash Sets, Politeness limits)

## Social & Content
* News Feed (Fan-out on Write [Push, fast read, heavy write] vs. Fan-out on Read [Pull, slow read, saves compute for inactive users])
* Chat System (Message ordering, Presence indicators via heartbeat, WebSocket connection management)

## Spatial & Location
* Proximity Service (Spatial indexing: Geohashes [string prefixes], Quadtrees [recursive grids] to avoid full DB scans)
