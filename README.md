# RAG-BluePrint  
### A Practical Notebook-Based Handbook for Building Retrieval-Augmented Generation Systems

**RAG-BluePrint** is designed as a **mini-book** in the form of 10 curated Jupyter notebooks.  
Each notebook focuses on one core component of the Retrieval-Augmented Generation (RAG) pipeline — with clean explanations and minimal, meaningful, **fully runnable** code.

No heavy frameworks.  
No over-engineering.  
Just the essential building blocks of modern RAG systems, presented clearly and practically.

---

## 🧭 Blueprint Overview  
RAG is an architecture for grounding LLM outputs using **external knowledge**.

This handbook walks through each stage of the pipeline:

1. **Data Loading** – reading and extracting clean text from PDFs, TXT, CSV  
2. **Chunking** – splitting documents into retrieval-friendly units  
3. **Embeddings** – converting text into vector representations  
4. **Vector Storage** – indexing embeddings for efficient search  
5. **Retrieval** – fetching the most relevant chunks  
6. **Reranking** – improving retrieval precision  
7. **Generation** – constructing a final answer using retrieved context  
8. **Evaluation** – checking retrieval accuracy and grounding quality  

Each stage is covered in a standalone notebook with examples and experiments.

---

## 📘 Table of Contents (Notebook Chapters)

```
01 – Introduction to RAG
02 – Loading & Preparing Your Data
03 – Chunking Strategies
04 – Embeddings: Concepts & Implementation
05 – Building a Vector Store with Chroma
06 – Basic Retrieval Techniques
07 – Your First RAG Pipeline
08 – Adding Rerankers
09 – Evaluating RAG (RAGAS)
10 – End-to-End RAG Pipeline (Blueprint)
```

Each notebook includes:

- A clear written explanation  
- Flow diagrams (simple ASCII-style where helpful)  
- Clean, reproducible code  
- Real output examples  
- A short summary  
- Optional exercises to reinforce understanding  

No clutter. No unnecessary visuals.

---

## 🎛️ Running the Blueprint  
Clone and start:

```bash
git clone https://github.com/arorarishi/RAG-BluePrint
cd RAG-BluePrint
pip install -r requirements.txt
jupyter lab
```

Runs entirely on **CPU**.  
**No GPU required.**  
**No API key required** unless you choose to enable LLM calling via OpenAI / Gemini / Mistral / DeepInfra.

---

## 📦 Requirements

- Python 3.9+  
- jupyterlab  
- sentence-transformers  
- chromadb  
- pandas  
- nltk  
- scikit-learn  
- ragas (optional, for evaluation)  

All notebooks use **small example datasets** kept inside `/assets` for easy reproducibility.

---

## 🧩 Why This Blueprint Exists  
Most RAG content online is either:

- **Too shallow** — tiny examples that teach nothing, or  
- **Too abstract** — enterprise frameworks hiding all the core logic  

**RAG-BluePrint fills the missing middle:**  
A clear, structured, low-level, notebook-driven handbook that teaches  
*exactly how RAG works under the hood.*

You will implement every part manually — chunking, embeddings, vector search, reranking, and evaluation — using only essential libraries.

This builds **true understanding**, not dependency on frameworks.

---

## 📝 Author’s Note  
This project is actively maintained.  
Advanced topics (HyDE, CRAG, RAPTOR, Agentic RAG, etc.) will be introduced in a **separate companion repository** once the Blueprint foundations are complete.

---

## 📄 License  
MIT License

---

## 🤝 Contributions  
Suggestions and educational improvements are welcome.  
Feel free to open issues or submit pull requests.
