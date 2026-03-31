**Title:** Django

**Idea:** Django is a full-stack Python web framework that follows the "batteries included" philosophy — it ships with an ORM, admin interface, authentication, form handling, URL routing, and templating out of the box. It favours convention over configuration and enforces an MTV (Model-Template-View) pattern.

**Key characteristics:**
- **ORM:** Maps Python classes to database tables; supports PostgreSQL, MySQL, SQLite, Oracle. Complex queries written in Python, not SQL
- **Admin interface:** Auto-generated admin UI from model definitions — a huge productivity win for content management and internal tools
- **Authentication:** Built-in user model, sessions, permissions, and groups
- **Migrations:** Schema changes tracked as versioned migration files, applied and rolled back with `manage.py`
- **Templating:** Django Template Language (DTL) for server-side rendering; can be replaced with Jinja2
- **Security defaults:** CSRF protection, SQL injection prevention, XSS escaping, clickjacking protection — all on by default

**Trade-offs:**
- Rapid development for data-driven applications — the admin alone saves weeks on internal tools
- Monolithic by default — can feel heavy for lightweight APIs (Flask or FastAPI are better fits)
- ORM is powerful but can generate inefficient queries; `select_related` / `prefetch_related` required for N+1 prevention
- Django REST Framework (DRF) is the standard for building REST APIs in Django but adds significant boilerplate compared to FastAPI
- Synchronous by default; Django Channels extends it for async/WebSocket support but adds complexity

**When to use:**
- Content-heavy applications, e-commerce, CMS, and admin-heavy internal tools
- Projects where the built-in admin saves significant time
- Teams that want convention over configuration and a mature, well-documented ecosystem
- When you need the full stack: auth, ORM, admin, forms, and views in one framework

**Connections:**
- [[Python]]
- [[Flask]]
- [[FastAPI]]
- [[REST]]
- [[Role-Based Access Control (RBAC)]]

Up: [[Languages, libraries & frameworks]]

## Tags
#llf
