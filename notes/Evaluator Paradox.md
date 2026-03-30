**Title:** Evaluator Paradox

**Idea:** The self-evaluation step in Agentic RAG uses an LLM to judge the quality of retrieved content. This means the system's ability to self-correct depends entirely on the LLM's ability to reason about relevance — which may itself be flawed, inconsistent, or overconfident.

**Why it matters:** You cannot assume evaluation is reliable just because it exists. A weak evaluator can do more harm than no evaluator — rejecting useful results and triggering loops that end up worse than the original one-shot answer. This is a key risk to quantify before deploying agentic systems.

**Connections:**

- [[Self-Evaluation in RAG]]
- [[Retrieval False Confidence]]
- [[Agentic RAG Control Loop]]

## Tags
#ai