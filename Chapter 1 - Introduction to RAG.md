# 📘 **Chapter 1 — Introduction to RAG (Retrieval-Augmented Generation)**

*A simple, practical walkthrough of the fundamental RAG pipeline*

---

# ⭐ What You Will Learn

In this chapter, we will build a **minimal but complete RAG system** using only the essentials.
You will understand the *core ideas* that every RAG architecture—simple or advanced—is built on.

We cover these steps:

1. **Load the document**
2. **Split it into chunks**
3. **Create and store embeddings**
4. **Retrieve relevant context**
5. **Generate answers from the context**
6. **Evaluate the output**

This chapter forms the foundation for everything that follows in the book.

---

[Notebook](https://colab.research.google.com/drive/1FnJSAC1Mrj62DpAwk2_pj0oL-vrOAHXi?usp=sharing)
# 🧩 **What is RAG?**

**Retrieval-Augmented Generation (RAG)** is a technique where an LLM answers questions using information retrieved from an external knowledge source.

Unlike a normal LLM (which “guesses” from its training data), a RAG system:

* Reads your documents
* Converts them into searchable vectors
* Retrieves the best matching pieces
* Uses them to ground the LLM's answer

This makes answers *accurate*, *context-aware*, and *verifiable*.

---

# 🧱 **RAG Architecture — The Essential Blocks**

Here are the four essential components of a RAG system:

## 1. **Document Loader**

Reads PDFs, text files, HTML pages, etc.

## 2. **Text Splitter**

Breaks large documents into manageable chunks.

## 3. **Embeddings + Vector Store**

Converts text into vectors and indexes them for similarity search.

## 4. **Retriever + LLM**

Finds relevant chunks and generates grounded answers.

We’ll implement each step now.

---

# 🛠️ **Step-by-Step Implementation**

---

# 🔹 **Step 1 — Read the Document**

```python
from langchain_community.document_loaders import PyPDFLoader

loader = PyPDFLoader("my-document.pdf")
documents = loader.load()

print("Pages loaded:", len(documents))
```

PDF files are loaded **page-by-page**.

---

# 🔹 **Step 2 — Create Chunks**

Breaking into chunks helps embeddings capture meaning and ensures retrieval is accurate.

```python
from langchain_text_splitters import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200
)

chunks = splitter.split_documents(documents)

print("Chunks created:", len(chunks))
```

* **chunk_size** controls the size of text blocks
* **chunk_overlap** preserves continuity between chunks

---

# 🔹 **Step 3 — Create Embeddings + Vector Store**

We embed each chunk using a text embedding model.

```python
from langchain_community.embeddings import DeepInfraEmbeddings
from langchain_community.vectorstores import FAISS

embeddings = DeepInfraEmbeddings(
    model_id="BAAI/bge-base-en-v1.5"
)

vectorstore = FAISS.from_documents(chunks, embeddings)
retriever = vectorstore.as_retriever(search_kwargs={"k": 3})
```

This step creates a **FAISS index** so similar chunks can be retrieved instantly.

---

# 🔹 **Step 4 — Ask Questions (RAG Inference)**

To answer a question, we:

1. Retrieve relevant chunks
2. Feed them + the question to the LLM

```python
from langchain_community.chat_models.deepinfra import ChatDeepInfra
from langchain.prompts import PromptTemplate

llm = ChatDeepInfra(
    model_id="mistralai/Mistral-7B-Instruct-v0.2",
    temperature=0.2
)

answer_prompt = PromptTemplate.from_template("""
Use ONLY the context below to answer the question.

Context:
{context}

Question: {question}

Answer:
""")

answer_chain = answer_prompt | llm

question = "What is the main idea of this document?"

# 1) Retrieve context
context_docs = retriever.get_relevant_documents(question)
context_text = "\n\n".join(doc.page_content for doc in context_docs)

# 2) Generate answer
answer = answer_chain.invoke({
    "context": context_text,
    "question": question
})["output_text"]

print(answer)
```

This creates a **grounded answer**, not a hallucinated one.

---

# 🔹 **Step 5 — Evaluate the Answer**

Evaluation checks:

* **Relevance** (Did the answer address the question?)
* **Completeness** (Is it detailed and accurate?)
* **Faithfulness** (Is it grounded in context, not hallucinated?)

```python
eval_prompt = PromptTemplate.from_template("""
Evaluate the QA pair from 1–5 in JSON.

Question: {question}
Answer: {answer}

Context:
{context}

Return JSON:
{"Relevance": x, "Completeness": y, "Faithfulness": z}
""")

eval_chain = eval_prompt | llm

evaluation = eval_chain.invoke({
    "question": question,
    "answer": answer,
    "context": context_text[:2000]
})["output_text"]

print(evaluation)
```

This ensures your system is not just *working*, but *performing well*.

---

# 🎉 **Summary - What You Built**

By completing Chapter 1, you have built a fully functional **local RAG pipeline**:

| Step        | What You Did                        |
| ----------- | ----------------------------------- |
| 📄 Load     | Loaded a PDF                        |
| ✂ Split     | Converted pages → chunks            |
| 🔡 Embed    | Created embeddings with DeepInfra   |
| 🔎 Retrieve | Built a FAISS index                 |
| 🤖 Generate | Got LLM answers grounded in context |
| 🧪 Evaluate | Scored relevance + accuracy         |

This builds the foundation for more advanced chapters:

* multi-vector RAG
* rerankers
* chunking strategies
* agents + tools
* caching + optimization
* evaluation frameworks
* retrieval pipelines
* hybrid search
* query transformation

