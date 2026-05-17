# Enterprise-Gen-AI-policy---RAG-Governance-Framework
Enterprise Gen AI policy - RAG Governance Framework
Architected a high-maturity Trust & Safety RAG framework using LangChain, ChromaDB, and local HuggingFace embeddings to automate content moderation audits with
strict metadata-driven source citations. Optimized document hierarchy preservation and contextual recall by decoupling version-controlled system prompts into YAML configurations and integrating a two-stage deep learning Cross-Encoder Reranker. Implemented an automated local evaluation pipeline leveraging the Ragas framework 
and cosine similarity matrices against a golden dataset, establishing an automated deployment gate that validated system faithfulness above a 0.80 production-ready threshold.

[ Step 1: Ingestion ]
    Raw Policy Text (.md) 
           │
           ▼
    Recursive Splitter (No Token Overlap)
           │
           ▼
    HuggingFace Embeddings (Vector Generation)
           │
           ▼
    ChromaDB (Local Vector Storage with Source Metadata)

 ──────────────────────────────────────────────────────────

 [ Step 2: Retrieval & Reranking ]
    User Query ("Is religious mocking allowed?")
           │
           ▼
    Vector Similarity Search (Pulls Top 3 Candidate Chunks)
           │
           ▼
    Cross-Encoder Model (Reranks chunks jointly for max accuracy)
           │
           ▼
    Extract Best Chunk + Match with Versioned YAML Prompt

 ──────────────────────────────────────────────────────────

 [ Step 3: Evaluation (The Gatekeeper) ]
    RAG Output vs. Pre-defined Golden Dataset (Ground Truth)
           │
           ▼
    Cosine Similarity & Ragas Framework Metric Evaluation
           │
           ▼
     [ Is Score > 0.80? ]
          ├── YES ──► ✅ STATUS: PRODUCTION READY (Merge Allowed)
          └── NO  ──► ❌ STATUS: NEEDS POLICY TUNING (Block Deployment)
