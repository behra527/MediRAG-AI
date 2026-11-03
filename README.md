# MediRAG AI

> Clinical Guideline Intelligence Platform

Ask questions about clinical guideline PDFs with retrieval-augmented generation, inspect evidence, and compare PDF parsers.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.100%2B-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-5.0-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![ChromaDB](https://img.shields.io/badge/VectorDB-ChromaDB-purple?style=for-the-badge)
![OpenRouter](https://img.shields.io/badge/LLM-OpenRouter-orange?style=for-the-badge)
![License](https://img.shields.io/badge/License-Unlicensed-lightgrey?style=for-the-badge)

---

> **IMPORTANT:** Research and educational use only. MediRAG AI is not a medical device and does not replace qualified clinical judgment. Always verify answers against original guideline documents.

---

## Overview

MediRAG AI is a full-stack application for exploring clinical guideline documents. It uses Retrieval-Augmented Generation (RAG) to retrieve relevant PDF passages before generating an answer, with a focus on traceability and understanding hallucinations.

The project also includes PDF text extraction and cleaning, plus a two-parser comparison workflow using PyMuPDF and pdfplumber to investigate common extraction issues.

---

## Features

- **Clinical PDF Upload:** Ingest searchable guideline documents.
- **Semantic Retrieval:** Chunk content, create embeddings with Sentence Transformers, and search with ChromaDB.
- **Evidence-Grounded Q&A:** Use retrieved passages as context for OpenRouter-hosted models.
- **Source References:** Display retrieved evidence when available.
- **RAG vs. Baseline Comparison:** Contrast grounded and ungrounded responses.
- **PDF Parser Comparison:** Compare PyMuPDF and pdfplumber output.
- **Text Cleaning:** Investigate repeated headers and footers, page numbers, line wraps, hyphenation, multi-column reading order, and tables.
- **React Dashboard:** Upload, manage, and query documents.

> **Verification Note:** Backend `/api/health` returned HTTP 200 with the expected CORS header during local testing. Full PDF indexing, live LLM generation, frontend build, and parser-quality evaluation have not yet been independently verified end to end.

---

## Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | React, Vite, Lucide React |
| **Backend** | Python, FastAPI, Uvicorn |
| **PDF Parsing** | PyMuPDF, pdfplumber |
| **Embeddings** | Sentence Transformers |
| **Vector Database** | ChromaDB |
| **LLM** | OpenRouter *(configurable model; example: `openai/gpt-4o-mini`)* |
| **Testing** | pytest |

---

## Architecture

```mermaid
flowchart TD
    A[React / Vite UI] --> B[FastAPI Backend]
    B --> C[PDF Upload & Extraction]
    C --> D[Text Cleaning & Chunking]
    D --> E[Sentence Transformers]
    E --> F[(ChromaDB)]
    A --> G[User Question]
    G --> B
    B --> H[Semantic Retrieval]
    F --> H
    H --> I[OpenRouter LLM]
    I --> J[Answer + Retrieved Evidence]
    J --> A
    C --> K[PyMuPDF vs pdfplumber Comparison]
