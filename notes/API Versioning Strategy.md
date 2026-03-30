**Title:** API Versioning Strategy

**Idea:** Embedding the version in the URL path (e.g., `/v1/`, `/v2/`) allows multiple versions to coexist, enabling consumers to migrate at their own pace. Backward compatibility must be maintained for existing versions until deprecation notices expire.

**Why it matters:** APIs are shared contracts. Breaking changes without versioning force all consumers to update simultaneously, which is often operationally impossible in distributed systems.

**Trade-offs:** URL versioning is the simplest approach but creates parallel maintenance burden. Header-based versioning is cleaner but less visible and harder to cache.

**Connections:**

- [[REST URL Design Conventions]]
- [[API Contract Design]]
- [[Backward Compatibility]]