# Knowledge Graph Taxonomy

## Domain → Tag → MOC mapping

| Domain | Tag | MOC file |
|---|---|---|
| AI & Machine Learning | #ai | AI systems.md |
| Security & Auth | #security | Security & auth.md |
| APIs & Integration | #api | API Integration Patterns.md |
| Frontend | #frontend | Languages, libraries & frameworks.md |
| Observability | #observability | Non-Functional.md |

---

## Clusters (for sibling link expectations)

### RAG Core (#ai → AI systems.md)
- RAG architecture
- Chunking strategies
- Embedding models
- Vector search
- Standard RAG's One-Shot Problem
- Query Ambiguity in Search Systems
- Retrieval False Confidence
- Retrieval Routing Across Multiple Knowledge Sources
- Semantic Caching in RAG

### RAG Evaluation (#ai → AI systems.md)
- Evaluation loops
- Evaluator Paradox
- Self-Evaluation in RAG

### Agentic RAG (#ai → AI systems.md)
- Agentic RAG
- Agentic RAG Control Loop
- Agentic RAG Latency-Cost Trade-off
- When to Use Agentic RAG vs. Standard RAG
- Multi-Agent Orchestration in RAG

### Agent Systems (#ai → AI systems.md)
- Agents
- ReAct Framework
- Pipeline-to-Loop as a General AI Architecture Pattern

### Auth Fundamentals (#security → Security & auth.md)
- Authentication and Authorization are Independent Checks
- HTTPS secures the channel, not the caller
- API Keys Are Long Passwords
- API Keys — Simple Stateless Authentication

### Delegated Auth (#security → Security & auth.md)
- OAuth 2.0 — Delegated Authorization
- OpenID Connect — Identity on Top of OAuth
- JWT and OAuth 2.0 for Scoped Access

### Authorization Models (#security → Security & auth.md)
- Principle of Least Privilege
- Role-Based Access Control (RBAC)
- Attribute-Based Access Control (ABAC)
- Broken object level authorization (BOLA)

### Input & API Security (#security → Security & auth.md)
- API security 101
- Server-Side Input Validation Is the Only Security Guarantee
- Allowlisting vs. Blocklisting for Input Validation

### Runtime Security (#security → Security & auth.md)
- Rate Limiting Covers Both Attacks and Accidents
- Rate Limiting Algorithm Trade-offs
- Anomaly Detection from Traffic Baselines

### API Design (#api → API Integration Patterns.md)
- REST URL Design Conventions
- HTTP Method Semantics
- API Versioning Strategy
- API Granularity — The Medium-Grained Sweet Spot
- KISS Principle in API Design
- HTTP Error Codes as a Shared Contract
- Structured Error Response Design
- Strict Service Contracts

### API Patterns (#api → API Integration Patterns.md)
- Webhooks vs. Polling
- Pagination Strategies and Their Trade-offs
- Query Parameter Conventions
- Partial Response and Field Selection
- Bulk Data Transfer Pattern
- SDK Design Best Practices

### Protocols (#api → API Integration Patterns.md)
- gRPC
- Protocol Buffers (Protobuf)
- HTTP2 Multiplexing
- Bidirectional Streaming
- Language Agnosticism (Polyglot Support)

### React Ecosystem (#frontend → Languages, libraries & frameworks.md)
- React library
- React Component Model
- JSX (JavaScript XML)
- React 19 compiler
- Declarative UI

### Vite & Build Tools (#frontend → Languages, libraries & frameworks.md)
- Native ESM Serving (Vite)
- Vite Hot Module Replacement (HMR)
- Rolldown Engine
- React-Vite Plugin Integration

### Observability (#observability → Non-Functional.md)
- Monitoring and Logging for Retroactive Visibility
