**Title:** Flask

**Idea:** Flask is a lightweight Python microframework that provides just the essentials: URL routing, request/response handling, and templating. Everything else — ORM, auth, validation, admin — is opt-in via extensions. It gives you full control over the architecture with no imposed structure.

**Key characteristics:**
- **Minimalist core:** ~1000 lines of code in the core; starts with routing and WSGI handling only
- **WSGI-based:** Synchronous by default; runs on any WSGI server (Gunicorn, uWSGI)
- **Jinja2 templating:** Powerful, well-documented templating engine built in
- **Blueprints:** Module-level routing grouping for organising larger applications
- **Extensions ecosystem:** Flask-SQLAlchemy (ORM), Flask-Login (auth), Flask-Migrate (migrations), Flask-WTF (forms) — composable rather than bundled
- **No ORM, no admin, no structure enforced:** Full freedom to use SQLAlchemy directly, raw SQL, or any other data layer

**Trade-offs:**
- Maximum flexibility — the right tool when you want to compose exactly what you need
- Less opinionated than Django; architectural decisions are left to you, which can lead to inconsistency across large teams
- Extension ecosystem is fragmented — some popular extensions are poorly maintained
- Synchronous by default; Flask 2.0+ supports async views but is not designed around async from the ground up (FastAPI is better for async-first APIs)
- No built-in API features (serialisation, validation, docs) — FastAPI handles these better for pure API projects

**When to use:**
- Small to medium web applications and REST APIs
- Prototypes and internal tools where Django's full stack is overkill
- Projects requiring full control over the tech stack
- When you need a thin HTTP layer around existing Python logic

**Connections:**
- [[Python]]
- [[Django]]
- [[FastAPI]]
- [[REST]]
- [[API security 101]]

Up: [[Languages, libraries & frameworks]]

## Tags
#llf
