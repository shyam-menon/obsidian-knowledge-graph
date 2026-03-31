**Title:** Python

**Idea:** Python is a high-level, dynamically typed, interpreted language designed for readability and developer productivity. Its philosophy — "there should be one obvious way to do it" — favours explicitness and clean syntax over terseness. It is the dominant language for AI/ML, data science, scripting, and backend APIs.

**Key characteristics:**
- **Dynamic typing:** Variables are not declared with a type; types are inferred at runtime. Type hints (PEP 484) allow optional static checking via mypy or Pyright
- **Interpreted:** Executed directly by the CPython interpreter; no compile step in development
- **GIL (Global Interpreter Lock):** CPython allows only one thread to execute Python bytecode at a time — limits true parallelism for CPU-bound tasks. Multiprocessing or async I/O work around this
- **Extensive standard library:** "Batteries included" — file I/O, networking, JSON, CSV, HTTP, and more out of the box
- **Package ecosystem (PyPI):** The largest ecosystem of third-party packages of any language

**Where Python excels:**
- AI/ML and data science (NumPy, Pandas, PyTorch, scikit-learn)
- Backend APIs (Django, Flask, FastAPI)
- Scripting, automation, and tooling
- Rapid prototyping where development speed matters more than runtime speed

**Trade-offs:**
- Slow execution speed compared to compiled languages (Go, Rust, Java) — mitigated by calling into C extensions (NumPy, etc.)
- GIL limits CPU-bound concurrency in the standard interpreter
- Dynamic typing can hide bugs that static typing catches at compile time — type hints help but are not enforced at runtime
- High memory usage relative to compiled languages

**Connections:**
- [[Django]]
- [[Flask]]
- [[FastAPI]]

Up: [[Languages, libraries & frameworks]]

## Tags
#llf
