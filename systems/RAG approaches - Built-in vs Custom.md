# RAG Pipeline Analysis: MPS-AI-Extension KB Agent vs. aisa-api-platform & Model Cost-Benefit  

**Project:** MPS-AI-Extension  

**Date:** April 2026  

**Author:** Analysis generated for MPS AI team 

---
## Executive Summary
  

This report addresses two questions facing the MPS AI team:
  

1. What capabilities does the `aisa-api-platform` custom RAG API provide over the built-in Knowledge Base agent in MPS-AI-Extension?

2. Across the three available generation models on AWS Bedrock — **GPT-OSS-120B**, **Amazon Nova Pro**, and **Claude Haiku 4.5** — what is the cost-benefit tradeoff during the generation phase, and how can DeepEval be used to make an evidence-based model selection?

---

## Section 1: MPS-AI-Extension KB Agent vs. aisa-api-platform

Both systems use the same AWS Bedrock `RetrieveCommand` (retrieve-only) to pull passages from a Knowledge Base. The difference is entirely in what happens around that retrieval call. 

### 1.1 How the MPS-AI-Extension KB Agent Works
  

The built-in KB agent in MPS-AI-Extension follows this pipeline:
  

```

User query

    │

    ▼

KB Subagent (SubagentManager loop)

    │  ├─ System prompt: knowledge-base-agent.md

    │  └─ LLM: GatewayLLMProvider → gateway /v1/chat (Claude Sonnet by default)

    │

    ▼

KBToolProvider.executeQuery()

    │  └─ POST /v1/knowledge-base/retrieve  (gateway)

    │

    ▼

knowledge-base-provider.ts

    │  └─ BedrockAgentRuntimeClient.RetrieveCommand

    │     → Raw passages (text, score, source URI)

    │

    ▼

KB agent LLM synthesises answer from passages

    │

    ▼

Structured answer injected into main conversation

```

  
**What it provides:**

- Bedrock Knowledge Base retrieval via `RetrieveCommand`

- LLM synthesis of passages into a readable answer (via the KB agent's own LLM call)

- Scoped KB access — `@kb-name` mentions target a specific KB connection

- Source URIs and relevance scores returned alongside the answer

- Multi-KB querying (agent can query multiple KBs and synthesise across them)

- The generation model is whatever the gateway's `DEFAULT_MODEL` is (or the per-subagent override in settings)

  

**What it does not have:**

- Any pre-processing of the query before retrieval

- Input sanitisation or prompt injection protection

- PII masking on the generated response

- Conversation memory within a KB session (each subagent execution is independent)

- Multi-tenant configuration

- Custom source filtering for UI presentation

- Application-level observability beyond gateway request logs

  

### 1.2 How aisa-api-platform Works

  

The custom API wraps the same `RetrieveCommand` with a full pipeline:

  

```

User query

    │

    ▼

InputValidator

    │  ├─ Strip HTML

    │  ├─ Detect prompt injection

    │  └─ Enforce length limits

    │

    ▼

QueryNormalizer

    │  ├─ Detect acronyms (regex)

    │  └─ Expand via DynamoDB glossary table

    │     e.g. "MPS" → "MPS (Mission Planning System)"

    │

    ▼

BedrockAgentRuntimeClient.RetrieveCommand

    │  → Raw passages sorted by relevance score

    │

    ▼

Strands Agent (AgentWrapper.generate())

    │  ├─ SlidingWindowConversationManager (session memory)

    │  ├─ Per-tenant system prompt (loaded from Secrets Manager)

    │  └─ Per-tenant model (configurable via RoleConfig)

    │

    ▼

ResponseProcessor

    │  ├─ PIIMasker — strip emails, phone numbers

    │  ├─ SourceFilter — separate UI sources from LLM context

    │  └─ Response cleaning (SharePoint URLs, HTML entities, markdown)

    │

    ▼

Structured response: answer + sources + conversation_id

```

  

### 1.3 Capability Comparison

  

| Capability | MPS-AI-Extension KB Agent | aisa-api-platform |

|---|---|---|

| **Retrieval API** | `RetrieveCommand` | `RetrieveCommand` |

| **Generation** | KB subagent LLM (gateway model) | Strands agent (per-tenant model) |

| **Query pre-processing** | None — raw query sent to Bedrock | Acronym expansion via DynamoDB glossary |

| **Input sanitisation** | None | HTML stripping, prompt injection detection, length limits |

| **Conversation memory** | None — each call is stateless | `SlidingWindowConversationManager` per session |

| **Multi-tenant support** | Single configuration | Per-tenant prompts, models, KB IDs from Secrets Manager |

| **PII masking on output** | Not present | `PIIMasker` strips emails and phone numbers |

| **Source filtering** | Raw source URIs returned | Separate UI sources from full LLM context |

| **Response post-processing** | None | SharePoint URL cleanup, HTML entity decoding |

| **Observability** | Gateway request logs only | OpenTelemetry tracing, Prometheus metrics, structlog, token tracking per session |

| **Model routing** | Gateway `DEFAULT_MODEL` or per-subagent override | Factory-based: Bedrock or LLM Gateway, configurable per tenant |

| **Deployment scope** | Single product (MPS-AI-Extension) | Multi-tenant, multi-product |

  

### 1.4 Where Each Approach Is Appropriate

  

| Use Case | MPS-AI-Extension KB Agent | aisa-api-platform |

|---|---|---|

| Quick Q&A within MPS chat UI | ✅ Fits well | ❌ Overkill |

| Domain with heavy acronyms / jargon | ⚠️ Retrieval may miss terms | ✅ Glossary expansion improves precision |

| Follow-up questions in a KB session | ❌ No memory | ✅ Session history maintained |

| PII compliance required on responses | ❌ Not supported | ✅ Built-in masking |

| Multiple teams with different KBs | ⚠️ Manual config per deployment | ✅ Tenant-driven at runtime |

| Debugging retrieval quality | ⚠️ Passage scores available but no logging pipeline | ✅ Full telemetry stack |

| Adversarial input protection | ❌ None | ✅ Injection detection and sanitisation |

  

**Conclusion:** The MPS-AI-Extension KB agent is well-suited to the current MPS chat use case — simple, embedded, model-agnostic. The `aisa-api-platform` is the right choice when the deployment needs to serve multiple teams, handle domain-specific terminology, maintain conversation continuity, or meet compliance requirements around PII and input safety.

  

---

  

## Section 2: Model Cost-Benefit During the Generation Phase

  

### 2.1 Assumptions

  

- All three models are accessed via **AWS Bedrock on-demand** pricing (no cross-cloud API calls).

- Document ingestion costs (embedding model, S3 storage, OpenSearch indexing) are **identical** regardless of generation model choice and are excluded from this analysis.

- Retrieval costs (`RetrieveCommand` via Bedrock Agent Runtime) are also **identical** across all three models.

- Only the **generation phase** (LLM inference) varies by model.

  

### 2.2 AWS Bedrock On-Demand Pricing

  

| Model | Bedrock Model ID | Input (per 1M tokens) | Output (per 1M tokens) |

|---|---|---|---|

| **GPT-OSS-120B** | `openai.gpt-oss-120b-1:0` | $0.15 | $0.60 |

| **Amazon Nova Pro** | `amazon.nova-pro-v1:0` | $0.80 | $3.20 |

| **Claude Haiku 4.5** | `anthropic.claude-haiku-4-5-20251001` | $1.00 | $5.00 |

  

*Note: GPT-OSS-120B is OpenAI's open-weights model (Apache 2.0, MoE architecture, 117B total / 5.1B active parameters, 131K context window), available on Bedrock since late 2025.*

  

### 2.3 Cost Per 1,000 User Queries

  

**Assumptions:** Average query involves 2,000 input tokens (user question + 5 retrieved passages) and 500 output tokens (generated answer with citations).

  

| Model | Input Cost | Output Cost | Total / 1K Queries | Relative Cost |

|---|---|---|---|---|

| **GPT-OSS-120B** | $0.30 | $0.30 | **$0.60** | 1× |

| **Amazon Nova Pro** | $1.60 | $1.60 | **$3.20** | ~5.3× |

| **Claude Haiku 4.5** | $2.00 | $2.50 | **$4.50** | ~7.5× |

  

*At 10,000 queries/day: GPT-OSS-120B ≈ $6/day, Nova Pro ≈ $32/day, Haiku 4.5 ≈ $45/day.*

  

### 2.4 Model Characteristics Relevant to RAG Generation

  

| Characteristic | GPT-OSS-120B | Nova Pro | Claude Haiku 4.5 |

|---|---|---|---|

| **Architecture** | MoE (5.1B active params) | Dense (undisclosed) | Dense (undisclosed) |

| **Context window** | 131K tokens | 300K tokens | 200K tokens |

| **Instruction following** | Good | Good | Excellent |

| **Structured output** | Supported | Supported | Excellent |

| **Citation accuracy** | Moderate | Moderate | High |

| **Adjustable reasoning** | Yes (low/medium/high) | No | No |

| **Extended thinking** | No | No | No |

| **AWS-native integration** | Via Bedrock | Full native | Via Bedrock |

| **License** | Apache 2.0 (open weights) | Proprietary | Proprietary |

  

### 2.5 When Is a Higher-Cost Model Worth It?

  

#### GPT-OSS-120B — Best for High-Volume, Routine Queries

  

Choose GPT-OSS-120B when:

- Query volume is high (>5,000/day) and cost control is a priority.

- Queries are factual and straightforward: policy lookups, document summaries, FAQ-style questions.

- You want the ability to fine-tune on proprietary data (Apache 2.0 license allows this).

- Adjustable reasoning effort is useful — set `low` for simple lookups, `high` for complex synthesis.

  

Watch for: Lower faithfulness scores on complex multi-document synthesis. Validate with DeepEval (Section 3) before committing.

  

#### Amazon Nova Pro — Best AWS-Native Balance

  

Choose Nova Pro when:

- Data residency requirements mandate all computation within AWS (no third-party model provider endpoint).

- Queries require moderate reasoning (multi-step, cross-referencing multiple passages).

- You need Bedrock-native features: Knowledge Base direct integration, Bedrock Guardrails, CloudTrail audit logs.

- GPT-OSS-120B fails DeepEval quality thresholds on your specific query dataset.

  

At ~5× the cost of GPT-OSS-120B, Nova Pro is only justified if there is a measurable quality improvement on your workload.

  

#### Claude Haiku 4.5 — Best for Instruction-Sensitive, Accuracy-Critical Use Cases

  

Choose Claude Haiku 4.5 when:

- Generated answers must follow a precise format (structured citations, specific tone, regulatory language).

- Faithfulness and hallucination avoidance are critical — answers influence real decisions.

- Answer completeness matters: the model must synthesize across all retrieved passages, not just the first.

- You are already using Claude models elsewhere in the pipeline (consistency in behavior).

  

At ~7.5× the cost of GPT-OSS-120B and ~1.4× Nova Pro, the premium for Haiku 4.5 is justified when DeepEval faithfulness scores show a meaningful gap (>5 points) over the cheaper alternatives.

  

### 2.6 Batch Inference Option

  

For non-real-time workloads (nightly report generation, bulk document Q&A), all three models support Bedrock Batch Inference at **50% discount**:

  

| Model | Batch Input | Batch Output | Batch / 1K Queries |

|---|---|---|---|

| GPT-OSS-120B | $0.075 | $0.30 | **~$0.30** |

| Nova Pro | $0.40 | $1.60 | **~$1.60** |

| Claude Haiku 4.5 | $0.50 | $2.50 | **~$2.25** |

  

---

  

## Section 3: DeepEval Tests for Model Selection

  

### 3.1 Overview

  

DeepEval provides LLM-as-judge evaluation metrics that can be run against all three models on the same query dataset to produce objective, comparable scores. The goal is to calculate a **cost-per-quality-point** ratio that guides model selection.

  

### 3.2 Metric Categories

  

RAG evaluation metrics split into two groups with different purposes:

  

| Category | Evaluates | Model-Sensitive? |

|---|---|---|

| **Generator metrics** | Quality of the generated answer | ✅ YES — use for model selection |

| **Retriever metrics** | Quality of the retrieved passages | ❌ NO — use for KB configuration tuning |

  

### 3.3 Generator Metrics (Use for Model Selection)

  

These metrics are sensitive to the choice of generation model. Run all three against the same retrieved passages and the same queries.

  

---

  

#### `FaithfulnessMetric` ← Most Important

  

```python

from deepeval.metrics import FaithfulnessMetric

from deepeval.test_case import LLMTestCase

  

metric = FaithfulnessMetric(threshold=0.8, model="gpt-4o")

  

test_case = LLMTestCase(

    input="What is the MPS approval process?",

    actual_output=model_response,         # generated answer from the model under test

    retrieval_context=retrieved_passages  # list of passage strings from Bedrock KB

)

```

  

**What it tests:** Whether every factual claim in the generated answer is grounded in the retrieved passages. Detects when a model supplements context with memorized knowledge that may be incorrect.

  

**Why it differentiates models:** Cheaper models with weaker instruction following are more likely to hallucinate facts not present in the retrieved passages. Claude Haiku 4.5 typically outperforms on this metric due to stronger instruction adherence.

  

**Score interpretation:** 1.0 = all claims grounded in retrieved context. 0.7 = approximately 30% of claims are unsupported.

  

---

  

#### `AnswerRelevancyMetric`

  

```python

from deepeval.metrics import AnswerRelevancyMetric

  

metric = AnswerRelevancyMetric(threshold=0.8, model="gpt-4o")

```

  

**What it tests:** How directly and completely the generated answer addresses the user's question, regardless of factual grounding.

  

**Why it differentiates models:** Weaker models may produce answers that are technically faithful to the context but fail to address what the user actually asked. They may also pad answers with unnecessary hedging.

  

---

  

#### `ContextualRecallMetric`

  

```python

from deepeval.metrics import ContextualRecallMetric

  

metric = ContextualRecallMetric(threshold=0.8, model="gpt-4o")

```

  

**What it tests:** Whether the generated answer covers all relevant information present across the retrieved passages — not just the first or most prominent passage.

  

**Why it differentiates models:** A stronger model synthesizes information across multiple passages. A weaker model may anchor on the first passage and ignore the rest, producing incomplete answers.

  

**Requirement:** Needs a ground-truth `expected_output` (ideal answer) — build a golden dataset for this.

  

---

  

#### `HallucinationMetric`

  

```python

from deepeval.metrics import HallucinationMetric

  

metric = HallucinationMetric(threshold=0.5, model="gpt-4o")

```

  

**What it tests:** Whether the model generates facts that are not supported by the provided context (cross-check to FaithfulnessMetric from a different angle).

  

**Why it differentiates models:** Directly measures the risk of the model "inventing" information. High hallucination rates make a model unsuitable for compliance or decision-support use cases regardless of cost.

  

---

  

#### `GEval` — Custom Domain Criteria

  

```python

from deepeval.metrics import GEval

from deepeval.test_case import LLMTestCaseParams

  

# Example: citation quality for your specific use case

citation_quality = GEval(

    name="Citation Quality",

    criteria=(

        "The answer should reference specific document titles or section names "

        "from the retrieval context when making factual claims. "

        "Vague references like 'the document states' are insufficient."

    ),

    evaluation_params=[

        LLMTestCaseParams.ACTUAL_OUTPUT,

        LLMTestCaseParams.RETRIEVAL_CONTEXT

    ],

    threshold=0.7

)

```

  

Use `GEval` for any domain-specific requirement not covered by the standard metrics — answer tone, regulatory language, response length compliance, or HP-specific citation format.

  

### 3.4 Retriever Metrics (Not for Model Selection — Use for KB Tuning)

  

These metrics evaluate the Bedrock Knowledge Base retrieval configuration, not the generation model. Running them across models will produce identical results.

  

| Metric | What It Evaluates |

|---|---|

| `ContextualPrecisionMetric` | Whether relevant passages are ranked higher than irrelevant ones |

| `ContextualRelevancyMetric` | How relevant the overall retrieved context is to the query |

  

Use these separately to tune your KB chunk size, embedding model, and number of retrieved results (`maxResults`).

  

### 3.5 Recommended Testing Workflow

  

```

Step 1: Build a golden dataset

         ├── 50–100 representative queries covering your actual use cases

         ├── Each query paired with: expected_output (ideal answer)

         └── Each query paired with: retrieval_context (passages from Bedrock KB)

  

Step 2: Run each model against the full dataset

         ├── Keep all prompts, retrieved passages, and parameters identical

         └── Only the generation model changes between runs

  

Step 3: Score each model on all generator metrics

         ├── FaithfulnessMetric    (weight: HIGH)

         ├── AnswerRelevancyMetric (weight: MEDIUM)

         ├── ContextualRecallMetric(weight: MEDIUM)

         ├── HallucinationMetric   (weight: HIGH)

         └── GEval (custom)        (weight: domain-dependent)

  

Step 4: Calculate cost-per-quality-point

         Formula: (Cost per 1K queries) ÷ (Average FaithfulnessMetric score)

  

         GPT-OSS-120B:   $0.60 ÷ score_gpt

         Nova Pro:        $3.20 ÷ score_nova

         Claude Haiku 4.5: $4.50 ÷ score_haiku

  

Step 5: Apply the decision rule

         ├── If scores are within 5 points → use the cheaper model

         ├── If Haiku 4.5 score > Nova Pro by >5 points → Haiku 4.5 justified

         └── If GPT-OSS-120B score is acceptable → use GPT-OSS-120B

```

  

### 3.6 Decision Matrix

  

| Scenario | Recommended Model |

|---|---|

| GPT-OSS faithfulness ≥ 0.80 and scores within 5pts of others | **GPT-OSS-120B** |

| GPT-OSS faithfulness < 0.80 but Nova Pro ≥ 0.80 | **Nova Pro** |

| Nova Pro faithfulness < Haiku by >5pts, use case is high-stakes | **Claude Haiku 4.5** |

| Batch workload, latency not critical | **Any model at 50% batch discount** |

| Fine-tuning on proprietary data required | **GPT-OSS-120B** (Apache 2.0) |

  

---

  

## Appendix: Key File References

  

### MPS-AI-Extension

  

| File | Purpose |

|---|---|

| [packages/gateway/src/providers/knowledge-base-provider.ts](../packages/gateway/src/providers/knowledge-base-provider.ts) | AWS Bedrock `RetrieveCommand` implementation |

| [packages/gateway/src/config.ts](../packages/gateway/src/config.ts) | Default model configuration (`DEFAULT_MODEL`) |

| [src/lib/core/kb-subagent.ts](../src/lib/core/kb-subagent.ts) | KB subagent orchestration |

| [src/prompts/knowledge-base-agent.md](../src/prompts/knowledge-base-agent.md) | Generation system prompt |

  

### aisa-api-platform (Custom API)

  

| File | Purpose |

|---|---|

| `src/aisa_platform/ask_engine/service.py` | Main pipeline orchestrator (`AskEngineService`) |

| `src/aisa_platform/ask_engine/query_normalizer.py` | Acronym expansion via DynamoDB |

| `src/aisa_platform/ask_engine/guardrails/input_validator.py` | Prompt injection protection |

| `src/aisa_platform/ask_engine/generation/pii_masker.py` | PII masking on outputs |

| `src/aisa_platform/ask_engine/generation/response.py` | Source filtering & response cleanup |

| `src/aisa_platform/ask_engine/models/factory.py` | Model provider factory |

  

---

  

## References

  

- [GPT-OSS-120B on AWS Bedrock — model card](https://docs.aws.amazon.com/bedrock/latest/userguide/model-card-openai-gpt-oss-120b.html)

- [OpenAI open-weight models on AWS — announcement](https://aws.amazon.com/blogs/aws/openai-open-weight-models-now-available-on-aws/)

- [Amazon Nova Pro pricing](https://aws.amazon.com/nova/pricing/)

- [Claude Haiku 4.5 on Bedrock — release announcement](https://aws.amazon.com/about-aws/whats-new/2025/10/claude-4-5-haiku-anthropic-amazon-bedrock/)

- [Amazon Bedrock pricing](https://aws.amazon.com/bedrock/pricing/)

- [DeepEval RAG evaluation guide](https://deepeval.com/guides/guides-rag-evaluation)

- [DeepEval RAG metrics overview](https://www.confident-ai.com/blog/rag-evaluation-metrics-answer-relevancy-faithfulness-and-more)

## Connections
- [[AIaaS Platform]]
- [[RAG architecture]]
- [[Agentic RAG]]
- [[Evaluation loops]]
- [[RAG Evaluation with DeepEval]]

Up: [[AIaaS Platform]]

## Tags
#systems