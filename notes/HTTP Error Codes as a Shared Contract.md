**Title:** HTTP Error Codes as a Shared Contract

**Idea:** HTTP status codes (1xx–5xx) are an internationally standardized signaling system between API producers and consumers. Every API integration must honor them rather than inventing proprietary error schemes, because consumers build their error-handling logic around these known codes.

**Why it matters:** Violating standard codes (e.g., returning 200 with an error in the body) breaks client error-handling logic and makes debugging exponentially harder across integrations.

**Trade-offs:** Standard codes are broad; a structured error body alongside the code is still needed to convey context-specific details.

**Connections:**

- [[Structured Error Response Design]]
- [[API Contract Design]]
- [[Consumer-Driven API Design]]

## Tags
#api