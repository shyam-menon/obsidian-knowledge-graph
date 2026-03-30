**Title:** API Granularity — The Medium-Grained Sweet Spot

**Idea:** Fine-grained APIs expose too much internal complexity (e.g., `/animals/mammals/omnivores/cats`), forcing clients to make many calls. Coarse-grained APIs offer no useful structure. Medium-grained APIs balance discoverability and usability — typically 2 levels of path nesting, and response objects with around 5 core fields.

**Why it matters:** Granularity directly determines how many round trips an integration requires and how much coupling exists between the API and its clients. Medium granularity optimizes for both.

**Trade-offs:** Medium-grained design requires more upfront thought about client use cases; it cannot simply mirror an internal data model.

**Connections:**

- [[KISS Principle in API Design]]
- [[Consumer-Driven API Design]]
- [[REST URL Design Conventions]]