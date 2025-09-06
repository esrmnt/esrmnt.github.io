---
layout: post
title: "RAG: The System Works (Terms and Conditions Apply)"
subtitle: Getting acquainted with Retrieval-Augmented Generation
date: 2025-08-02 10:35:00 +0000
tags:
- rag
- ai
---
Well, this is unexpected. I managed to build a functional basic RAG system. And it actually works. Who saw that coming?

### What Do Have Here

Meet **Reference Chat** — a local document search and chat assistant that lets you upload PDF and TXT files, then ask questions about them using a local language model. Everything runs locally, so the documents never leave my machine. No cloud dependencies, no privacy concerns, no additional cost - just me and my PDFs having a conversation.

I've noticed that the RAG system struggles with converted PDFs, i.e when I convert PPTs to PDF. Most of the times text content that the extractor and indexer gets are missing the content from embedded images. I'm guessing that could be the issue. I need to attend to it, mostly over next weekend. 

#### The Core Features

- **Local-only processing**: The documents stay on my machine where they belong
- **Document upload and management**: PDF and TXT support (more formats coming when I'm feeling brave enough)
- **Semantic and keyword search**: Because sometimes you need both approaches
- **Chat interface**: Ask questions and get answers with proper citations
- **REST API**: For when you want to integrate it with other tools
- **Streamlit**: A quick and easy way to build interactive frontend

### The Architecture (Or: How I Organized the Chaos)

The backend is built with FastAPI and handles document processing, search, and chat endpoints. The frontend is built with Streamlit and provides a web interface for uploading, searching, and chatting with documents. Ollama is used for local language model inference. All document data and processing remain local.

![High level Setup](https://github.com/esrmnt/local-ref-chat/blob/main/images/architecture.png?raw=true)

#### Backend (FastAPI)
```
backend/
├── main.py              # Application setup with lifespan management
├── settings.py          # Environment-based configuration
├── models.py            # Pydantic request/response models
├── logging_config.py    # Structured logging setup
├── config.py            # Backward compatibility layer
├── core/
│   ├── document_manager.py # File handling, validation, text extraction
│   ├── indexer.py          # Semantic indexing and search
│   ├── model.py           # Ollama LLM integration
│   ├── utils.py           # Text processing utilities
│   └── state.py           # Application state management
└── api/
    ├── knowledge.py       # Document upload/management endpoints
    ├── search.py          # Search endpoints (keyword/semantic)
    └── chat.py            # RAG chat endpoints
```

#### Frontend (Streamlit)
```
frontend/
├── app.py               # Main Streamlit application
├── components/          # Reusable UI components (future)
└── pages/               # Multi-page app structure (future)
```

### The Tech Stack and Implementation Details

I ended up using:
- **FastAPI** for the backend (because it makes APIs almost enjoyable)
- **SentenceTransformers** with `all-MiniLM-L6-v2` model for embeddings 
- **Ollama** for local LLM serving (defaulting to Llama3 but configurable)
- **Streamlit** for the frontend (who knew building UIs could be this simple?)
- **In-memory storage** with numpy arrays for similarity search (keeping it simple for now)
- **NLTK** for sentence tokenization and **PyPDF2** for PDF text extraction

### How It Actually Works

The pipeline follows that classic three-stage approach:

1. **Indexing**: Upload a document, extract text, chunk it into overlapping sentences, generate embeddings, store in memory
2. **Retrieval**: Ask a question, embed the query, calculate cosine similarity with all stored chunks, return top-k matches
3. **Generation**: Feed the retrieved context to Llama3 via Ollama and get an answer with proper citations

The whole thing runs locally using Ollama, which means no API keys, no usage limits.

### The Surprising Parts

A few things caught me off guard:

- **Python came back faster than expected**: Turns out it's like riding a bicycle, just with more indentation
- **Sentence-based chunking works better than expected**: More natural breaks than character-based chunking
- **In-memory search is plenty fast**: Even with hundreds of chunks, cosine similarity calculation is near-instantaneous
- **Ollama is genuinely impressive**: Local LLM serving that actually works without a PhD in infrastructure
- **The citations work properly**: The system actually tells you which document and chunk each answer comes from
- **Embedding quality matters more than I thought**: The choice of sentence transformer model significantly impacts retrieval quality

### What's Next

Now that I have a working Simple RAG system, the real fun begins. The roadmap includes:

- **Persistent storage**: Moving to a proper vector database (FAISS, Chroma, or similar)
- **Support for more file types**: DOCX, Markdown (and OCR ?)
- **Conversation**: Multi-turn conversation memory
- **Better RAG**: Maybe exploring Graph RAG or Hybrid RAG approaches

But for now, I'm going to enjoy the rare feeling of having built something that works on the first major attempt. It won't last long, but I'll take the win.

[Here is a link to the repository](https://github.com/esrmnt/local-ref-chat)