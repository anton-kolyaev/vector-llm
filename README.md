# Vector LLM Stack

This project provides a complete local LLM stack using Docker Compose, including:
- **AnythingLLM**: A full-stack application for RAG (Retrieval-Augmented Generation) and document chatting.
- **Ollama**: For running local LLM models (like Llama 3, Mistral, etc.).
- **PostgreSQL (pgvector)**: Vector database for storing embeddings.
- **PgAdmin**: Web interface for managing the PostgreSQL database.

## Prerequisites

- Docker and Docker Compose installed.
- (Optional) NVIDIA GPU + NVIDIA Container Toolkit for accelerated inference with Ollama.

## Quick Start

1.  **Start the stack:**
    ```bash
    docker-compose up -d
    ```

2.  **Access the services:**
    - **AnythingLLM**: [http://localhost:3001](http://localhost:3001)
    - **PgAdmin**: [http://localhost:5050](http://localhost:5050)
        - **Email**: `admin@admin.com`
        - **Password**: `admin`
    - **Ollama API**: [http://localhost:11434](http://localhost:11434)

## Alternative: Running with Local Ollama

If you prefer to run Ollama natively on your host machine (outside of Docker) to better utilize hardware resources or simply because you already have it installed:

1.  **Ensure Ollama is running**: Make sure Ollama is running on your host machine (usually at `http://localhost:11434`).
2.  **Pull Desired Model**:
    ```bash
    ollama pull llama3
    ```
3.  **Start the stack with the local profile**:
    ```bash
    docker compose -f docker-compose.local-ollama.yml up -d
    ```
    This profile excludes the `ollama` container and configures `anythingllm` to connect to your host's Ollama instance.

## Configuration

- **Environment Variables**: Check `.env` to configure ports, credentials, and database settings.
- **Data Persistence**: Data is persisted in the local directories:
    - `./storage` (AnythingLLM)
    - `./postgres_data` (PostgreSQL)
    - `./pgadmin_data` (PgAdmin)
    - `./ollama_data` (Ollama models)

## Using Ollama

Since the `ollama` container starts empty, you need to pull a model before you can use it.

To pull a model (e.g., `llama3`):
```bash
docker exec -it ollama_container ollama run llama3
```
(Press `Ctrl+D` to exit the chat after it loads).

Once pulled, you can select **Ollama** as your LLM provider in AnythingLLM settings and use `http://ollama:11434` as the base URL.

## Tips

- **Use Agent Rules**: Define clear rules for your AI agent to improve performance. You can find useful examples at [Cursor Directory](https://cursor.directory/rules).
- **Manage Context Effectively**: Keep the agent's context focused. Start a fresh chat for new topics and disable RAG, rules, or MCP tools if they are not relevant to the current task.
- **Select Appropriate Models**: Browse the [Ollama Library](https://ollama.com/library) for models. Model size matters for local performance; choose "non-cloud" sized models (e.g., 1B-8B parameters) that fit your hardware capabilities if you want to run everything locally.

