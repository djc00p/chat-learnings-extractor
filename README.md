# 🧠 Chat Learnings Extractor

[![ClawHub Skill](https://img.shields.io/badge/ClawHub-Skill-blue)](#) [![Python 3.x](https://img.shields.io/badge/python-3.x-blue)](#) [![Local AI/Ollama](https://img.shields.io/badge/Mode-Ollama-green)](#) [![Cloud AI/OpenAI](https://img.shields.io/badge/Mode-OpenAI-orange)](#)

**Chat Learnings Extractor** is an intelligent analysis engine designed to mine actionable insights from your AI conversation history. While the [Chat History Importer](https://github.com/djc00p/chat-history-importer) handles the *logistics* of moving data, this tool handles the *intelligence*—distilling massive JSON exports into structured, high-value "learnings" like lessons learned, decisions made, and patterns identified.

By using either a local **Ollama** instance or any **OpenAI-compatible API**, this tool transforms raw, unstructured chat logs into **Semantic Memory** that your agents can use to avoid past mistakes and replicate successful strategies.

---

## 🔄 The Knowledge Pipeline

This tool is the second step in a two-part workflow designed to build a permanent, searchable brain for your AI agents.

1. **Step 1: Ingestion (`chat-history-importer`)**
    * **Input:** Raw OpenAI/Anthropic JSON exports.
    * **Output:** **Episodic Memory** (`memory/episodic/YYYY-MM-DD.md`).
    * *Purpose:* Stores the "what happened" in a chronological timeline.

2. **Step 2: Extraction (`chat-learnings-extractor`)**
    * **Input:** The processed conversations.
    * **Output:** **Semantic Memory** (`memory/semantic/learnings-from-exports.md`).
    * *Purpose:* Extracts the "what we learned" (lessons, decisions, patterns, dead ends).

---

## ✨ Key Features

* **🤖 Dual-Mode Intelligence:**
  * **Local Mode (Privacy First):** Uses **Ollama** to process everything on your own machine. No data leaves your hardware.
  * **Cloud Mode (Power First):** Uses **OpenAI-compatible APIs** (OpenAI, Bedrock, LM Studio) for high-reasoning tasks.
* **🔍 Pattern Mining:** Specifically looks for **Lessons Learned**, **Decisions Made**, **Patterns**, and **Dead Ends** (to prevent repeating mistakes).
* **🚫 Smart Deduplication:** Uses a `.processed_ids` tracker. You can run the extractor on the same folder repeatedly without duplicating insights.
* **📉 Context Management:** Automatically summarizes long conversations to fit within the model's context window, ensuring even massive chats can be analyzed.
* **📂 Structured Output:** Appends results to a clean, Markdown-formatted "Semantic Memory" file.

---

## 🚀 Quick Start

### Scenario A: Running Locally (Ollama)

*Best for privacy and zero cost.*
**Prerequisite:** Ollama must be running.

```bash
# Dry run to see what will be processed
python3 scripts/extract.py --dir ~/Downloads/exports --limit 3 --dry-rag

# Process an entire directory
python3 scripts/extract.py --dir ~/Downloads/exports
```

### Scenario B: Using Cloud APIs (OpenAI/Bedrock/etc.)

*Best for complex reasoning and larger datasets.*

```bash
# Set your credentials
export OPENAI_API_KEY=sk-your-key-here
export OPENAI_BASE_URL=https://api.openai.com/v1

# Run extraction using a specific model
python3 scripts/extract.py --dir ~/Downloads/exports --model gpt-4o-mini
```

---

## 🛠 Usage Reference

| Argument | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `--dir` | `path` | The directory containing your JSON exports. | `--dir ~/exports` |
| `--file` | `path` | Process a single specific JSON file. | `--file chat.json` |
| `--limit` | `int` | Number of conversations to process (great for testing). | `--limit 5` |
| `--since` | `date` | Only process chats from this date (`YYYY-MM-DD`). | `--since 2024-01-01` |
| `--model` | `string` | Override the default model name. | `--model llama3` |
| `--dry-run` | `flag` | Print findings to terminal without saving to disk. | `--dry-run` |

---

## 📂 Output Structure

The extractor appends findings to `memory/semantic/learnings-from-exports.md`. Each extraction follows this clean format:

```markdown
## Chat Title (YYYY-MM-DD)

### Lessons Learned

- [Extracted lesson 1]
- [Extracted lesson 2]

### Decisions Made

- [Decision regarding project X]

### Patterns Noticed

- [Recurring behavior or theme]

### Dead Ends

- [What didn't work and why]
```

---

## ⚙️ Configuration & Environment

The tool automatically detects your workspace via `OPENCLAW_WORKSPACE`. If not set, it defaults to `~/.openclaw/workspace`.

### Environment Variables

| Variable | Default | Description |
| :--- | :--- | :--- |
| `OPENAI_API_KEY` | *None* | If set, the tool switches from **Ollama** to **OpenAI mode**. |
| `OPENAI_BASE_URL` | `https://api.openai.com/v1` | Useful for using LM Studio, Groq, or Anthropic Bedrock. |
| `OLLAMA_BASE_URL` | `http://127.0.0.1:11434` | Use this if your Ollama instance is on a different machine. |

---

### Clawhub [Chat Learnings Extractor](https://clawhub.ai/djc00p/chat-learnings-extractor)

**Original implementation by [@djc00p](https://github.com/djc00p)**
