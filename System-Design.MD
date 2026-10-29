
# 1. Databases & Data Systems

## Data Models & Paradigms
* Relational (MySQL, PostgreSQL)
* Key-Value (Redis, DynamoDB)
* Document (MongoDB, CouchDB)
* Wide-Column (Cassandra, HBase)
* Graph (Neo4j)
* Time-Series (InfluxDB, Prometheus)
* Vector (Pinecone, Milvus)

## Scaling & Partitioning (Sharding)
* Vertical (Scale Up) vs. Horizontal (Scale Out)
* Hash-Based vs. Range-Based vs. Directory-Based
* Consistent Hashing

## Replication & Consistency
* Single-Leader vs. Multi-Leader vs. Leaderless
* Synchronous vs. Asynchronous
* Replication Lag
* Linearizability (Strong Consistency)
* Eventual Consistency

## Storage Internals & Indexing
* B-Trees / B+ Trees
* LSM-Trees & SSTables
* Write-Ahead Log (WAL)
* Inverted Indexes
* Bloom Filters

## Concurrency Control
* Optimistic vs. Pessimistic Locking
* MVCC (Multi-Version Concurrency Control)
* Isolation Levels (Read Uncommitted to Serializable)

---

# 2. Cache

## Layers
* Client / Edge (CDN) / API Gateway / Application / Database

## Topologies
* Local (In-Memory)
* Distributed (Redis, Memcached)

## Strategies & Eviction
* Write-Through, Write-Around, Write-Back
* LRU, LFU, FIFO

## Common Failures
* Cache Penetration
* Cache Stampede / Thundering Herd
* Cache Avalanche

---

# 3. CDN (Content Delivery Network)

## Core Concepts
* Push CDN vs. Pull CDN
* Edge Servers / Points of Presence (PoPs)
* Anycast IP Routing
* Geo-DNS

---

# 4. Load Balancers

## Types / OSI Layers
* Layer 4 (Transport: TCP/UDP)
* Layer 7 (Application: HTTP/HTTPS)

## Routing Algorithms
* Round Robin / Weighted Round Robin
* Least Connections / Least Response Time
* IP Hash (Consistent Hashing)

---

# 5. Rate Limiters

## Algorithms
* Token Bucket
* Leaky Bucket
* Fixed Window Counter
* Sliding Window Log
* Sliding Window Counter

---

# 6. API & Communication Protocols

## RESTful Architecture 
* 6 Constraints: Client-Server, Stateless, Cacheable, Uniform Interface, Layered System, Code on Demand
* Richardson Maturity Model (Levels 0-3)
* HATEOAS (Hypermedia as the Engine of Application State)
* Idempotency (Safe vs. Unsafe Methods)

## API-Led / Layered Connectivity (Integration Pattern)
* Experience Layer (BFF): Tailors data for specific client channels (Web, Mobile, IoT)
* Process Layer: Handles business logic, orchestration, and aggregation
* System Layer: Wraps and abstracts core backend systems of record

## Other API Paradigms
* GraphQL (Over-fetching / Under-fetching solutions)
* gRPC / RPC
* Webhooks (Reverse APIs)

## Network & Web Protocols
* TCP vs. UDP
* HTTP/1.1 vs. HTTP/2 (Multiplexing) vs. HTTP/3 (QUIC)
* WebSockets (Bi-directional)
* Server-Sent Events (SSE - Uni-directional)
* Long Polling

## Data Serialization / Encoding
* Text: JSON, XML, CSV
* Binary: Protocol Buffers (Protobuf), Apache Avro, Thrift

---

# 7. Microservices Architecture & Patterns

## Decomposition & Migration
* Strangler Fig Pattern (Monolith to Microservices)
* Domain-Driven Design (Bounded Contexts)

## Integration & Routing
* API Gateway Pattern
* Sidecar Pattern
* Service Mesh (e.g., Istio, Linkerd)
* Scatter-Gather (Parallel downstream calls aggregated into a single response)
* Message Filtering (Conditional routing based on payload content)

## Data & State Management
* CQRS (Command Query Responsibility Segregation)
* Event Sourcing
* Saga Pattern (Distributed Transactions)
  * Choreography (Event-based)
  * Orchestration (Central Controller)
* Two-Phase Commit (2PC)
* Watermarking (Tracking last-processed timestamps for delta syncs/state management)

## Resiliency Patterns
* Circuit Breaker
* Bulkhead Pattern
* Retry with Exponential Backoff
* Jitter

---

# 8. Asynchronous & Data Processing

## Message Brokers & Event Streams
* Point-to-Point (RabbitMQ, ActiveMQ)
* Pub/Sub (Apache Kafka, AWS SNS)
* Dead Letter Queues (DLQ) (Isolation for poisoned/failed messages)
* Delivery Semantics: At-Most-Once, At-Least-Once, Exactly-Once
* Idempotency Keys (Caching unique request IDs to prevent duplicate processing on retries)

## Big Data Processing
* Batch Processing (MapReduce, Hadoop)
* Stream Processing (Apache Flink, Spark Streaming)

---

# 9. Distributed System Theory & Coordination

## Coordination Services
* Service Discovery (Consul, Eureka, Zookeeper)
* Distributed Locks
* Leader Election (Paxos, Raft Algorithms)

## Clocks & Ordering
* Physical vs. Logical Clocks
* Vector Clocks
* Lamport Timestamps

## Failure Modes & Theorems
* CAP Theorem (CP vs. AP)
* PACELC Theorem
* Byzantine Fault Tolerance (BFT)
* Split-Brain Problem

---

# 10. Monitoring, Observability, and Proxies

## Observability Pillars
* Metrics (Prometheus, Grafana)
* Logging (ELK / EFK Stack, Splunk)
* Distributed Tracing (Jaeger, Zipkin, OpenTelemetry)

## Proxies
* Forward Proxy (Client masking/filtering)
* Reverse Proxy (Server masking, SSL termination, Load balancing - e.g., Nginx, HAProxy)

---

# 11. Security

## Identity & Access
* Authentication (AuthN) vs. Authorization (AuthZ)
* OAuth 2.0 / OpenID Connect (OIDC)
* SAML
* JWT (JSON Web Tokens)

## Data Protection
* Encryption In-Transit (TLS/SSL)
* Encryption At-Rest (AES)
* Web Application Firewall (WAF)
* CORS (Cross-Origin Resource Sharing)

---

# 12. Classic Interview System Archetypes

## Global Systems
* Unique ID Generator (Twitter Snowflake)
* URL Shortener (TinyURL - Base62 encoding)
* Web Crawler (BFS, Politeness policy, URL Frontier)

## Social & Content
* News Feed System (Fan-out on write vs. Fan-out on read)
* Chat System (WebSockets, Presence servers)
* Notification System (APNS, FCM, Rate limiting)

## Spatial & Location
* Proximity Service (Yelp/Tinder - Geohashes, Quadtrees)
* Ride-Sharing (Uber - Dispatch systems, location tracking)

## Infrastructure
* Distributed Cache (Consistent hashing)
* Rate Limiter (Rules caching, Redis Lua scripts)
* Distributed Message Queue

Adding AWS concepts is highly beneficial because interviews often expect you to map abstract architectural components to concrete, industry-standard cloud services. Here is the structured section to append to your cheat sheet.

# 13. Cloud Infrastructure (AWS Mapping)

## Compute & Execution
* Virtual Machines: Amazon EC2 (Elastic Compute Cloud)
* Container Orchestration: Amazon EKS (Managed Kubernetes), Amazon ECS
* Serverless Compute: AWS Lambda (Event-driven execution, cold starts)

## Storage
* Object / Blob Storage: Amazon S3 (Unstructured data, backups, static media)
* Block Storage: Amazon EBS (Elastic Block Store - attached directly to VMs)
* File Storage: Amazon EFS (Elastic File System - shared across multiple VMs)

## Databases & Caching
* Relational (SQL): Amazon RDS, Amazon Aurora (Highly scalable, cloud-native MySQL/PostgreSQL)
* Key-Value / Document (NoSQL): Amazon DynamoDB (Single-digit millisecond latency)
* Distributed Cache: Amazon ElastiCache (Managed Redis / Memcached)
* Graph: Amazon Neptune
* Data Warehouse (OLAP): Amazon Redshift

## Networking & Edge
* Load Balancing: Elastic Load Balancing (ALB for Layer 7 HTTP/HTTPS, NLB for Layer 4 TCP/UDP)
* Content Delivery Network (CDN): Amazon CloudFront
* Domain Name System (DNS): Amazon Route 53 (Supports Geo-DNS, Latency-based, and Weighted routing)
* API Management: Amazon API Gateway (Rate limiting, auth, throttling)
* Virtual Network: Amazon VPC (Virtual Private Cloud, Subnets, Peering, Transit Gateway)

## Integration, Messaging & Streaming
* Message Queues: Amazon SQS (Point-to-point, Standard vs. FIFO queues, DLQ integration)
* Pub/Sub: Amazon SNS (Fan-out, push-based notifications)
* Event Routing: Amazon EventBridge (Serverless event bus)
* Data Streams: Amazon Kinesis (Real-time stream processing, alternative to Kafka)

## Security & Observability
* Identity & Access: AWS IAM (Internal service/role access), Amazon Cognito (External user authentication)
* Encryption: AWS KMS (Key Management Service for at-rest encryption)
* Edge Protection: AWS WAF (Web Application Firewall), AWS Shield (DDoS protection)
* Monitoring & Logging: Amazon CloudWatch (Metrics, Alarms, Logs)
* Distributed Tracing: AWS X-Ray (Visualizing service-to-service requests)
