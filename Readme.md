# RAG Project

This folder contains a simple Retrieval-Augmented Generation (RAG) setup using:

- `Qdrant` as the vector database
- `langchain` document loading and splitting
- OpenAI embeddings via `text-embedding-3-large`
- a sample `nodejs.pdf` source document

## Files

- `docker-compose.yml` - starts a local Qdrant instance
- `index.py` - loads the PDF, splits it into chunks, embeds the chunks, and stores them in Qdrant

## Prerequisites

- Python 3.10+ or compatible
- Docker installed and running
- An OpenAI API key available in your environment

## Setup

1. Start Qdrant:

```bash
docker compose up -d
```

2. Install Python dependencies.

If the root `requirements.txt` contains the needed packages, run:

```bash
pip install -r requirements.txt
```

Alternatively, install the required packages manually:

```bash
pip install python-dotenv langchain langchain-openai langchain-qdrant langchain-text-splitters qdrant-client
```

3. Place the PDF file you want to index in the `RAG/` folder and name it `nodejs.pdf`.

4. Run the indexing script:

```bash
python RAG/index.py
```

## What it does

- loads `nodejs.pdf`
- splits the content into smaller chunks using `RecursiveCharacterTextSplitter`
- creates embeddings with OpenAI
- stores the embeddings in a Qdrant collection named `RAG`

## Notes

- Make sure Qdrant is available at `http://localhost:6333`
- Update the script if you want a different PDF path or collection name
- If you use an environment file, ensure `OPENAI_API_KEY` is set before running the script
