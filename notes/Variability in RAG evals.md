## 1. LLM Judge Non-determinism (primary cause)

The evaluation metrics (Faithfulness, Hallucination, etc.) themselves use an LLM (`us.amazon.nova-pro-v1:0`) to judge the results. Unless that model is called with `temperature=0`, it will produce slightly different verdicts each run. You can see this directly in the two runs:

- Run 1: Faithfulness = **0.67** (FAILED) — judge said AM attribution contradicts context
- Run 2: Faithfulness = **1.0** (PASSED) — same judge said the answer perfectly aligns

Same answer, same context, different verdict from the LLM judge.

## 2. Ambiguous Source Content

The knowledge base itself contains what appears to be conflicting information:

- One passage: _"AM schedules the logistics for a call..."_ → Sales/AM is responsible
- Another passage: implies CDM is responsible for scheduling

When the retriever returns different chunks in different runs, the judge model sees different "truths" and evaluates differently.

## 3. KB Pipeline Non-determinism

If your KB agent uses a non-zero temperature for generating the answer, the actual output can vary between runs — sometimes saying "AM is responsible," sometimes "CDM is responsible."

## 4. Retrieval Variability

Vector search with approximate nearest-neighbor algorithms can return slightly different ranked results across runs, changing which passages land in `retrieval_context`.

---

## How to reduce variability

|Fix|Where|
|---|---|
|Set `temperature=0` on the judge model|`DeepEvalBaseLLM` config|
|Set `temperature=0` on the KB answer model|Your pipeline config|
|Use `use_cache=True` in deepeval|`CacheConfig` — caches LLM judge calls|
|Fix the ambiguity in source docs|Knowledge base content|
|Add `expected_output` to pin ground truth|`TestCase` definition|

The most impactful fix is **deterministic temperatures on both the judge and the answer model**. The ambiguous source content is a deeper issue that will keep causing metric disagreement regardless of temperature.

Links:
- [[Evaluation loops]]
- [[Evaluator Paradox]]
- [[Self-Evaluation in RAG]]
- [[RAG Evaluation with DeepEval]]
- [[Contextual Relevancy — Analysis and Improvement]]

Up: [[AI Systems]]

## Tags
#ai