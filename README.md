#RAG MODEL

This project provides a minimal, well-structured implementation of a Retrieval-Augmented Generation (RAG) pipeline. RAG is a powerful technique that enhances Large Language Models (LLMs) by grounding their responses in a user-provided knowledge base. This helps to reduce hallucinations, provide up-to-date information, and offer answers based on specific, private documents.

This basic model demonstrates the core workflow:

-Load documents from a source (e.g., text files, PDFs).

-Split documents into manageable chunks.

-Embed these chunks and store them in a vector database (in-memory FAISS).

-Retrieve the most relevant chunks for a user query.

-Generate a response by providing the retrieved context to a Language Model (LLM).
