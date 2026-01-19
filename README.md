# LangGraph Memory Tutorial

This repository contains a **hands-on set of Jupyter notebooks and supporting Python modules** focused on **Semantic, Episodic and procedural memory patterns in LangGraph**.  
The material is organized by lesson, and in addition to exploring long-term (semantic memory, episodic and procedural) memory patterns, demonstrates custom memory writers and memory-aware agents using **LangGraph** and **LangMem**.

The project targets **Python 3.13** and uses **uv exclusively** as the Python package manager and dependency resolver  
(`pyproject.toml` + `uv.lock`). No Conda is required or used.

---

## Quick Start

### Prerequisites
- Python **3.13+**
- [`uv`](https://docs.astral.sh/uv/) installed
- An OpenAI API key

### 1) Clone the repository
```bash
git clone https://github.com/markcberman/langgraph-memory-tutorial.git
cd langgraph-memory-tutorial
```

### 2) Create and sync the virtual environment
```bash
uv sync
```

This will:
- Create a local virtual environment (`.venv`)
- Install all pinned dependencies from `uv.lock`

### 3) Activate the environment
```bash
source .venv/bin/activate   # macOS / Linux
```

### 4) Launch Jupyter
```bash
jupyter lab
```

---

## Repository Structure

The repository is organized by lesson. Each lesson directory contains:
- A **primary Jupyter notebook** (the instructional material)
- Supporting Python modules used by the notebook:
  - `examples.py` — runnable LangGraph examples
  - `prompts.py` — prompt templates
  - `schemas.py` — typed state / data models
  - `utils.py` — shared helpers

```
.
├── L3/
│   ├── lesson_3.ipynb
│   ├── lesson_3_5_semantic_memory_custom_mem_writer.ipynb
│   ├── examples.py
│   ├── prompts.py
│   ├── schemas.py
│   └── utils.py
│
├── L4/
│   ├── lesson_4.ipynb
│   ├── examples.py
│   ├── prompts.py
│   ├── schemas.py
│   └── utils.py
│
├── L5/
│   ├── lesson_5.ipynb
│   ├── examples.py
│   ├── prompts.py
│   ├── schemas.py
│   └── utils.py
│
├── main.py
├── pyproject.toml
├── uv.lock
├── requirements.locked.txt
└── README.md
```

### Top-level files
- **`main.py`** — Optional entry point for running or experimenting with components outside of notebooks
- **`pyproject.toml`** — Project metadata and declared dependencies
- **`uv.lock`** — Fully resolved dependency lockfile (authoritative)
- **`requirements.locked.txt`** — Pip-compatible lockfile exported from `uv.lock` (optional / reference)
- **`README.md`** — Project documentation


---

## Memory Types Used in This Project

This tutorial draws inspiration from well-established cognitive science distinctions and maps them onto **LangGraph memory primitives**. Throughout the lessons, you will encounter three complementary forms of memory:

### Semantic Memory
**Semantic memory** represents *general knowledge* that is not tied to a specific moment in time.  
In agent systems, this typically corresponds to facts, preferences, profiles, or domain knowledge that should persist across many interactions.

**In this project:**
- Implemented using vector-backed memory via **LangMem**
- Queried based on semantic similarity
- Written explicitly using custom memory writers

**Typical use cases:**
- User preferences (tone, formatting, recurring instructions)
- Domain knowledge learned over time
- Long-lived facts that should influence future responses

---

### Episodic Memory
**Episodic memory** captures *specific past interactions or events*, usually tied to time, context, or execution state.

In agentic systems, episodic memory allows an agent to recall *what happened before*, not just *what is generally true*.

**In this project:**
- Implemented via checkpointed state and execution history
- Used to resume, inspect, or reason over prior runs
- Often scoped to a conversation or workflow instance

**Typical use cases:**
- Remembering prior emails or tasks in a workflow
- Debugging or replaying agent behavior
- Maintaining continuity across multi-step or long-running executions

---

### Procedural Memory
**Procedural memory** represents *how to do things* — skills, routines, and learned behaviors rather than facts.

For agents, procedural memory often manifests as reusable strategies, workflows, or decision policies that improve with experience.

**In this project:**
- Encoded through structured prompts, schemas, and graph logic
- Reinforced by writing outcomes back into memory
- Used to guide future planning and tool usage

**Typical use cases:**
- Learned response patterns (e.g., how to handle certain email types)
- Task-specific workflows that improve over time
- Strategy selection based on past success or failure

---

Together, **semantic, episodic, and procedural memory** enable agents that are not only stateful, but *adaptive* — capable of learning from experience, retaining knowledge, and refining behavior over time.
---

## Notebook Overview

### Lesson 3 — Memory Fundamentals  
`L3/lesson_3.ipynb`

Introduces **Email Assitant with Semantic memory** in LangGraph:
- How state persists across graph executions
- Differences between message passing and memory
- Basic memory-backed workflows

This lesson establishes the conceptual foundation for the rest of the project.

---

### Lesson 3.5 — Email Assistant with Semantic Memory & Custom Memory Writers  
`L3/lesson_3_5_semantic_memory_custom_mem_writer.ipynb`

Dives deeply into **semantic memory** using LangMem:
- Vector-based memory stores
- Custom memory writer implementations
- Explicit control over memory read/write behavior

This notebook is the conceptual core of the repository.

---

### Lesson 4 — Email Assistant with Sematic and Episodic Memory
`L4/lesson_4.ipynb`

Explores production-oriented memory patterns:
- Checkpoint-backed memory
- Durable state persistence
- Resumable and inspectable graph executions

Focuses on making memory reliable in longer-running or iterative workflows.

---

### Lesson 5 — Email Assistant with Semantic, Episodic and Procedural Memory
`L5/lesson_5.ipynb`

Demonstrates how agents can:
- Read selectively from memory
- Write new memories based on outcomes
- Use memory to influence future planning and reasoning

Shows memory as a **first-class agent capability**, not just storage.

---

## Dependency Management (uv-only)

This project intentionally uses **uv and only uv** for dependency management.

### Install dependencies
```bash
uv sync
```

### Add or update a dependency
```bash
uv add <package>
uv lock
uv sync
```

### Export a pip-compatible lockfile (optional)
```bash
uv pip compile pyproject.toml -o requirements.locked.txt
```

> `uv.lock` is the authoritative lockfile.  
> `requirements.locked.txt` is included only for compatibility with tooling that expects a `requirements.txt`-style file.

---

## API Keys

Set your OpenAI API key before running the notebooks:

```bash
export OPENAI_API_KEY=your-key-here
```

Or via a `.env` file:
```
OPENAI_API_KEY=your-key-here
```

---

## Requirements

- macOS, Linux, or WSL2
- Python 3.13+
- uv
- OpenAI API key

---

## Notes

- This repository intentionally avoids Conda to keep the environment minimal and reproducible.
- All examples assume execution inside the `uv`-managed virtual environment.
- Supporting `.py` files are designed to be read alongside the notebooks and reused across lessons.
