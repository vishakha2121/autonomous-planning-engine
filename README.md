# 🚀 Autonomous Planning Engine

> **Turn vague enterprise goals into executed outcomes — automatically.**

![Python](https://img.shields.io/badge/Python-3.11-blue?style=flat-square&logo=python)
![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=flat-square&logo=fastapi)
![React](https://img.shields.io/badge/React-18-61dafb?style=flat-square&logo=react)
![LangGraph](https://img.shields.io/badge/LangGraph-latest-orange?style=flat-square)
![Gemini](https://img.shields.io/badge/Gemini-API-4285F4?style=flat-square&logo=google)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)
![Status](https://img.shields.io/badge/Status-Practice%20Project-purple?style=flat-square)

An autonomous AI planning engine that takes a high-level organizational goal 
(e.g., *"Increase Q1 revenue by 40%"*) and breaks it down into a structured, 
executable task graph — then assigns each task to a specialized AI agent, 
monitors execution in real time, and intelligently replans when something fails.

Built as a **practice / learning project** to explore how modern agentic 
systems combine **HTN Planning**, **LangGraph orchestration**, 
**Model Context Protocol (MCP)**, and **Vector Memory** into one coherent engine.

---

## 📌 Table of Contents

- [What It Does](#-what-it-does)
- [Core Concepts](#-core-concepts)
- [Architecture](#-architecture)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Database Schema](#-database-schema)
- [Getting Started](#-getting-started)
- [API Endpoints](#-api-endpoints)
- [Screenshots](#-screenshots)
- [Roadmap](#-roadmap)
- [Disclaimer](#-disclaimer)
- [License](#-license)

---

## 🎯 What It Does

| Step | Action |
|------|--------|
| 1️⃣ | User submits a high-level enterprise goal |
| 2️⃣ | **HTN Planner** decomposes it into a hierarchical task network |
| 3️⃣ | **LangGraph** orchestrates specialized agents (Marketing, Finance, HR, Eng…) |
| 4️⃣ | Agents execute tasks using tools exposed via **MCP** |
| 5️⃣ | A **Monitor** node tracks progress and detects failures |
| 6️⃣ | A **Replanner** node dynamically adapts the plan |
| 7️⃣ | Every execution is stored in **Vector Memory** for future learning |
| 8️⃣ | A live **React dashboard** shows the entire flow in real time |

---

## 🧠 Core Concepts

| Concept | Description |
|---------|-------------|
| **HTN Planning** | Hierarchical Task Network for goal decomposition into primitive + compound tasks |
| **LangGraph** | Stateful multi-agent workflow with conditional routing and checkpointing |
| **MCP (Model Context Protocol)** | Standardized interface connecting LLMs to external tools (files, DB, calendar, email) |
| **Vector Memory** | Episodic + semantic memory stored in ChromaDB for retrieval-augmented reasoning |
| **Gemini API** | LLM backbone for planning, execution, and embeddings — **CPU-friendly**, no GPU required |
| **FastAPI + SQLite** | Lightweight, production-style backend with clean architecture |
| **React + Tailwind** | Modern, animated, dark-mode dashboard with live WebSocket updates |

---

## 🏗️ Architecture



---

## 🛠️ Tech Stack

### Backend
- **Python 3.11+**
- **FastAPI** — REST API framework
- **Uvicorn** — ASGI server
- **SQLAlchemy 2.0** — ORM
- **SQLite** — Database (practice-friendly)
- **Pydantic v2** — Data validation
- **LangChain** + **LangGraph** — Agent orchestration
- **ChromaDB** — Vector store
- **Google Generative AI SDK** — Gemini API client
- **WebSockets** — Live updates
- **Alembic** — DB migrations

### Frontend
- **React 18** + **Vite**
- **TailwindCSS** — Styling
- **Zustand** — State management
- **React Router v6** — Routing
- **React Flow** — Task graph visualization
- **Framer Motion** — Animations
- **Recharts** — Charts
- **Axios** — HTTP client
- **Lucide React** — Icons
- **React Hot Toast** — Notifications

### AI / Agent Layer
- **HTN Planner** — Custom implementation
- **LangGraph Nodes** — Planner, Router, Executor, Monitor, Replanner
- **MCP Client/Server** — Tool interface
- **Gemini Embeddings** — `text-embedding-004`

### DevOps
- **Docker Compose** — Local dev
- **GitHub Actions** — CI pipeline

---

## 📁 Project Structure



---

## 🗄️ Database Schema

| Table | Purpose |
|-------|---------|
| `goals` | High-level organizational objectives |
| `plans` | HTN-generated plans (versioned per goal) |
| `tasks` | Individual tasks (hierarchical, with `parent_task_id`) |
| `task_dependencies` | DAG edges — task A must finish before B |
| `agents` | Specialized agent definitions + capabilities |
| `executions` | Execution record per task (input, output, status, duration) |
| `execution_logs` | Step-by-step logs for each execution |
| `memory_entries` | Vector memory (embedding_id, content, type) |
| `audit_logs` | Who did what, when |
| `metrics` | Performance + success metrics |

---

## 🚀 Getting Started

### Prerequisites
- **Python 3.11+**
- **Node.js 20+**
- **Git**
- **Gemini API key** → [Get one here](https://aistudio.google.com/apikey)

> ⚠️ **No GPU required!** This project runs entirely on CPU using the Gemini API 
> for all LLM and embedding operations.

### 1. Clone the Repository

```bash
git clone https://github.com/vishakha2121/autonomous-planning-engine.git
cd autonomous-planning-engine

cd backend

# Create virtual environment
python -m venv .venv

# Activate it
# Windows:
.venv\Scripts\activate
# Mac/Linux:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Setup environment variables
copy .env.example .env       # Windows
cp .env.example .env         # Mac/Linux

# Edit .env and add your GEMINI_API_KEY

# Initialize database
python scripts/init_db.py

# Seed sample data (optional)
python scripts/seed_db.py

# Run server
uvicorn main:app --reload --port 8000