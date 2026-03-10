# langgraph-local-pdf-rag
Production-style, local Retrieval-Augmented Generation (RAG) assistant for PDFs.
Runs fully locally using an Ollama-served Mistral model, orchestration via LangGraph and LangChain, and a local vector store (Chroma / FAISS). Designed for privacy-first deployments and offline-first engineering teams.


### Project description
langgraph-local-pdf-rag is a local-first RAG system that:

- Ingests many PDFs and slices them into semantic chunks.
- Stores embeddings and chunk metadata (doc_version, embedding_version) in a partitioned vector DB (Chroma / FAISS).
- Performs hash-based chunk diffing and upserts only changed chunks (individual updates).
- Orchestrates retrieval → prompt construction → LLM generation via a LangGraph workflow.
- Uses a Mistral model served by a local Ollama instance for inference.
- Provides a clean, extendable codebase suitable for productionization and open-source collaboration.

Key technologies: LangGraph, LangChain, Ollama, Mistral, Chroma / FAISS, sentence-transformers, and PyPDF.

### Features

- PDF ingestion and page-level extraction
- Chunking (configurable size + overlap)
- Local embeddings (sentence-transformers)
- Vector DB with partitioning (Chroma collections per namespace)
- Chunk-level hashing + upsert for incremental updates (tombstone support)
- Document & embedding versioning (doc_version, embedding_version)
- LangGraph workflow for retrieval → prompt → generate → response
- Local LLM generation using Ollama + Mistral (streaming-ready)
- Source citation in answers (file + page + chunk)
- Simple FastAPI demo endpoints (sync + streaming placeholders)
- Production guidance & scaling notes

### Tech stack

- Python 3.10+
- LangGraph (workflow orchestration)
- LangChain (utilities, text splitters)
- Chroma (default vector store; optional: FAISS)
- sentence-transformers (local embedder; all-MiniLM-L6-v2 recommended)
- PyPDF (PDF text extraction)
- Ollama (serves Mistral locally)
- FastAPI for demo API / streaming endpoints

### Folder structure

pdf-rag-local/
├── LICENSE
├── README.md
├── requirements.txt
├── .env.example
├── data/
│   ├── pdfs/                # place PDFs here for ingestion
│   └── vectordb/            # Chroma / FAISS persistence
├── src/
│   ├── __init__.py
│   ├── config.py
│   ├── utils.py
│   ├── embeddings.py
│   ├── vector_store.py
│   ├── ingest.py
│   ├── llm.py
│   ├── rag_graph.py
│   ├── app.py               # FastAPI server (demo)
│   └── examples/
│       └── demo_ingest.sh
└── docs/
    └── architecture.md
