
## 📖 Overview

Most modern search engines are **English-centric**. If you search for "Brave" in a digital library of Sanskrit texts, you get zero results because the text says *Veera*.

This project solves the **"Language Barrier" in Heritage Search**. It builds an end-to-end semantic search pipeline that ingests static PDFs (like the *Subramanya Bhujangam*), creates a vector knowledge base, and allows users to query in their native language to find the correct verse—searching by **meaning**, not just keywords.

## 🚀 Key Features

* **True Polyglot Search:** Query in **English**, **Hindi**, **Sanskrit**, or **Tamil**. The engine understands that "Grace" = "Kripa" = "Arul".
* **Vector-First Architecture:** Uses `paraphrase-multilingual-MiniLM-L12-v2` to map concepts across languages into a shared vector space.
* **Context-Aware Chunking:** Implements a **Sliding Window** strategy to ensure poetry verses aren't cut in half, preserving semantic integrity.
* **Layout-Preserving Extraction:** Uses `pdfplumber` to accurately extract complex Indic scripts (Devanagari) without "mojibake" (encoding errors).
* **100% Local & Private:** Built on **ChromaDB**, running entirely on your local machine or a Kaggle notebook without needing cloud APIs.

## 🛠️ Tech Stack

* **Ingestion:** `pdfplumber` (PDF Text Extraction)
* **Embeddings:** `sentence-transformers` (Hugging Face)
* **Vector Database:** `chromadb` (Local Vector Store)
* **Language:** Python 3.x
## 🧠 How It Works

1. **Ingestion:** The PDF is parsed using `pdfplumber` to handle complex Devanagari font renderings.
2. **Sliding Window Chunking:** We split text into 1000-character blocks with a 200-character overlap. This ensures that if a verse is split at the end of one chunk, it appears fully intact in the next.
3. **Vectorization:** The `paraphrase-multilingual-MiniLM-L12-v2` model converts text into vectors. It is "aligned," meaning the vector for *Agni* (Sanskrit) and *Fire* (English) are mathematically close.
4. **Retrieval:** ChromaDB performs a **Cosine Similarity** search to find the nearest neighbor to your query vector.


## 🔮 Future Work

* **Parent-Child Retrieval:** Indexing small English summaries for better precision, but returning the full Sanskrit Verse (Parent) for better context.
* **LLM Integration:** Adding Llama 3 or Gemma to "explain" the retrieved verse in natural language.
* **OCR Support:** Adding Tesseract to handle scanned image PDFs.

