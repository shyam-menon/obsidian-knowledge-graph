**Title: Strict Service Contracts** 

**Idea:** The `.proto` file acts as a single source of truth. If the schema changes, the code generation tool ensures both sides are updated or handle versioning explicitly. 

**Why it matters:** Prevents "runtime surprises" where a field is renamed or missing, moving errors from production to compile-time. 

**Connections:**
- [[Type Safety]]    
- [[Schema Evolution]]