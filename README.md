**RAG MODEL**

This project provides a minimal, well-structured implementation of a Retrieval-Augmented Generation (RAG) pipeline. RAG is a powerful technique that enhances Large Language Models (LLMs) by grounding their responses in a user-provided knowledge base. This helps to reduce hallucinations, provide up-to-date information, and offer answers based on specific, private documents.

This basic model demonstrates the core workflow:

-Load documents from a source (e.g., text files, PDFs).

-Split documents into manageable chunks.

-Embed these chunks and store them in a vector database (in-memory FAISS).

-Retrieve the most relevant chunks for a user query.

-Generate a response by providing the retrieved context to a Language Model (LLM).


# GraphRAG

## What it is
GraphRAG (Graph Retrieval-Augmented Generation) is a variant of RAG that retrieves from a **knowledge graph** instead of (or alongside) raw text chunks. Rather than pulling isolated passages by embedding similarity, it pulls connected entities, relationships, and community summaries — giving the LLM structured context to reason over.

## Why it exists
Traditional RAG struggles with:
- **Multi-hop questions** — answers that require connecting facts across multiple documents
- **Global / thematic questions** — "What are the main themes in this corpus?" (no single chunk answers this)
- **Relationship-heavy queries** — "How is X connected to Y?"

GraphRAG addresses these by giving the retriever *structure*, not just similarity.

## How it works
1. **Extract** — an LLM reads source documents and extracts entities (people, places, concepts) and relationships between them.
2. **Build the graph** — entities become nodes, relationships become edges. Related nodes are often clustered into **communities**.
3. **Summarize** — each community gets a generated summary, capturing its key themes at different levels of granularity.
4. **Retrieve** — at query time, relevant nodes/edges or community summaries are pulled (via traversal, not just vector similarity).
5. **Generate** — the LLM answers using this connected, structured context instead of disjointed chunks.

## Traditional RAG vs. GraphRAG

| | Traditional RAG | GraphRAG |
|---|---|---|
| Data structure | Flat text chunks | Knowledge graph (nodes + edges) |
| Retrieval | Vector similarity search | Graph traversal + community summaries |
| Good at | Direct factual lookup | Multi-hop reasoning, thematic/global questions |
| Cost | Cheaper, simpler to build | Higher upfront cost (extraction + graph build) |

## When to use it
- Large, interconnected corpora (research papers, legal docs, internal wikis)
- Questions that span multiple documents or require reasoning over relationships
- Need for both local (specific fact) and global (summary/theme) queries

## When traditional RAG is enough
- Simple fact lookup from a single source
- Small or loosely related document sets
- Latency/cost is a tight constraint

## Reference
Microsoft Research's original GraphRAG paper and open-source implementation are the most commonly cited starting point for further reading.
