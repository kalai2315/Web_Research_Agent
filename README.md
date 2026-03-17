# ReAct Research Agent (Ollama + Tavily)

A lightweight AI-powered research agent built in a Jupyter notebook. Given any topic, it autonomously plans research questions, searches the web for current information, and compiles everything into a structured markdown report — all without human intervention.

---

## How It Works

The agent follows the **ReAct (Reason → Act → Observe)** pattern across three phases:

1. **Reason** — An Ollama LLM decomposes the topic into 5 targeted research questions.
2. **Act** — The Tavily search API retrieves up-to-date web results for each question.
3. **Report** — All findings are compiled into a structured markdown report with introduction, per-question sections, and a conclusion.

---

## Prerequisites

- Python 3.10+
- [Ollama](https://ollama.com/) installed and running locally with a model pulled (default: `llama3.2:3b`)
- A [Tavily](https://tavily.com/) API key

---

## Installation

```bash
pip install ollama tavily-python python-dotenv
```

---

## Configuration

Create a `.env` file in the project root:

```env
TAVILY_API_KEY=your_tavily_api_key_here
OLLAMA_MODEL=llama3.2:3b 
```

---

## Usage

Open `web_agent.ipynb` in Jupyter and run all cells. To change the research topic, edit the `TOPIC` variable in the runner cell:

```python
TOPIC = "Climate Change"   # ← change this to any topic
agent  = ResearchAgent(topic=TOPIC)
report = agent.run(max_results=3)
```

The generated report is:
- Rendered as formatted markdown inside the notebook.
- Saved as a `.md` file (e.g., `report_climate_change.md`) in the working directory.

---

## Project Structure

```
web_agent.ipynb          # Main notebook
report_<topic>.md        # Auto-generated research report (created on run)
.env                     # API keys and model config (not committed)
```

---

## ResearchAgent API

| Method | Description |
|---|---|
| `ResearchAgent(topic)` | Initialise the agent with a research topic |
| `.generate_questions()` | Ask the LLM to produce 5 research questions |
| `.search_web(max_results)` | Run Tavily searches for each question |
| `.compile_report()` | Assemble findings into a markdown report |
| `.run(max_results)` | Run the full pipeline end-to-end |

---

## Example Output

Running on the topic **"Climate Change"** produces a report covering questions such as:
- How do climate change mitigation strategies impact local economies?
- Can machine learning algorithms accurately predict ocean acidification rates?
- What is the relationship between deforestation and global temperature regulation?
- How do climate change projections affect global food security?
- Are urban green spaces effective in reducing heat island effects?

---

## Dependencies

| Package | Purpose |
|---|---|
| `ollama` | Local LLM inference via Ollama |
| `tavily-python` | Web search API client |
| `python-dotenv` | Load environment variables from `.env` |
