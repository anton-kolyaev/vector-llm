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
