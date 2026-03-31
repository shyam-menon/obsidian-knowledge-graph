**Title:** FastAPI

**Idea:** FastAPI is a modern Python web framework for building APIs, built on top of Starlette (ASGI) and Pydantic. It is async-first, leverages Python type hints for automatic request validation and serialisation, and auto-generates OpenAPI/Swagger documentation from the code itself.

**Key characteristics:**
- **Async-first (ASGI):** Built on Starlette's async foundation; handles concurrent requests efficiently without threads
- **Type hint-driven:** Request bodies, query parameters, and path parameters declared as typed Python function arguments — Pydantic validates them automatically
- **Auto-generated docs:** OpenAPI (Swagger UI) and ReDoc documentation generated directly from the code with zero extra configuration
- **Pydantic models:** Request/response schemas defined as Pydantic classes — serialisation, deserialisation, and validation handled automatically
- **Dependency injection:** Built-in DI system for shared logic (database sessions, auth checks, config)
- **Performance:** One of the fastest Python frameworks — comparable to Node.js and Go for I/O-bound workloads due to async

**Trade-offs:**
- Best Python framework for pure API backends — minimal boilerplate, automatic docs, type safety
- No built-in ORM, admin, or templating — pairs with SQLAlchemy (sync or async) and Alembic for the data layer
- Async requires understanding of Python's `asyncio` model; mixing sync and async code incorrectly causes performance issues
- Younger than Django/Flask — ecosystem and community smaller, though growing rapidly
- Pydantic v2 (used in FastAPI 0.100+) has breaking changes from v1 — migration required for older codebases

**When to use:**
- REST and async API backends where performance and developer experience matter
- Microservices where auto-generated API docs and type safety reduce integration friction
- AI/ML model serving (common pattern: wrap a PyTorch/scikit-learn model in a FastAPI endpoint)
- Any project where the API schema should be the single source of truth for validation and documentation

**Connections:**
- [[Python]]
- [[Django]]
- [[Flask]]
- [[REST]]
- [[gRPC]]
- [[API security 101]]
- [[Strict Service Contracts]]
- [[Agentic RAG]]

Up: [[Languages, libraries & frameworks]]

## Tags
#llf
