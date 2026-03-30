**Title:** Bulk Data Transfer Pattern

**Idea:** When large volumes of data need to move between systems, individual API calls become impractical. Bulk jobs submit a request once, and the server processes it asynchronously in batches, reporting status back. This avoids rate-limit exhaustion and connection overhead from thousands of individual requests.

**Why it matters:** Essential for data migrations, ETL pipelines, and sync operations. Using bulk correctly is the difference between a stable integration and one that hammers an API into rate limiting.

**Trade-offs:** Asynchronous nature means the client needs to poll for job status or receive a webhook callback — adding integration complexity.

**Connections:**

- [[Webhooks vs. Polling]]
- [[Pagination Strategies and Their Trade-offs]]
- [[SDK Design Best Practices]]

## Tags
#api