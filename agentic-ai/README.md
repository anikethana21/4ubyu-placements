# 🤖 Agentic AI & LangGraph — Dual-Track Interactive Engineering Masterclass

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue?style=flat&logo=python&logoColor=white)](https://www.python.org/)
[![LangChain](https://img.shields.io/badge/LangChain-v0.2%2B-green?style=flat)](https://www.langchain.com/)
[![LangGraph](https://img.shields.io/badge/LangGraph-v0.1%2B-purple?style=flat)](https://langchain-ai.github.io/langgraph/)
[![No Dependencies](https://img.shields.io/badge/web_dependencies-zero-brightgreen?style=flat)](.)
[![License: MIT](https://img.shields.io/badge/License-MIT-purple?style=flat)](LICENSE)

> **The definitive dual-track engineering handbook and interactive application suite for Agentic AI, RAG Systems, LangChain LCEL, and LangGraph Orchestration.**

---

## 🎯 What Is This?

A **production-grade, dual-track learning hub** built with lightweight, dependency-free vanilla web technologies. It provides exhaustive theoretical depth, mathematical derivations, numerical examples, interactive simulations, and **complete, unabridged Python production source code** for 8 real-world AI projects.

### Dual-Track Architecture

| Application | Scope & Modules | Core Highlights |
|---|---|---|
| **[index.html](index.html)** | **Central Portal Hub** | Dual-track navigation, architectural comparison matrix (LangChain vs LangGraph), and 8-project catalog. |
| **[langchain.html](langchain.html)** | **Track 1: LangChain & RAG Engineering** | 4 Eras of Software, LLM Anatomy, Softmax Temperature Simulator, Prompting Schema, LCEL, 5 Pillars of RAG, Cosine Vector Lab, Chroma/FAISS, MMR λ Explorer, Function Calling, ReAct Finite State Machine, Project 1 (Multi-Agent Research Pipeline), Project 2 (Video Assistant with `.pkl` Caching), and the 6-Step Blueprint. |
| **[langgraph.html](langgraph.html)** | **Track 2: LangGraph Orchestration** | State Modeling (`states.py` TypedDict vs Pydantic), all 6 course projects with full production code (`sequential_base.py`, `parallel_reducers.py`, `conditional_RAG.py`, `iterative_tools.py`, `humanintheloop.py`, `app.py` Streamlit UI), Annotated Reducers, HITL `interrupt()` & `Command`, and LangSmith tracing. |

---

## 🛠️ Tech Stack & Design Philosophy

| Layer | Technology | Architectural Rationale |
|---|---|---|
| **Web Frontend** | HTML5 + Vanilla CSS3 + ES6+ JavaScript | Zero external node_modules bloat, zero build steps, instant sub-millisecond local loading. |
| **Styling & Theme** | Modern Glassmorphism & Sleek Dark Mode | Curated HSL color palette, typography via *Plus Jakarta Sans* and *JetBrains Mono*. |
| **Simulations** | HTML5 Canvas API + Dynamic JS DOM | Real-time mathematical simulation of Softmax temperature, 2D vector angles, and ReAct execution loops. |
| **AI Frameworks** | LangChain Core, LCEL, LangGraph | State-of-the-art declarative pipelines and cyclic multi-agent graph orchestration. |
| **Vector Indexing** | ChromaDB, FAISS, OpenAI Embeddings | High-dimensional geometric semantic search with sub-second nearest-neighbor retrieval. |
| **Caching Engine** | Python `pickle` (`.pkl`) Serialization | 1,500×–2,500× faster cold starts and $0 redundant API re-run expenses. |

---

## 📁 Repository Structure

```
langchain-langgraph-course/
├── index.html          # Gateway portal: dual-track navigation & comparison matrix
├── langchain.html      # Track 1: Complete LangChain, RAG & Single-Agent Handbook
├── langgraph.html      # Track 2: Complete LangGraph & Multi-Agent Engineering Manual
├── README.md           # Comprehensive project documentation
└── LICENSE             # MIT License
```

---

## 🚀 How to Run the Web Applications

### Option 1 — Direct File Access (No Installation Required)
Double-click `index.html`, `langchain.html`, or `langgraph.html` in your file explorer to open immediately in any modern web browser (Chrome, Edge, Firefox, Safari).

### Option 2 — Local Development Server
Serve via Python's built-in HTTP server:
```bash
# From within the repository directory:
python -m http.server 3000
```
Then navigate to `http://localhost:3000` in your browser.

Or using Node.js:
```bash
npx serve .
```

---

## 📚 Complete Project Catalog

This repository contains the complete architectural blueprints and unabridged production code for **8 projects**:

### LangGraph Orchestration Projects (`langgraph.html`)
1. **P1: Sequential Video Content Pipeline (`sequential_base.py`)**  
   Linear hand-off where each node processes the previous node's output: Raw Text $\rightarrow$ Copyeditor $\rightarrow$ Video Scriptwriter Hook $\rightarrow$ Hinglish Translator.
2. **P2: Multi-Branch Content Safety Analyzer (`parallel_reducers.py`)**  
   Parallel fan-out from START to Toxicity, Copyright, and Regional Culture nodes. Employs `Annotated[dict, merge_score_dicts]` to eliminate the "last-writer-wins" data overwrite bug.
3. **P3: College Assistant with Multi-PDF RAG (`conditional_RAG.py`)**  
   Dynamic LLM query classification routing requests to specialist FAISS retrievers across academic, fee, placement, and exam policies.
4. **P4: LinkedIn Post Generator (`iterative_tools.py`)**  
   Generator-Critic reflection loop with live Tavily web search tools. Evaluates drafts against 7 strict criteria with an automatic recursion cap (`score >= 8.5` or `iterations >= 3`).
5. **P5: Human-in-the-Loop Approval Gate (`humanintheloop.py`)**  
   Mission-critical human oversight using `interrupt()`, `MemorySaver` thread checkpointing, and graph resumption via `Command(resume=...)`.
6. **P6: Enterprise Streamlit Web Portal (`app.py`)**  
   Full-featured web application with cached resource ingestion (`@st.cache_resource`), custom CSS badges, sidebar program selector, and live streaming chat.

### LangChain & RAG Engineering Projects (`langchain.html`)
7. **P7: Multi-Agent Research Pipeline (`project_1_multi_agent_research/`)**  
   Specialist Search, Read, and Writer agents coordinated with Tavily web search, BeautifulSoup scraping, and persistent `.pkl` search caching.
8. **P8: AI Video Assistant with `.pkl` Caching Engine (`project_2_video_rag_assistant/`)**  
   YouTube transcript extraction, timecode preservation, semantic chunking, and 2,500× faster cold-start vector search via serialized binary indices.

---

## 📐 Mathematical Foundations

The applications mathematically illustrate four foundational formulas:

```
1. SOFTMAX WITH TEMPERATURE SCALING:
   P(wᵢ) = exp(zᵢ / T) / ∑ exp(zⱼ / T)

2. VECTOR COSINE SIMILARITY:
   CosineSim(A, B) = (A · B) / ( ||A|| × ||B|| )

3. MAXIMAL MARGINAL RELEVANCE (MMR):
   MMR = argmax [ λ · Sim₁(dᵢ, q) - (1 - λ) · max Sim₂(dᵢ, dⱼ) ]

4. THE COGNITIVE REACT LOOP:
   Input ──> ( Thought ──> Action ──> Observation )* ──> Final Answer
```

---

## 📄 License

Distributed under the **MIT License**. Free for educational, research, and commercial reference.
