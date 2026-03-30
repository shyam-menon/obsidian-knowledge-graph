**Title:** Self-Evaluation in RAG

**Idea:** After retrieval, an agentic system uses an LLM to assess whether the retrieved content is relevant, complete, and current — before passing it to the generator. If the evaluation fails, the system retries with a different query or source.

**Why it matters:** This directly addresses the false confidence problem in standard RAG: the system stops trusting similarity scores alone and introduces a semantic quality check. It transforms retrieval from "find the closest match" to "find something actually useful."

**Trade-offs:** The evaluator is itself an LLM — subject to its own reasoning limitations. A poor evaluator can reject good results, trigger unnecessary retries, or accept bad content. This is the "evaluator paradox."

**Connections:**

- [[Agentic RAG Control Loop]]
- [[Retrieval False Confidence]]
- [[Evaluator Paradox]]