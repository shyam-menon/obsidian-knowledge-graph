## What is Contextual Relevancy?

Contextual Relevancy measures how relevant the retrieved passages are to the question asked. DeepEval scores it as the fraction of statements across all retrieved passages that are actually relevant to the input query. A score of 1.0 means every retrieved statement is on-topic; a score of 0.35 means most of the retrieved content is noise.

**Threshold used in tests:** 0.7

---

## Why the Score Was Low (0.35 before fixes)

The AWS Bedrock Knowledge Base retrieves passages by vector similarity — how close the question's embedding is to each passage's embedding. For the question _"Who is responsible for scheduling the welcome call during onboarding?"_, the word **"onboarding"** caused the vector search to pull in passages from the **MPS SLA Tool Account Onboarding** document, which is about a completely different process (SLA data entry and validation). Those passages dominated the context window, making most retrieved statements irrelevant to the actual question.

---

## Options Considered

### Option 1 — Score-based filtering in the test pipeline (chosen)

**What it does:** Each passage returned by AWS Bedrock includes a relevance score (0–1). Passages scoring below a minimum threshold are dropped before being passed to the LLM and DeepEval.

**Where it lives:** `tests/helpers/pipeline.py` — `MIN_PASSAGE_SCORE = 0.4`

**Result:** Score improved from 0.35 → 0.64

**Trade-offs:**

- Simple, zero infrastructure changes
- Threshold must be tuned per knowledge base — too high risks dropping valid passages (hurts recall), too low lets noise through
- Only filters at the test layer; the gateway still returns all passages to other callers

---

### Option 2 — AWS Bedrock Reranking

**What it does:** After the initial vector search, a dedicated reranking ML model (e.g. `amazon.rerank-v1:0`) rescores each candidate passage by true semantic relevance to the query. A larger initial pool (e.g. 10 passages) is retrieved, reranked, then trimmed to the top-N.

**Where it would live:** `packages/gateway/src/providers/knowledge-base-provider.ts` — add `rerankingConfiguration` to `RetrieveCommandInput`

**Trade-offs:**

- Most powerful option — catches cases where a passage has a high vector score but low true relevance
- Adds latency (~200–500 ms) and per-query cost
- Requires the rerank model to be enabled in the AWS Bedrock account

---

### Option 3 — Hybrid search (semantic + keyword)

**What it does:** Combines dense vector search with BM25 keyword matching. Specific terms like "welcome call" or "Account Manager" get boosted by the keyword component.

**Where it would live:** `packages/gateway/src/providers/knowledge-base-provider.ts` — add `overrideSearchType: "HYBRID"` to `vectorSearchConfiguration`

**Trade-offs:**

- Free and low-effort to add
- Less powerful than reranking for ambiguous queries
- Helps most when the question contains distinctive keywords that appear verbatim in the right document

---

## Current State

|Approach|Applied|Score impact|
|---|---|---|
|Score-based filtering (`MIN_PASSAGE_SCORE = 0.4`)|Yes|0.35 → 0.64|
|AWS Bedrock Reranking|No|—|
|Hybrid search|No|—|

The score (0.64) is still below the passing threshold (0.70). The remaining gap is because one passage about the SLA Tool onboarding process still passes the score filter — it scores above 0.4 in vector similarity due to the shared word "onboarding", but is irrelevant to the welcome call question.

---

## Recommended Next Steps

1. **Add AWS Bedrock Reranking (Option 2)** — This is the most effective fix for the remaining gap. By retrieving 10 candidates and letting a rerank model select the best 5, the SLA onboarding document would receive a much lower rerank score and be excluded. Changes needed:
    
    - Add `rerankingConfiguration` to `RetrieveCommandInput` in [knowledge-base-provider.ts](https://file+.vscode-resource.vscode-cdn.net/c%3A/Code/Work/mps-ai-extension/packages/gateway/src/providers/knowledge-base-provider.ts)
    - Expose `numberOfRerankedResults` as a request parameter (similar to existing `maxResults`)
2. **Enable hybrid search (Option 3)** — Low effort, can be added alongside reranking as a complementary improvement.
    
3. **Tune `MIN_PASSAGE_SCORE`** — Run the test suite across more questions and plot score distributions to find the threshold that best separates relevant from irrelevant passages for this knowledge base.