
# Quantitative Evaluation of Enterprise-Grade Retrieval-Augmented Generation Systems using DeepEval and AWS Knowledge Bases with OpenSearch

The contemporary enterprise landscape is characterized by a reliance on vast, unstructured document repositories, where the ability to extract actionable intelligence determines the efficiency of automated support systems. The emergence of Retrieval-Augmented Generation (RAG) has transformed Large Language Models (LLMs) from static repositories of general knowledge into dynamic engines capable of grounding their outputs in proprietary, domain-specific data.
Within the AWS ecosystem, Amazon Bedrock Knowledge Bases serves as a managed orchestration layer that handles the complexities of document ingestion, chunking, and embedding, utilizing Amazon OpenSearch Service as a high-performance vector database.
However, the deployment of such an architecture is merely the first phase of the development lifecycle; ensuring the reliability, accuracy, and safety of the generated responses necessitates a rigorous evaluation framework. 
DeepEval provides this necessary infrastructure, offering a suite of research-backed metrics designed to quantify the performance of both the retrieval and generation components of the RAG pipeline.

## The Architecture of Managed Retrieval in Enterprise Environments

The fundamental challenge in enterprise RAG systems is the "semantic gap" between raw corporate documents and the high-dimensional vector space required for modern search. AWS Knowledge Bases for Amazon Bedrock addresses this by providing a fully managed workflow that automates the ingestion of documents from Amazon S3 into supported vector stores like Amazon OpenSearch. This architecture allows organizations to provide foundation models with up-to-date information without the prohibitive cost and complexity of model fine-tuning. The orchestration engine converts text into mathematical embeddings using models such as Amazon Titan Text Embeddings v2, which are then stored and indexed in OpenSearch.

### OpenSearch as a Foundation for Semantic and Hybrid Search

The selection of a vector database is a critical design decision that dictates the scalability and precision of the retrieval process. Amazon OpenSearch Service provides two primary deployment options: managed clusters and serverless collections.
Managed clusters are suitable for organizations requiring granular control over instance types, storage configurations, and fine-grained access control, whereas OpenSearch Serverless is optimized for use cases prioritizing automatic scaling and simplified operations. Both options leverage k-nearest neighbors (k-NN) search to identify document chunks that are semantically similar to a user’s query.

In an enterprise context, semantic search is often complemented by traditional keyword search and metadata filtering. This hybrid search approach is essential for handling queries that involve specific identifiers, dates, or technical terminology that might not be captured by semantic embeddings alone. OpenSearch supports a unified index structure that concurrently stores vector embeddings, raw text chunks, and metadata, enabling complex Boolean queries that can narrow the search space before semantic similarity is calculated.

|                       |                                       |                                      |
| --------------------- | ------------------------------------- | ------------------------------------ |
| Vector Store Feature  | Managed Cluster (OpenSearch)          | Serverless Collection (OpenSearch)   |
| Scaling               | Manual instance management.           | Fully automatic capacity scaling.    |
| Performance Tuning    | Customizable GP3 IOPS and throughput. | Managed performance based on load.   |
| Access Control        | Granular IAM and Cognito integration. | Simplified IAM-based security.       |
| Deployment Complexity | High: requires domain configuration.  | Low: provisioned via "Quick Create". |
| Best Use Case         | Specialized technical requirements.   | Rapid prototyping and standard RAG.  |

### The Role of Metadata in Retrieval Precision

Metadata serves as a structural scaffold for the retrieval process, allowing the system to categorize and filter information based on non-semantic attributes such as department, document version, or publication date. 
Without robust metadata, a RAG system risks retrieving semantically similar but contextually irrelevant information, such as an outdated policy document or a report from a different business unit. 
AWS Knowledge Bases implements metadata through sidecar files—specifically JSON files with the .metadata.json extension—that must be co-located with the source documents in Amazon S3.

During the ingestion process, the Knowledge Base parser extracts these attributes and indexes them within OpenSearch. When a query is executed, the retrieve or retrieve_and_generate API can apply dynamic filters to these attributes, ensuring that the retrieval engine only considers documents that meet specific criteria. This pre-filtering mechanism reduces the computational overhead on the vector store and improves the accuracy of the foundation model by providing a more targeted context.

## DeepEval: A Framework for Objective Performance Assessment

Deploying a RAG system on AWS is only half of the journey; the other half is verification. Enterprise stakeholders require quantitative evidence that the AI system is providing accurate, grounded, and helpful responses.
DeepEval addresses this need by providing an open-source framework that implements advanced "LLM-as-a-judge" techniques. By using more powerful models to evaluate the output of the application model, DeepEval transforms qualitative assessments into repeatable, numerical metrics ranging from 0 to 1

### The RAG Triad for Fundamental Validation

The "RAG Triad" is the foundational framework within DeepEval for evaluating RAG pipelines. It decomposes the interaction into three measurable relationships: Answer Relevancy, Faithfulness, and Contextual Relevancy. This decomposition is vital because it allows developers to pinpoint exactly where a failure occurs—whether in the prompt template, the retrieval strategy, or the choice of the foundation model itself

**Answer Relevancy** measures the alignment between the generated output and the user’s input. This metric focuses on the generator component, evaluating whether the LLM addresses the core of the user's question without including extraneous "fluff" or irrelevant information. A low answer relevancy score typically suggests that the system prompt or the in-context examples provided to the model need refinement

**Faithfulness**—also known as groundedness—measures the degree to which the generated response is based solely on the retrieved context. This metric is the primary defense against hallucinations, ensuring that the model does not invent facts or rely on its own internal training data when those facts are not present in the provided enterprise documents. If a model scores low on faithfulness, it may be necessary to switch to a model with better instruction-following capabilities or a longer context window.

**Contextual Relevancy** assesses the retriever by quantifying the proportion of the retrieved text chunks that are actually relevant to answering the query. This metric is used to optimize hyperparameters such as chunk size and the number of results (top-K) returned by the OpenSearch query. A high score indicates a well-tuned retrieval engine that provides high-signal context to the generator.

|                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                          |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| Metric               | Measured Relationship                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Core Impact                              |
| Answer Relevancy     | Input → Actual Output             | Prompt quality and instruction following |
| Faithfulness         | Retrieval Context → Actual Output | Hallucination detection and grounding    |
| Contextual Relevancy | Input → Retrieval Context.        | Retrieval strategy and top-K tuning      |

### Advanced Retrieval Metrics: Precision and Recall

While the RAG Triad provides a broad overview, complex enterprise systems require the more granular insights offered by Contextual Precision and Contextual Recall. These metrics are "reference-based," meaning they require a "Golden" or ground-truth answer to serve as a benchmark.

**Contextual Recall** measures the extent to which the retrieved context contains all the necessary information to produce the ideal answer. It is calculated by identifying undisputed facts in the ground-truth answer and checking if they can be attributed to the retrieved chunks in OpenSearch. A failure in contextual recall often points to issues in the embedding model or data ingestion phase, where critical information might have been lost due to poor chunking.

**Contextual Precision** evaluates the ranking of the retrieved results. It checks whether the most relevant information appears at the top of the context list provided to the LLM. This is critical because LLMs often exhibit "positional bias," where they prioritize information found at the beginning of the context window. Contextual precision is the primary metric used to evaluate the effectiveness of reranker models in Bedrock.

## Implementing the Evaluation Bridge between AWS and DeepEval

The technical integration of DeepEval with AWS Knowledge Bases involves creating a bridge that extracts the data from the Bedrock runtime and formats it into DeepEval's LLMTestCase structure This process is facilitated by the AWS SDK for Python, Boto3, specifically the bedrock-agent-runtime client.

### Data Extraction from the Bedrock Runtime

To evaluate an interaction, three pieces of data are required: the user's original query (input), the text chunks retrieved from OpenSearch (retrieval_context), and the final answer generated by the foundation model (actual_output). The retrieve_and_generate API provides all three elements in a single response object.

In this workflow, the citations key in the Bedrock response is particularly important. Each citation contains a list of retrievedReferences, which includes the raw text used for grounding and the S3 URI of the source document. This structured output allows developers to reconstruct the exact context window seen by the model during generation, which is a prerequisite for metrics like Faithfulness and Contextual Relevancy.

  

Python  
  

import boto3  
from deepeval.test_case import LLMTestCase  
  
# Initialize the runtime client  
bedrock_agent_runtime = boto3.client('bedrock-agent-runtime', region_name='us-east-1')  
  
# Query the Knowledge Base  
response = bedrock_agent_runtime.retrieve_and_generate(  
    input={'text': 'What is the standard procedure for equipment maintenance?'},  
    retrieveAndGenerateConfiguration={  
        'type': 'KNOWLEDGE_BASE',  
        'knowledgeBaseConfiguration': {  
            'knowledgeBaseId': 'YOUR_KB_ID',  
            'modelArn': 'arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-sonnet-20240229-v1:0'  
        }  
    }  
)  
  
# Extract content for evaluation  
actual_output = response['output']['text']  
# Extract all text chunks from citations  
retrieved_chunks =  
for citation in response.get('citations',):  
    for ref in citation.get('retrievedReferences',):  
        retrieved_chunks.append(ref['content']['text'])  
  
# Create DeepEval Test Case  
test_case = LLMTestCase(  
    input='What is the standard procedure for equipment maintenance?',  
    actual_output=actual_output,  
    retrieval_context=retrieved_chunks  
)  
  
This script serves as the core of a standalone evaluation pipeline. By looping through a dataset of queries and creating these test cases, a developer can use DeepEval's evaluate() function to generate a comprehensive report on the Knowledge Base's performance.

### Configuring Amazon Bedrock as the Evaluator Model

DeepEval utilizes an LLM to calculate most of its metrics. While it defaults to OpenAI, many enterprise environments prefer to use Amazon Bedrock models for evaluation to ensure data remains within the AWS cloud boundary and adheres to existing security agreements. DeepEval supports this through the AmazonBedrockModel class, which uses the Bedrock Runtime Converse API.

Configuring Bedrock as the evaluator requires setting the USE_AWS_BEDROCK_MODEL=1 environment variable and providing AWS credentials. Developers can then specify models like Claude 3 Opus or Nova Pro as the judge. **Using a high-reasoning model for evaluation is crucial**, as the judge must be capable of identifying subtle nuances in factual claims and semantic relevance.

## The Mathematics of Retrieval Accuracy

DeepEval’s metrics are grounded in specific algorithms that convert qualitative LLM observations into quantitative scores. Understanding these calculations is essential for interpreting scores and setting appropriate success thresholds.

### Calculating Faithfulness and Grounding

The Faithfulness score is a ratio that determines how much of the generated response can be objectively attributed to the source material. The judge model first breaks the actual_output into a list of atomic factual claims. It then performs a binary check for each claim against the retrieval_context.

→

A score of 1.0 indicates that every statement in the response is supported by the enterprise documents. If the score drops, DeepEval provides a "Reason" field that lists which specific claims were ungrounded, allowing developers to see if the model is "imagining" details or perhaps conflating information from two different chunks.

### Scoring Contextual Recall

Contextual Recall uses a similar claim-extraction logic but reverses the comparison.  It identifies the "undisputed facts" within the expected_output (ground truth) and checks if those facts were successfully retrieved from OpenSearch.

→

This metric is a direct measure of the retriever’s ability to find relevant information. In an enterprise setting where documents are updated frequently, a low recall score often indicates that the ingestion pipeline hasn't synced the latest documents or that the chunking strategy is cutting off important context.

## Optimization Strategies for AWS Knowledge Bases

The primary utility of DeepEval is not just to generate reports but to drive iterative improvements in the RAG pipeline. By tracking metrics over time, organizations can see the impact of various optimization techniques within the AWS environment.

### Improving Recall through Chunking and Parsing

Chunking is the process of splitting large documents into smaller pieces that can be embedded effectively. If chunks are too small, the model may lose the overall context; if they are too large, irrelevant information may dilute the semantic signal. AWS Knowledge Bases supports several advanced chunking strategies to optimize this.

|                   |                                                    |                                                       |
| ----------------- | -------------------------------------------------- | ----------------------------------------------------- |
| Chunking Strategy | Mechanism                                          | Impact on Metrics                                     |
| Fixed-Size        | Constant token counts with a set overlap.          | Baseline performance; predictable cost.               |
| Semantic          | Uses embeddings to identify sentence boundaries.   | High Contextual Recall: maintains meaning.            |
| Hierarchical      | Creates parent-child relationships between chunks. | Improved precision: returns granular info in context. |
| Custom (Lambda)   | User-defined logic for specialized document types. | Maximum flexibility for structured data.              |

Semantic chunking is particularly effective for complex reports where meaning is tied to logical paragraph structures. By setting similarity thresholds, the Knowledge Base can ensure that sentences related to the same topic stay together, thereby increasing the signal-to-noise ratio in the retrieval stage.

### Optimizing Precision with Reranking and Filtering

While chunking improves recall, reranking is the most powerful tool for improving precision.A reranker model (such as those from Cohere or Amazon) takes the top N results from the initial OpenSearch vector search and re-evaluates them using a cross-encoder approach. This ensures that the single most relevant chunk is placed at position one, which has been shown in workshops to result in the "highest accuracy" for RAG pipelines.

DeepEval's Contextual Precision metric provides a clear way to validate this improvement. By comparing the scores of a pipeline with and without a reranker, developers can justify the additional latency and cost of the reranking step. Furthermore, metadata filtering can be used to prune the search space before reranking, further enhancing the system's ability to discriminate between similar-sounding documents from different time periods or departments.

## Advanced Evaluation: Tracing and Multi-Turn Chatbots

Modern enterprise chatbots are rarely single-turn systems; they are conversational agents that maintain state over multiple exchanges. Evaluating these systems requires a more sophisticated approach than simple input-output testing.

### Tracing with the @observe Decorator

DeepEval’s @observe decorator allows developers to instrument their RAG code to capture internal state without restructuring the application. In a Bedrock-based application, this can be used to trace the retrieve call and the subsequent model invocation as separate spans.

Tracing provides several advantages for enterprise teams:

1. Dynamic Test Case Generation: By tracing production interactions, developers can capture real-world user queries and retrieval contexts to build a more representative test suite.
    
2. Component-Level Evaluation: Metrics can be applied directly to internal functions. For example, the FaithfulnessMetric can be applied to the output of the generator function, while the ContextualRelevancyMetric is applied to the retriever function.
    
3. Debugging Traceability: When a test fails on the AI platform, developers can drill down into the trace to see exactly which text chunks were retrieved and what the model’s internal reasoning was before it produced the final answer.
    
### Conversational and Agentic Metrics

For multi-turn chatbots, DeepEval introduces "Conversational" metrics that evaluate the entire dialogue history. These include metrics like Conversation Relevancy, which checks if the chatbot’s responses remain on-topic across multiple turns, and Role Adherence, which ensures the bot stays within its persona (e.g., as a formal technical support agent).

In more advanced agentic workflows—where the chatbot might use tools to look up data in an external database—DeepEval offers metrics like Tool Correctness and Step Efficiency. These are critical for AWS environments where agents might be using Lambda functions to perform real-time lookups alongside the Knowledge Base retrieval.

## Scaling Evaluation with Synthetic Data Generation

One of the largest barriers to rigorous evaluation is the manual effort required to create a diverse and comprehensive test dataset. DeepEval’s Synthesizer addresses this by using the documents in the Knowledge Base to automatically generate thousands of "Goldens"—pairs of high-quality queries and reference answers.

### The Data Evolution Process

DeepEval’s synthesizer uses a technique called "Data Evolution," originally inspired by Evol-Instruct. The process begins by chunking the documents in the Knowledge Base and selecting semantically rich context clusters. It then uses a powerful model to generate a basic question from that context.

To ensure the test suite covers more than just simple factual recall, the synthesizer "evolves" these questions into more complex forms. These evolutions include:

- Reasoning: Rewriting the question to require multi-step logical deduction.
    
- Multi-Context: Creating a question that can only be answered by combining information from two or more document chunks.
    
- In-Breadth Coverage: Broadening the topics covered to ensure the entire Knowledge Base is tested.
    
This synthetic dataset serves as a "stress test" for the RAG pipeline. If the Knowledge Base is updated with a new set of product manuals, the synthesizer can quickly generate a new test suite to ensure that the RAG system remains accurate for the new material.

## Comparing DeepEval with Native AWS Evaluation Tools

AWS provides built-in evaluation features for Knowledge Bases, which can be accessed through the Bedrock console or the bedrock-agentcore API. Understanding the differences between DeepEval and these native tools is essential for defining an enterprise evaluation strategy.

### Native Bedrock Evaluation Features

Bedrock's native evaluation is primarily designed for large-scale, asynchronous batch jobs. It supports evaluating both retrieval-only and retrieval-with-generation workflows. The service provides a selection of "Built-in" evaluators for metrics like Helpfulness, Correctness, and Faithfulness.

The primary advantage of Bedrock evaluation is its seamless integration with other AWS services. For example, it integrates with S3 for data input/output and CloudWatch for monitoring evaluation progress. It also includes responsible AI metrics such as harmfulness and stereotyping, which are integrated with Bedrock Guardrails.

### Strategic Integration for Enterprise Readiness

For many enterprise teams, the optimal approach is a "Hybrid Evaluation Strategy" that uses DeepEval for local development and CI/CD testing, and Bedrock's native evaluation for final pre-production benchmarking and compliance monitoring.

|               |                                  |                                  |
| ------------- | -------------------------------- | -------------------------------- |
| Feature       | DeepEval Framework               | AWS Bedrock Evaluations          |
| Core Focus    | Developer-centric; CI/CD.        | Management-centric; Batch jobs.  |
| Metric Depth  | 50+ research-backed metrics.     | Focused set of standard metrics. |
| Tracing       | Real-time component observation. | Post-hoc job analysis.           |
| Deployment    | Python library.                  | Managed service.                 |
| Data Location | Local or Cloud (Confident AI).   | strictly AWS (S3/Bedrock).       |

DeepEval's flexibility in allowing custom judge models and modified prompt templates is a major advantage during the R&D phase when developers are trying to understand the failure modes of a new retrieval strategy. Once the strategy is finalized, the Bedrock native evaluation can be used to run a 1,000-prompt benchmark to satisfy corporate governance and risk management requirements.

## Operationalizing Evaluation for Production Chatbots

Transforming evaluation from a one-time project into a sustainable operational process requires careful planning around data engineering, security, and performance.

### Security, Permissions, and Data Governance

In an enterprise AWS environment, all interactions must be governed by IAM policies.  The Bedrock execution role must have the necessary permissions to read from S3 buckets, write to OpenSearch indices, and invoke foundation models. When using DeepEval, it is essential to ensure that the environment where evaluation scripts are running has similar permissions.

Furthermore, data privacy is a significant concern. DeepEval’s integration with Bedrock allows metrics to be calculated without data leaving the AWS VPC if configured correctly. Organizations should also use Bedrock Guardrails to filter out PII (Personally Identifiable Information) or sensitive content before it is even sent to the evaluator, ensuring that the evaluation process itself does not violate security policies.

### Managing Latency and API Rate Limits

Running an evaluation job involving 500 test cases with 5 metrics each results in 2,500 LLM calls. This can quickly hit the rate limits for foundation models on Bedrock. DeepEval provides built-in support for managing this through the AsyncConfig class, which allows developers to set a maximum number of concurrent requests and implement throttling.

Additionally, monitoring latency is critical. While the focus of DeepEval is quality, the Boto3 logs and Bedrock metrics in CloudWatch provide data on how long each retrieval and generation step takes. A RAG system that is 99% accurate but takes 30 seconds to respond is often unusable for customer-facing chatbots, necessitating a balance between accuracy and response speed.

## Nuanced Conclusions on Enterprise RAG Evaluation

The journey toward a production-ready chatbot grounded in enterprise documents is iterative and data-driven. The evidence gathered in this analysis indicates that AWS Knowledge Bases provides a robust, managed infrastructure, but its success is entirely dependent on the strategic configuration of retrieval parameters like chunking, metadata filtering, and reranking.  DeepEval serves as the essential navigational tool for this journey, transforming subjective observations of chatbot behavior into actionable, research-backed metrics.

A comprehensive evaluation strategy must prioritize the "RAG Triad" to detect hallucinations and ensure relevancy, while also deep-diving into retrieval precision and recall to optimize the search backend in OpenSearch. By utilizing synthetic data generation, teams can maintain high evaluation coverage even as document volume scales, and by implementing component-level tracing, they can debug complex failure modes with surgical precision.

Ultimately, the most successful enterprise chatbots are those built on a foundation of "continuous evaluation". By integrating DeepEval into the development lifecycle and leveraging Bedrock’s native evaluation for final compliance, organizations can deploy AI systems with the confidence that they are providing accurate, safe, and helpful information to their users. This systematic approach ensures that the RAG pipeline remains a valuable asset for the business, capable of evolving alongside the ever-changing landscape of corporate knowledge.

#### Works cited

1. Using the RAG Triad for RAG evaluation | DeepEval by Confident AI, accessed April 8, 2026, [https://deepeval.com/guides/guides-rag-triad](https://deepeval.com/guides/guides-rag-triad)
    
2. RAG Testing with DeepEval: A Hands-On Guide to Reliable Retrieval-Augmented Generation - Victory Square Partners, accessed April 8, 2026, [https://victorysquarepartners.com/rag-testing-with-deepeval/](https://victorysquarepartners.com/rag-testing-with-deepeval/)
    
3. How to Use Amazon Bedrock Knowledge Bases for RAG - OneUptime, accessed April 8, 2026, [https://oneuptime.com/blog/post/2026-02-12-amazon-bedrock-knowledge-bases-rag/view](https://oneuptime.com/blog/post/2026-02-12-amazon-bedrock-knowledge-bases-rag/view)
    
4. Foundation Models for RAG - Amazon Bedrock Knowledge Bases, accessed April 8, 2026, [https://aws.amazon.com/bedrock/knowledge-bases/](https://aws.amazon.com/bedrock/knowledge-bases/)
    
5. Improve search results for AI using Amazon OpenSearch Service as a vector database with Amazon Bedrock | AWS Big Data Blog, accessed April 8, 2026, [https://aws.amazon.com/blogs/big-data/improve-search-results-for-ai-using-amazon-opensearch-service-as-a-vector-database-with-amazon-bedrock/](https://aws.amazon.com/blogs/big-data/improve-search-results-for-ai-using-amazon-opensearch-service-as-a-vector-database-with-amazon-bedrock/)
    
6. Building Intelligent Search with Amazon Bedrock and Amazon OpenSearch for hybrid RAG solutions, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/building-intelligent-search-with-amazon-bedrock-and-amazon-opensearch-for-hybrid-rag-solutions/](https://aws.amazon.com/blogs/machine-learning/building-intelligent-search-with-amazon-bedrock-and-amazon-opensearch-for-hybrid-rag-solutions/)
    
7. RAG Evaluation Quickstart | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/docs/getting-started-rag](https://deepeval.com/docs/getting-started-rag)
    
8. Introduction to LLM Metrics | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/docs/metrics-introduction](https://deepeval.com/docs/metrics-introduction)
    
9. Building a Knowledge-Base Agent with Amazon Bedrock and Strands | AWS Builder Center, accessed April 8, 2026, [https://builder.aws.com/content/37QDCywzwqZPDQ4zTpDnsowXLsT/building-a-knowledge-base-agent-with-amazon-bedrock-and-strands](https://builder.aws.com/content/37QDCywzwqZPDQ4zTpDnsowXLsT/building-a-knowledge-base-agent-with-amazon-bedrock-and-strands)
    
10. Amazon Bedrock Knowledge Bases now supports Amazon OpenSearch Service Managed Cluster as vector store | Artificial Intelligence - AWS, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-knowledge-bases-now-supports-amazon-opensearch-service-managed-cluster-as-vector-store/](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-knowledge-bases-now-supports-amazon-opensearch-service-managed-cluster-as-vector-store/)
    
11. Optimizing RAG Pipelines with Amazon Bedrock: Chunking, Metadata, Reranking, and Evaluation | AWS Builder Center, accessed April 8, 2026, [https://builder.aws.com/content/36SOCCxQN0Dm1zj8nroBbWtV8k5/optimizing-rag-pipelines-with-amazon-bedrock-chunking-metadata-reranking-and-evaluation](https://builder.aws.com/content/36SOCCxQN0Dm1zj8nroBbWtV8k5/optimizing-rag-pipelines-with-amazon-bedrock-chunking-metadata-reranking-and-evaluation)
    
12. How to Build a RAG Application with Amazon Bedrock and OpenSearch - OneUptime, accessed April 8, 2026, [https://oneuptime.com/blog/post/2026-02-12-build-a-rag-application-with-amazon-bedrock-and-opensearch/view](https://oneuptime.com/blog/post/2026-02-12-build-a-rag-application-with-amazon-bedrock-and-opensearch/view)
    
13. Evaluate and improve performance of Amazon Bedrock Knowledge Bases | Artificial Intelligence - AWS, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/evaluate-and-improve-performance-of-amazon-bedrock-knowledge-bases/](https://aws.amazon.com/blogs/machine-learning/evaluate-and-improve-performance-of-amazon-bedrock-knowledge-bases/)
    
14. [Workshop 2] Retrieve Data from Documents with Bedrock and Knowledge Bases, accessed April 8, 2026, [https://builder.aws.com/content/36O7nnukL3R3olRZZpUPt7jS0ST/workshop-2-retrieve-data-from-documents-with-bedrock-and-knowledge-bases](https://builder.aws.com/content/36O7nnukL3R3olRZZpUPt7jS0ST/workshop-2-retrieve-data-from-documents-with-bedrock-and-knowledge-bases)
    
15. Supercharging RAG: How Metadata enhance retrieval in Amazon Bedrock Knowledge Bases | by Chiara Relandini | Medium, accessed April 8, 2026, [https://medium.com/@crelandini/supercharging-rag-how-metadata-enhance-retrieval-in-amazon-bedrock-knowledge-bases-6e05f24043fe](https://medium.com/@crelandini/supercharging-rag-how-metadata-enhance-retrieval-in-amazon-bedrock-knowledge-bases-6e05f24043fe)
    
16. Metadata filtering for tabular data with Amazon Bedrock Knowledge Bases - AWS, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/metadata-filtering-for-tabular-data-with-knowledge-bases-for-amazon-bedrock/](https://aws.amazon.com/blogs/machine-learning/metadata-filtering-for-tabular-data-with-knowledge-bases-for-amazon-bedrock/)
    
17. Enhancing search in Amazon Bedrock Knowledge Base | by raji krishnamoorthy - Medium, accessed April 8, 2026, [https://raji-krishnamoorthy.medium.com/enhancing-search-in-amazon-bedrock-knowledge-base-dc7269ef62fb](https://raji-krishnamoorthy.medium.com/enhancing-search-in-amazon-bedrock-knowledge-base-dc7269ef62fb)
    
18. Amazon Bedrock Knowledge Bases now supports metadata filtering to improve retrieval accuracy | Artificial Intelligence, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-knowledge-bases-now-supports-metadata-filtering-to-improve-retrieval-accuracy/](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-knowledge-bases-now-supports-metadata-filtering-to-improve-retrieval-accuracy/)
    
19. Dynamic metadata filtering for Amazon Bedrock Knowledge Bases with LangChain - AWS, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/dynamic-metadata-filtering-for-amazon-bedrock-knowledge-bases-with-langchain/](https://aws.amazon.com/blogs/machine-learning/dynamic-metadata-filtering-for-amazon-bedrock-knowledge-bases-with-langchain/)
    
20. # Complete Guide to RAG Evaluations in Amazon Bedrock - DEV Community, accessed April 8, 2026, [https://dev.to/rajmurugan/-complete-guide-to-rag-evaluations-in-amazon-bedrock-4je3](https://dev.to/rajmurugan/-complete-guide-to-rag-evaluations-in-amazon-bedrock-4je3)
    
21. Evaluating RAG applications with Amazon Bedrock knowledge base evaluation - AWS, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/evaluating-rag-applications-with-amazon-bedrock-knowledge-base-evaluation/](https://aws.amazon.com/blogs/machine-learning/evaluating-rag-applications-with-amazon-bedrock-knowledge-base-evaluation/)
    
22. RAG Evaluation Metrics: Assessing Answer Relevancy, Faithfulness, Contextual Relevancy, And More - Confident AI, accessed April 8, 2026, [https://www.confident-ai.com/blog/rag-evaluation-metrics-answer-relevancy-faithfulness-and-more](https://www.confident-ai.com/blog/rag-evaluation-metrics-answer-relevancy-faithfulness-and-more)
    
23. RAG Evaluation Metrics Explained: A Complete Guide with Examples | by Sanjeeb Panda, accessed April 8, 2026, [https://medium.com/@sanjeebmeister/rag-evaluation-metrics-explained-a-complete-guide-with-examples-dea8bf4467db](https://medium.com/@sanjeebmeister/rag-evaluation-metrics-explained-a-complete-guide-with-examples-dea8bf4467db)
    
24. Contextual Recall | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/docs/metrics-contextual-recall](https://deepeval.com/docs/metrics-contextual-recall)
    
25. Contextual Precision | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/docs/metrics-contextual-precision](https://deepeval.com/docs/metrics-contextual-precision)
    
26. Amazon Bedrock | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/integrations/models/amazon-bedrock](https://deepeval.com/integrations/models/amazon-bedrock)
    
27. Single-Turn Test Case | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/docs/evaluation-test-cases](https://deepeval.com/docs/evaluation-test-cases)
    
28. retrieve - Boto3 1.42.84 documentation, accessed April 8, 2026, [https://docs.aws.amazon.com/boto3/latest/reference/services/bedrock-agent-runtime/client/retrieve.html](https://docs.aws.amazon.com/boto3/latest/reference/services/bedrock-agent-runtime/client/retrieve.html)
    
29. Boto3 Knowledge Base Retrieve: Unlock AI's Full Potential (2024) - CodeGive, accessed April 8, 2026, [https://codegive.com/blog/boto3_knowledge_base_retrieve.php](https://codegive.com/blog/boto3_knowledge_base_retrieve.php)
    
30. retrieve_and_generate - Boto3 1.42.84 documentation, accessed April 8, 2026, [https://docs.aws.amazon.com/boto3/latest/reference/services/bedrock-agent-runtime/client/retrieve_and_generate.html](https://docs.aws.amazon.com/boto3/latest/reference/services/bedrock-agent-runtime/client/retrieve_and_generate.html)
    
31. Introduction to LLM Evals | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/docs/evaluation-introduction](https://deepeval.com/docs/evaluation-introduction)
    
32. Systematic AI Agent Evaluation: DeepEval Framework Powered by DeepSeek - Medium, accessed April 8, 2026, [https://medium.com/@manuedavakandam/systematic-ai-agent-evaluation-deepeval-framework-powered-by-deepseek-c81d39b13f8b](https://medium.com/@manuedavakandam/systematic-ai-agent-evaluation-deepeval-framework-powered-by-deepseek-c81d39b13f8b)
    
33. Frequently Asked Questions | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/docs/faq](https://deepeval.com/docs/faq)
    
34. Amazon Bedrock Knowledge Bases now supports advanced parsing, chunking, and query reformulation giving greater control of accuracy in RAG based applications | Artificial Intelligence, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-knowledge-bases-now-supports-advanced-parsing-chunking-and-query-reformulation-giving-greater-control-of-accuracy-in-rag-based-applications/](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-knowledge-bases-now-supports-advanced-parsing-chunking-and-query-reformulation-giving-greater-control-of-accuracy-in-rag-based-applications/)
    
35. Contextual retrieval in Anthropic using Amazon Bedrock Knowledge Bases - AWS, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/contextual-retrieval-in-anthropic-using-amazon-bedrock-knowledge-bases/](https://aws.amazon.com/blogs/machine-learning/contextual-retrieval-in-anthropic-using-amazon-bedrock-knowledge-bases/)
    
36. LLM Tracing | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/docs/evaluation-llm-tracing](https://deepeval.com/docs/evaluation-llm-tracing)
    
37. Deployment | DeepEval by Confident AI - The LLM Evaluation Framework, accessed April 8, 2026, [https://deepeval.com/tutorials/rag-qa-agent/evals-in-prod](https://deepeval.com/tutorials/rag-qa-agent/evals-in-prod)
    
38. Trace Amazon Bedrock applications - Docs by LangChain, accessed April 8, 2026, [https://docs.langchain.com/langsmith/trace-bedrock](https://docs.langchain.com/langsmith/trace-bedrock)
    
39. Generate Synthetic Test Data for LLM Applications | DeepEval by Confident AI, accessed April 8, 2026, [https://deepeval.com/guides/guides-using-synthesizer](https://deepeval.com/guides/guides-using-synthesizer)
    
40. LLM-as-a-judge on Amazon Bedrock Model Evaluation | Artificial Intelligence, accessed April 8, 2026, [https://aws.amazon.com/blogs/machine-learning/llm-as-a-judge-on-amazon-bedrock-model-evaluation/](https://aws.amazon.com/blogs/machine-learning/llm-as-a-judge-on-amazon-bedrock-model-evaluation/)
    
41. evaluate - Boto3 1.42.83 documentation, accessed April 8, 2026, [https://docs.aws.amazon.com/boto3/latest/reference/services/bedrock-agentcore/client/evaluate.html](https://docs.aws.amazon.com/boto3/latest/reference/services/bedrock-agentcore/client/evaluate.html)
    
42. Practical LLM Evaluation: Deepchecks and Bedrock, accessed April 8, 2026, [https://deepchecks.com/practical-llm-evaluation-deepchecks-bedrock/](https://deepchecks.com/practical-llm-evaluation-deepchecks-bedrock/)
    
43. amazon-bedrock-samples/evaluation-observe/bedrock-rag-evaluation/knowledge-base-evaluation-job.ipynb at main - GitHub, accessed April 8, 2026, [https://github.com/aws-samples/amazon-bedrock-samples/blob/main/evaluation-observe/bedrock-rag-evaluation/knowledge-base-evaluation-job.ipynb](https://github.com/aws-samples/amazon-bedrock-samples/blob/main/evaluation-observe/bedrock-rag-evaluation/knowledge-base-evaluation-job.ipynb)
    
44. Using Custom LLMs for Evaluation | DeepEval by Confident AI, accessed April 8, 2026, [https://deepeval.com/guides/guides-using-custom-llms](https://deepeval.com/guides/guides-using-custom-llms)
    
45. Mastering boto3 bedrock invoke_model (2026): Unlock AI's Full Potential for Your Python Applications! - CodeGive, accessed April 8, 2026, [https://codegive.com/blog/boto3_bedrock_invoke_model.php](https://codegive.com/blog/boto3_bedrock_invoke_model.php)
    
46. End-to-End LLM Evaluation | DeepEval by Confident AI, accessed April 8, 2026, [https://deepeval.com/docs/evaluation-end-to-end-llm-evals](https://deepeval.com/docs/evaluation-end-to-end-llm-evals)

## Connections
- [[RAG architecture]]
- [[Evaluation loops]]
- [[Evaluator Paradox]]
- [[Self-Evaluation in RAG]]
- [[Chunking strategies]]
- [[Vector search]]
- [[Agentic RAG]]
- [[AIaaS Platform]]

Up: [[AI Systems]]

## Tags
#ai
