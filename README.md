
# Building a RAG System with **LangChain + Gemini**

*Notebook: **`Building a RAG system using Langchain and Gemini.ipynb`***  
*Session date: 9 May 2025*

This repository accompanies an interactive workshop that walks through building a **Retrieval‑Augmented Generation (RAG)** pipeline powered by **Google Gemini** and **LangChain**.  
The entire demo lives in a single Jupyter/Colab notebook so you can **run it end‑to‑end** with zero boilerplate.

---

## 🗂️ What’s inside?

| Path | Purpose |
|------|---------|
| `Building a RAG system using Langchain and Gemini.ipynb` | Step‑by‑step notebook with code cells and mini‑tasks |
| `README.md` | ← you are here |

---

## 🚀 Quick‑start

### Option 1 — Google Colab (easiest)

1. Upload the notebook to Colab or click **“Open in Colab”** from GitHub.  
2. In the first code cell, paste your **Gemini API key** when prompted.  
   ```python
   import os
   os.environ["GOOGLE_API_KEY"] = "yah‑ai‑key"
   ```  
3. Run the notebook top‑to‑bottom ▶️.

### Option 2 — Local Jupyter

```bash
# Clone & enter
git clone https://github.com/<your‑handle>/gemini‑rag‑demo.git
cd gemini‑rag‑demo

# Create a virtual env (optional but tidy)
python -m venv .venv && source .venv/bin/activate

# Install requirements
pip install -r requirements.txt      # see list below

# Export your key (fish / PowerShell syntax will differ)
export GOOGLE_API_KEY="yah‑ai‑key"

# Launch Jupyter
jupyter lab  Building\ a\ RAG\ system\ using\ Langchain\ and\ Gemini.ipynb
```

### Minimal `requirements.txt`

```
langchain>=0.1
langchain-community
langchain-core
langchain-google-genai
chromadb
google-generativeai     # pulled in by langchain‑google‑genai
beautifulsoup4          # HTML parsing for WebBaseLoader
tiktoken                # token counting utilities
```

---

## 🛠️ How the notebook builds RAG

| Stage | LangChain component | What happens |
|-------|--------------------|--------------|
| **Load docs** | `WebBaseLoader` + **BeautifulSoup** | Scrapes an article on AI agents |
| **Split text** | `RecursiveCharacterTextSplitter` | Keeps chunks < 1 k tokens |
| **Embed** | `GoogleGenerativeAIEmbeddings` (`embedding‑001`) | Turns chunks → vectors |
| **Index** | **Chroma** | Stores vectors on disk (`./chroma_db`) |
| **Retrieve** | `VectorStoreRetriever` | Cosine‑similar top‑*k* search |
| **Generate** | `ChatGoogleGenerativeAI` (`gemini‑2.0‑flash`) | LLM answers with retrieved context |
| **Prompt** | LangChain Hub *“rag‑prompt”* | Standard Q‑A template |

---

## 🎓 Mini‑tasks inside the notebook

| Task | Skill |
|------|-------|
| **Task 1** – Install packages & set API keys | Setup |
| **Task 2** – Inspect document chunks | Text splitting |
| **Task 3** – Print retrieved docs & their count | Retrieval debugging |
| **Task 4** – Make *k* configurable instead of fixed | Vector‑store tuning |
| **Task 5** – Explain what the *temperature* parameter does | LLM prompting |

Feel free to delete or adapt these challenge cells when you turn the demo into production code.

---

## 🔄 Customisation ideas

* **Swap Gemini for GPT‑4/Together/Anthropic** – just change the `Chat*` & `Embeddings` classes.  
* **Try another vector DB** – FAISS, Pinecone, or Supabase all work via LangChain.  
* **Chunk smarter** – use `TokenTextSplitter` or semantic chunking for long PDFs.  
* **Add a UI** – wrap the `rag_chain` in Streamlit or Gradio for a chat experience.

---

## 🐞 Troubleshooting

| Problem | Fix |
|---------|-----|
| `google.generativeai.types.APIKeyError` | `GOOGLE_API_KEY` missing or incorrect |
| No module named `chromadb` | `pip install chromadb` |
| Output hallucinations | Increase *k*, give more relevant docs, or adjust prompt |

---

## 📄 License

MIT – free to use, modify, and distribute with attribution.

---

_README generated automatically on 2025-05-09._
