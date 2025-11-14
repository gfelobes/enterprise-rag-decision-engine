# Enterprise RAG Decision Engine (LangGraph)

An advanced RAG + multi-agent system using LangGraph subgraphs, memory, and optional fine-tuning to act as an AI Architecture Reviewer.

## Features

- Hybrid RAG pipeline (BM25 + dense embeddings)
- Reranker for better context selection
- LangGraph main workflow with retrieval, reasoning, and evaluation subgraphs
- Persistent memory node to track conversation context and constraints
- Self-refinement loop for answers (bounded number of iterations)
- Optional fine-tuning of a small model on architecture Q&A
- Evaluation metrics for RAG quality and answer consistency

## Tech Stack

- Python
- LangGraph / LangChain
- Vector DB (Chroma / Weaviate / Qdrant)
- FastAPI
- Any LLM + optional fine-tuned model

## Getting Started

```bash
pip install -r requirements.txt
python -m src.rag.index_builder   # build index from data/docs
uvicorn src.services.api:app --reload
```

## Demo Scenario
- Upload or use sample architecture docs in data/docs/.
- Ask: “Design a workflow with sub-second agent coordination for X scenario.”
- Show LangGraph visualization with subgraphs + memory node.
- Optionally compare base vs fine-tuned model for structured answers.

## Design Notes
See docs/graph-diagrams.md for DAG and subgraph layouts.
See docs/eval-metrics.md for how RAG quality is measured.





### 📁 Structure
```bash
enterprise-rag-decision-engine/
├─ src/
│  ├─ rag/
│  │  ├─ index_builder.py
│  │  ├─ retriever.py
│  │  └─ reranker.py
│  ├─ graph/
│  │  ├─ main_graph.py
│  │  ├─ subgraphs/
│  │  │  ├─ retrieval_graph.py
│  │  │  ├─ reasoning_graph.py
│  │  │  └─ evaluation_graph.py
│  │  └─ memory_node.py
│  ├─ finetune/
│  │  ├─ dataset_builder.py
│  │  └─ train.py
│  ├─ services/
│  │  └─ api.py
│  └─ config/
│     └─ settings.py
├─ data/
│  ├─ docs/                 # tech architecture docs
│  └─ training/             # Q&A for fine-tuning
├─ tests/
│  ├─ test_retrieval.py
│  └─ test_graph_flows.py
├─ docs/
│  ├─ architecture.md
│  ├─ graph-diagrams.md
│  └─ eval-metrics.md
├─ README.md
└─ requirements.txt
```
