
# 1. Core Trade-offs & Antipatterns

## Foundational Trade-offs
* Performance vs Scalability (Testing tools: JMeter, Locust, Gatling)
* Latency vs Throughput
* Availability vs Consistency (CAP Theorem)
* Availability in Numbers: 99.9% (three 9s) vs. 99.99% (four 9s)
* PACELC Theorem (Latency vs. Consistency during normal operation)

## Performance Antipatterns
* Noisy Neighbor (Shared resource monopolization)
* Retry Storm (Overwhelming a recovering service)
* Synchronous I/O & Chatty I/O (Too many small network calls)
* Extraneous Fetching (Over-fetching data)
* Monolithic Persistence & Busy Database

---

# 2. Databases & Data Management

## Data Models & Tech Stack
* Relational / OLTP: MySQL, PostgreSQL, Oracle, SQL Server, Google Cloud Spanner (NewSQL)
* Key-Value: Redis, Amazon DynamoDB, Riak, Memcached
* Document: MongoDB, Couchbase, Amazon DocumentDB
* Wide-Column: Apache Cassandra, ScyllaDB, Apache HBase
* Graph: Neo4j, Amazon Neptune, ArangoDB
* Time-Series: InfluxDB, Prometheus, TimescaleDB
* Vector: Pinecone, Milvus, Weaviate, Qdrant
* Data Warehouse / OLAP: Snowflake, Google BigQuery, Amazon Redshift
* Data Lake: Databricks, AWS Lake Formation, Hadoop (HDFS)

## Scaling & Architecture
* Sharding (Horizontal): Hash, Range, Directory-Based
* Routing: Consistent Hashing
* Federation (Functional partitioning)
* Denormalization & SQL Tuning

## Replication & Consistency
* Topologies: Single-Leader, Multi-Leader, Leaderless
* Fail-over: Active-Active vs. Active-Passive
* Consistency: Weak, Eventual, Strong (Linearizability)
* Quorum Consensus (W + R > N)

## Internals & Concurrency
* Indexing: B-Trees, LSM-Trees (WAL, SSTables), Inverted Indexes (Elasticsearch, Solr), Bloom Filters
* Concurrency: Pessimistic vs. Optimistic Locking, MVCC

---

# 3. Caching Strategies

## Topologies & Tech Stack
* Client / Browser Cache
* Edge / CDN Cache (Cloudflare, Fastly)
* Web Server Cache (Varnish, Squid)
* Application / Local Cache (Ehcache, Guava Cache, Caffeine)
* Distributed Cache (Redis, Memcached, Hazelcast)

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

## Load Balancers & Proxies
* Types: Layer 4 (TCP/UDP) vs. Layer 7 (HTTP/HTTPS)
* Reverse Proxies & LBs: Nginx, HAProxy, Envoy, Traefik, F5 BIG-IP
* Algorithms: Round Robin, Least Connections, IP Hash

## CDNs, Edge, & DNS
* CDNs: Cloudflare, Akamai, Fastly, Amazon CloudFront
* DNS Servers: Route 53, CoreDNS, BIND
* Models: Push CDN vs. Pull CDN
* Routing: Anycast IP, Geo-DNS routing

## Rate Limiting (Traffic Control)
* Algorithms: Token Bucket, Leaky Bucket, Fixed/Sliding Window
* Implementation: Redis (Lua scripts), API Gateways (Kong)

---

# 5. API & Communication Architecture

## API Paradigms
* REST (Stateless, HTTP methods, JSON/XML)
* GraphQL (Apollo, Relay - Solves over/under-fetching)
* RPC / gRPC (Protocol Buffers/Protobuf, HTTP/2, low latency)
* Real-time: Webhooks, WebSockets (Socket.io), SSE, Long Polling

## API-Led Connectivity (Integration Pattern)
* Experience Layer (BFF): Tailors data for Web/Mobile.
* Process Layer: Orchestration, routing, aggregation.
* System Layer: Wraps and abstracts core backend databases.

## Gateway Patterns & Tech
* API Gateways: Kong, Apigee, MuleSoft Anypoint, Tyk, AWS API Gateway
* Gateway Routing, Gateway Offloading, Gateway Aggregation

---

# 6. Microservices & Cloud Design Patterns

## Decomposition & Structure
* Strangler Fig (Monolith to Microservices)
* Domain-Driven Design (Bounded Contexts)
* Sidecar & Ambassador (Helper services)
* Service Mesh: Istio, Linkerd, Consul Connect
* Anti-Corruption Layer (Isolates new systems from legacy)

## Data & State
* CQRS (Command Query Responsibility Segregation)
* Event Sourcing (EventStoreDB, Apache Kafka)
* Saga Pattern (Choreography vs. Orchestration)
* Materialized View & Index Table

---

# 7. Asynchronous Messaging & Event Processing

## Message Brokers (Point-to-Point / Queues)
* Tools: RabbitMQ, ActiveMQ, Amazon SQS, MuleSoft Anypoint MQ, IBM MQ
* Use Case: Task distribution, decoupled workers, message deleted after processing.

## Event Streams (Pub/Sub / Append-Only Logs)
* Tools: Apache Kafka, Amazon SNS, Google Cloud Pub/Sub, Apache Pulsar
* Use Case: Broadcasting events, replayable logs, multiple independent consumer groups.

## Data Processing Engines
* Batch Processing: Hadoop MapReduce, AWS EMR
* Stream Processing: Apache Flink, Apache Spark Streaming, Kafka Streams

## Messaging Patterns
* Claim Check (Payload to DB/S3, reference ID to queue)
* Queue-based Load Leveling (Smoothing traffic spikes)
* Priority Queue & Competing Consumers
* Pipes and Filters
* Dead Letter Queues (DLQ) & Back Pressure

---

# 8. Distributed System Theory & Coordination

## Coordination Services
* Tools: Apache Zookeeper, etcd (used in Kubernetes), HashiCorp Consul
* Use Cases: Service Discovery, Distributed Locks, Configuration Management.
* Leader Election Algorithms: Paxos, Raft

## Clocks & Failures
* Time: Logical Clocks, Vector Clocks, Lamport Timestamps
* Failures: Split-Brain, Byzantine Fault Tolerance (BFT), Gossip Protocol

---

# 9. Resiliency, Security & Identity

## Resiliency Patterns
* Circuit Breaker & Bulkhead (Libraries: Resilience4j, Netflix Hystrix)
* Retry with Exponential Backoff & Jitter
* Compensating Transaction (Undoing failed Saga steps)

## Identity, Access & Secrets
* IAM & SSO: Okta, Auth0, Keycloak, Ping Identity, AWS Cognito
* Standards: OAuth 2.0, SAML, OIDC, JWT
* Secrets Management: HashiCorp Vault, AWS Secrets Manager

## Security Patterns & Edge Defense
* Edge: WAF (Web Application Firewall), Cloudflare DDoS Protection
* App Level: CORS, TLS/SSL termination
* Gatekeeper & Valet Key (Presigned URLs in AWS S3)

---

# 10. Observability & Monitoring

## Telemetry Pillars & Tech Stack
* Metrics (Time-series data): Prometheus, Datadog, New Relic, InfluxDB
* Logging (Event data): ELK Stack (Elasticsearch, Logstash, Kibana), Splunk, Fluentd, Grafana Loki
* Distributed Tracing (Request journey): Jaeger, Zipkin, OpenTelemetry
* Visualization & Alerting: Grafana, PagerDuty, Opsgenie

## Monitoring Types
* Health Endpoint Monitoring
* Availability, Performance, Security, & Usage Monitoring

---

# 11. Classic System Archetypes

* Global: Unique ID Generator (Twitter Snowflake, MongoDB ObjectIDs), URL Shortener
* Content/Social: News Feed (Fan-out), Web Crawler (Apache Nutch)
* Real-Time: Chat System (Erlang, WebSockets), Notification System
* Spatial: Proximity Service (Geohashes, Quadtrees, PostGIS), Ride-Sharing
* Search: Auto-complete / Typeahead (Trie data structures, Redis)

---

# 12. Cloud Infrastructure (AWS Mapping)

* Compute: EC2 (VMs), EKS (Kubernetes), ECS (Docker), Lambda (Serverless)
* Storage: S3 (Object), EBS (Block), EFS (File)
* Databases: RDS/Aurora (SQL), DynamoDB (NoSQL), Redshift (OLAP)
* Caching: ElastiCache (Redis/Memcached)
* Network & CDN: ALB/NLB (Load Balancing), CloudFront (CDN), Route 53 (DNS), VPC
* Async/Messaging: SQS (Queues), SNS (Pub/Sub), Kinesis (Streams), EventBridge (Event Bus)
