# Copilot Instructions for Agentic AI Engineer Course

This repository contains educational course materials for teaching LangChain and LangGraph concepts through hands-on exercises and demonstrations.

## Repository Structure

The repository is organized into **lesson folders** and a **project folder**:

- **Lesson folders**: `L1_Introduction_to_Agentic_Frameworks`, `L2_Building_with_LLMs_in_LangChain`, `L3_Agentic_Workflows_with_LangGraph`, `L4_Creating_a_Knowledge_Base_Agent`
- Each lesson folder contains:
  - `demos/`: Demo notebooks showing concepts (named `L#_demo_##_topic.ipynb`)
  - `exercises/`: Exercise folders with starter and solution notebooks
- **Project folder**: `project/` contains final project materials

### File Naming Conventions

- **Demo notebooks**: `L#_demo_##_topic_name.ipynb` (e.g., `L1_demo_01_memory_layer.ipynb`)
- **Starter exercises**: `L#_starter_exercise_##_topic_name.ipynb` 
- **Solution exercises**: `L#_solution_exercise_##_topic_name.ipynb`
- Each exercise folder contains both starter and solution files side-by-side

## Architecture

### Educational Content Flow

1. **L1**: Introduction to core agentic patterns (memory, function calling, ReAct, multi-agents) using raw OpenAI client
2. **L2**: Building LLM applications with LangChain (chat, streaming, output parsing, LCEL, RAG, tools, agents)
3. **L3**: Advanced workflows with LangGraph (state graphs, schemas, reducers, config, checkpoints)
4. **L4**: Knowledge base agents with evaluation

### Key Technologies

- **LangChain**: Core framework for LLM applications (`langchain_openai`, `langchain_core`)
- **LangGraph**: Workflow orchestration with state management (`langgraph.graph`)
- **OpenAI**: Primary LLM provider (uses `gpt-4o-mini` and similar models)
- **Environment Management**: `.env` files with `python-dotenv` for API keys

## Working with Notebooks

### Running Notebooks

Notebooks are Jupyter notebooks (`.ipynb`) that can be run in:
- Jupyter Notebook/Lab
- VS Code with Jupyter extension
- Udacity workspace environment

### Common Setup Pattern

Most notebooks follow this pattern:
```python
from dotenv import load_dotenv
from openai import OpenAI  # or from langchain_openai import ChatOpenAI

load_dotenv()  # Loads OPENAI_API_KEY from .env
client = OpenAI()  # Auto-uses env var
```

### Dependencies

No centralized `requirements.txt` - dependencies are per-lesson/exercise. Common packages:
- `openai` - OpenAI client
- `langchain`, `langchain-openai`, `langchain-core` - LangChain framework
- `langgraph` - LangGraph for workflows
- `python-dotenv` - Environment variable management
- `sqlalchemy` - Database operations (L3 exercises)

## Key Conventions

### Starter vs Solution Files

- **Starter files**: Incomplete notebooks with `# TODO` sections for students to complete
- **Solution files**: Complete implementations showing the intended approach
- Always maintain both files in sync regarding structure and instructions

### Memory and State Management

- **L1**: Manual message history arrays (`memory = [{"role": "system", ...}, ...]`)
- **L2**: LangChain memory abstractions
- **L3**: LangGraph state management with `TypedDict` schemas and reducers

### Tool Definition Patterns

**L1 (Raw OpenAI)**:
```python
tools = [{
    "type": "function",
    "function": {
        "name": "tool_name",
        "description": "...",
        "parameters": {...}
    }
}]
```

**L2/L3 (LangChain)**:
```python
from langchain_core.tools import tool

@tool
def tool_name(arg: str, config: RunnableConfig) -> str:
    """Tool description"""
    pass
```

### Configuration Passing (L3+)

LangGraph exercises use `RunnableConfig` to pass context:
```python
@tool
def my_tool(config: RunnableConfig):
    db_engine = config.get("configurable", {}).get("db_engine")
```

### SQLite Databases

Some exercises (e.g., L3 text2sql) include `.db` files (like `sales.db`) - these are SQLite databases used for demonstrations.

## Supporting Helper Files

- **sql_toolkit.py** (L3): Reusable SQL tools for database interaction exercises
- Exercise folders may contain custom Python modules - always check for `.py` files alongside notebooks

## Environment Setup

Create a `.env` file in the working directory with:
```
OPENAI_API_KEY=your_api_key_here
```

This is git-ignored and required for all notebooks to function.

## Content Development Guidelines

When creating new content:

1. **Maintain naming convention**: Follow `L#_[demo|starter|solution]_exercise_##_name.ipynb`
2. **Keep pairs in sync**: Starter and solution files should have identical structure/instructions
3. **Import consistency**: Use established import patterns for each lesson level
4. **API key handling**: Always use `dotenv` pattern, never hardcode keys
5. **Incremental complexity**: Each lesson builds on previous concepts

## Project Folder

The `project/` folder contains:
- `README.md`: Template for project setup instructions
- `solution/`: Reference implementation for course project

This serves as the capstone where students apply all learned concepts.
