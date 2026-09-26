# Enterprise Hybrid RAG Analyzer for Legal & Financial Documents

An enterprise-grade Retrieval-Augmented Generation (RAG) pipeline built for parsing and answering complex queries over dense financial reports and legal credit agreements. Designed to solve common enterprise LLM failures: **recall blind spots, context noise, and hallucinations.**

---

## Architecture & Tech Stack

```text
[PDF / 10-K Document] 
       │
       ▼
[Semantic Chunking (900/180 + Semicolon Split)]
       │
       ├─────────────────────────┐
       ▼                         ▼
[BM25 Sparse Index]    [FAISS Dense Vector Index]
       │                         │
       └───────────┬─────────────┘
                   ▼
         [Ensemble Retriever (50/50 RRF)]
                   │ (Top 15 Chunks)
                   ▼
     [Cohere Cross-Encoder Reranker]
                   │ (Top 4 Chunks)
                   ▼
       [ChatGroq (Llama 3) LLM + Guardrails]
                   │
                   ▼
         [Ragas Evaluation Telemetry]
