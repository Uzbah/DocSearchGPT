# DocSearchGPT

This project demonstrates how to build a document search and response generation system using **Sentence Transformers** for embedding-based search and **GPT-based models** for generating responses. The system allows users to upload a document (in `.txt` or `.pdf` format), search for relevant content within the document, and generate responses to user queries using a fine-tuned GPT model.

---

## Table of Contents
1. [Overview](#overview)
2. [Features](#features)
3. [Installation](#installation)
4. [Usage](#usage)
5. [How It Works](#how-it-works)
6. [Future Work](#future-work)
---

## Overview

This project combines **embedding-based search** and **GPT-based response generation** to create a system that can:
1. **Search for relevant content** within a document using semantic similarity.
2. **Generate responses** to user queries based on the retrieved content.

The system is designed to work with both `.txt` and `.pdf` files, making it versatile for various types of documents.

---

## Features

- **Document Loading**: Supports `.txt` and `.pdf` files for document input.
- **Embedding-Based Search**: Uses **Sentence Transformers** to generate embeddings for document chunks and queries, enabling semantic search.
- **Response Generation**: Utilizes a **GPT-based model** to generate responses based on the retrieved content.
- **Interactive Query Interface**: Allows users to input queries and receive relevant responses in real-time.
- **Fine-Tuning Support**: Provides a framework for fine-tuning GPT models on custom datasets.

---

## Installation

To run this project, you need to install the required Python libraries. You can do this using pip:

```bash
pip install sentence-transformers PyPDF2 transformers torch
```

### Additional Dependencies
- **GPU Support**: For faster processing, ensure you have a GPU-enabled environment (e.g., Google Colab or a local machine with CUDA).

---

## Usage

### 1. **Install Required Libraries**
```bash
pip install sentence-transformers PyPDF2 transformers torch
```

### 2. **Load the Document**
The system supports `.txt` and `.pdf` files. You can load a document using the `load_corpus` function:

```python
corpus, doc_names = load_corpus("path/to/your/document.pdf")
```

### 3. **Initialize Embedding Search**
The `EmbeddingSearch` class is used to generate embeddings for the document and perform semantic search:

```python
embed_search = EmbeddingSearch(model_name="all-MiniLM-L6-v2")
embed_search.fit(corpus)
```

### 4. **Search for Relevant Content**
You can search for relevant content in the document using a query:

```python
query = "What is Machine Learning?"
relevant_docs = embed_search.search(query, top_k=3)
```

### 5. **Generate Responses**
The system uses a GPT-based model to generate responses based on the retrieved content:

```python
response = generate_response(gpt_pipeline, query, relevant_docs)
print(response)
```

### 6. **Interactive Query Interface**
Run the script to interactively query the document:

```bash
python document_search.py
```

---

## How It Works

1. **Document Loading**:
   - The system loads the document and splits it into chunks for processing.
   - For `.pdf` files, it extracts text using `PyPDF2`.

2. **Embedding-Based Search**:
   - The document chunks are encoded into embeddings using a **Sentence Transformer** model.
   - User queries are also encoded, and cosine similarity is used to find the most relevant chunks.

3. **Response Generation**:
   - The retrieved document chunks are passed to a **GPT-based model** (e.g., GPT-2) to generate a response.
   - The model is fine-tuned to ensure accurate and context-aware responses.

4. **Interactive Query Interface**:
   - Users can input queries, and the system will return relevant content and generate responses in real-time.

---

## Future Work

- **Support for More File Formats**: Extend the system to support additional file formats like `.docx` and `.html`.
- **Improved Fine-Tuning**: Implement fine-tuning on custom datasets to improve response quality.
- **Multi-Document Search**: Enable searching across multiple documents simultaneously.
- **User Interface**: Develop a web-based or desktop interface for easier interaction.
