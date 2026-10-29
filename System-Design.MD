# 1. Core Trade-offs & Antipatterns

## Foundational Trade-offs
* Performance vs Scalability
* Latency vs Throughput
* Availability vs Consistency (CAP Theorem)
* Availability Availability in Numbers: 99.9% (three 9s) vs. 99.99% (four 9s)
* PACELC Theorem (Latency vs. Consistency during normal operation)

## Performance Antipatterns
* Noisy Neighbor (Shared resource monopolization)
* Retry Storm (Overwhelming a recovering service)
* Synchronous I/O & Chatty I/O (Too many small network calls)
* Extraneous Fetching (Over-fetching data)
* Monolithic Persistence & Busy Database

---

# 2. Databases & Data Management

## Data Models
* Relational (MySQL, PostgreSQL)
* NoSQL: Key-Value (Redis), Document (MongoDB), Wide-Column (Cassandra), Graph (Neo4j)
* Specialized: Time-Series (InfluxDB), Vector (Pinecone)

## Scaling & Architecture
* Sharding (Horizontal): Hash, Range, Directory-Based
* Routing: Consistent Hashing (Minimizes data movement)
* Federation (Functional partitioning)
* Denormalization & SQL Tuning (Read optimization)

## Replication & Consistency
* Topologies: Single-Leader (Master-Slave), Multi-Leader (Master-Master), Leaderless
* Fail-over: Active-Active vs. Active-Passive
* Consistency: Weak, Eventual, Strong (Linearizability)
* Quorum Consensus (W + R > N)

## Internals & Concurrency
* Indexing: B-Trees, LSM-Trees (WAL, SSTables), Inverted Indexes, Bloom Filters
* Concurrency: Pessimistic vs. Optimistic Locking, MVCC

---

# 3. Caching Strategies

## Topologies & Layers
* Layers: Client, CDN, Web Server, Application, Database
* Setup: Local (In-Memory) vs. Distributed (Redis)

## Update & Eviction Policies
* Writing: Write-Through, Write-Around, Write-Back
* Reading/Updating: Cache Aside, Refresh Ahead
* Eviction: LRU, LFU, TTL Expiration

## Common Failures
* Cache Penetration (Mitigation: Bloom Filters)
* Cache Stampede / Thundering Herd (Mitigation: Distributed Locks, Jitter)
* Cache Avalanche (Mitigation: Randomized TTLs)

---

# 4. Networking, Load Balancing & Content Delivery

## Load Balancers & Routing
* Types: Layer 4 (TCP/UDP) vs. Layer 7 (HTTP/HTTPS)
* Algorithms: Round Robin, Least Connections, IP Hash
* Network: TCP vs. UDP, Domain Name System (DNS)

## CDNs & Edge
* Models: Push CDN vs. Pull CDN
* Routing: Anycast IP, Geo-DNS routing

## Rate Limiting (Traffic Control)
* Algorithms: Token Bucket, Leaky Bucket, Fixed/Sliding Window
* Throttling & Geodes (Geographical distribution)

---

# 5. API & Communication Architecture

## API Paradigms
* REST (Stateless, HTTP methods, HATEOAS)
* GraphQL (Solves over/under-fetching)
* RPC / gRPC (Binary, fast, strict contracts)
* Webhooks, WebSockets, SSE, Long Polling

## API-Led Connectivity (Integration Pattern)
* Experience Layer (BFF): Tailors data for specific client channels.
* Process Layer: Orchestration, routing, and aggregation.
* System Layer: Wraps and abstracts core backend databases.

## Gateway Patterns
* API Gateway (Centralized auth, rate limiting)
* Gateway Routing, Gateway Offloading, Gateway Aggregation

---

# 6. Microservices & Cloud Design Patterns

## Decomposition & Structure
* Strangler Fig (Monolith to Microservices)
* Domain-Driven Design (Bounded Contexts)
* Sidecar & Ambassador (Helper services for network/logging)
* Anti-Corruption Layer (Isolates new systems from legacy)

## Data & State
* CQRS & Event Sourcing
* Saga Pattern (Choreography vs. Orchestration)
* Materialized View & Index Table

---

# 7. Asynchronous Messaging & Event Processing

## Event & Message Brokers
* Paradigms: Message Queues (Point-to-Point) vs. Event-Driven Pub/Sub
* Triggers: Event-Driven vs. Schedule Driven Background Jobs
* Delivery: At-Most-Once, At-Least-Once, Exactly-Once (Idempotency)

## Messaging Patterns
* Claim Check (Payload to DB, reference ID to queue)
* Queue-based Load Leveling (Smoothing traffic spikes)
* Priority Queue & Competing Consumers
* Pipes and Filters (Breaking down complex processing)
* Dead Letter Queues (DLQ) & Back Pressure

---

# 8. Distributed System Theory & Coordination

## Coordination
* Service Discovery & Distributed Locks
* Leader Election (Paxos, Raft)

## Clocks & Failures
* Time: Logical Clocks, Vector Clocks, Lamport Timestamps
* Failures: Split-Brain, Byzantine Fault Tolerance (BFT)

---

# 9. Resiliency, Security & Identity

## Resiliency Patterns
* Circuit Breaker & Bulkhead
* Retry with Exponential Backoff & Jitter
* Compensating Transaction (Undoing failed Saga steps)

## Identity & Access
* AuthN (Identity) vs. AuthZ (Permissions)
* Standards: OAuth 2.0, SAML, JWT
* Federated Identity

## Security Patterns & Edge Defense
* Gatekeeper (Validates/sanitizes requests) & Valet Key (Limited resource token)
* CORS, TLS/SSL, WAF (Web Application Firewall)

---

# 10. Observability & Monitoring

## Monitoring Types
* Health Endpoint Monitoring
* Availability, Performance, Security, & Usage Monitoring

## Telemetry Pillars
* Metrics (Counters/Gauges), Logging (Events), Distributed Tracing
* Tools: Instrumentation, Visualization, & Alerts

---

# 11. Classic System Archetypes

* Global: Unique ID Generator (Snowflake), URL Shortener
* Content/Social: News Feed (Fan-out), Web Crawler
* Real-Time: Chat System, Notification System
* Spatial: Proximity Service (Geohashes/Quadtrees), Ride-Sharing

---

# 12. Cloud Infrastructure (AWS Mapping)

* Compute: EC2 (VMs), EKS/ECS (Containers), Lambda (Serverless)
* Storage: S3 (Object), EBS (Block), EFS (File)
* Databases: RDS/Aurora (SQL), DynamoDB (NoSQL), Redshift (OLAP)
* Caching: ElastiCache (Redis/Memcached)
* Network & CDN: ALB/NLB (Load Balancing), CloudFront (CDN), Route 53 (DNS)
* Async/Messaging: SQS (Queues), SNS (Pub/Sub), Kinesis (Streams)
