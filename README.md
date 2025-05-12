## 🧠 RAG-Powered Multi-Agent Q\&A Assistant

This project is a minimal, modular **Retrieval-Augmented Generation (RAG)** system with simple **multi-agent logic**. It can:

* 🗃️ Ingest and search from uploaded `.txt` files (RAG)
* 🤖 Answer natural-language questions using an LLM
* 🔀 Route certain queries to specialized tools:

  * Calculator for math
  * Dictionary for word definitions (via API)

---

### 📌 Features

* ✅ RAG: Retrieve relevant document chunks based on your query
* 🤖 LLM: Generate answers using context from retrieved chunks
* 🧠 Agent Logic: Decide whether to:

  * Use calculator for math expressions
  * Use dictionary API for definitions
  * Or default to document-based Q\&A (RAG)

---

### 📂 File Upload Flow

You can upload your own `.txt` files. The assistant reads and chunks these files for semantic search using vector embeddings (via FAISS).

---

### 🛠️ How to Run (in Google Colab)

1. Open the Colab notebook.
2. Run all setup cells.
3. Upload your `.txt` files when prompted.
4. Ask questions like:

   * `"What is your return policy?"`
   * `"Define intelligence"`
   * `"2 + 2 * 3"`

---

### 🧠 Agent Routing Logic

| Keyword(s) in Query             | Routed To            |
| ------------------------------- | -------------------- |
| `calculate`, `+`, `-`, `*`, `/` | Calculator Tool      |
| `define`, `meaning of`          | Dictionary API       |
| Otherwise                       | RAG (retrieve + LLM) |

---

### 📚 Tools & Libraries Used

* [LangChain](https://python.langchain.com/)
* [FAISS](https://github.com/facebookresearch/faiss)
* [HuggingFace Transformers](https://huggingface.co/)
* [Free Dictionary API](https://dictionaryapi.dev/)
* `requests`, `re`, `eval`, and basic Python tools

---

### 📝 Architecture Diagram (Textual)

```
           +---------------------+
           |   User Query Input  |
           +---------+-----------+
                     |
             [route_query()]
                     |
     +---------------+------------------+
     |               |                  |
"Calculator"   "Dictionary"         "RAG Pipeline"
     |               |                  |
[eval(expr)]   [API call]      [Retrieve + LLM Answer]
```

---

### 🚀 Example Queries

```bash
> Ask: what is return policy
Routing: rag
Answer: [LLM output based on retrieved context]

> Ask: 12 * 9 + 3
Routing: calculator
Answer: 111

> Ask: define artificial intelligence
Routing: dictionary
Answer: Artificial Intelligence: The ability to acquire and apply knowledge and skills.
```

---

### 📎 Notes

* LLM used: `HuggingFacePipeline` (based on `google/flan-t5-base`)
* Retrieval uses dense vector similarity via FAISS
* Dictionary uses `https://api.dictionaryapi.dev/`

