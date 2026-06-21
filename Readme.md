# RAG Project

This folder contains a simple Retrieval-Augmented Generation (RAG) setup using:

- `Qdrant` as the vector database
- `langchain` document loading and splitting
- OpenAI embeddings via `text-embedding-3-large`
- a sample `nodejs.pdf` source document
- a simple `chat.py` query interface for retrieving context and asking OpenAI

## Files

- `docker-compose.yml` - starts a local Qdrant instance
- `index.py` - loads the PDF, splits it into chunks, embeds the chunks, and stores them in Qdrant
- `chat.py` - queries the existing Qdrant collection and sends results to OpenAI chat

## Prerequisites

- Python 3.10+ or compatible
- Docker installed and running
- An OpenAI API key available in your environment (for example, in `.env`)

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
pip install python-dotenv langchain langchain-openai langchain-qdrant langchain-text-splitters qdrant-client openai
```

3. Place the PDF file you want to index in the `RAG/` folder and name it `nodejs.pdf`.

4. Create a `.env` file in `RAG/` or the project root with your OpenAI API key:

```bash
OPENAI_API_KEY=your_api_key_here
```

## Indexing documents

Run the indexing script to load and index the PDF into Qdrant:

```bash
python RAG/index.py
```

## Chat / query interface

After indexing, ask questions against the stored embeddings:

```bash
python RAG/chat.py
```

The script will retrieve relevant chunks from Qdrant and use OpenAI to answer based on that context.

## What it does

- loads `nodejs.pdf`
- splits the content into smaller chunks using `RecursiveCharacterTextSplitter`
- creates embeddings with OpenAI
- stores the embeddings in a Qdrant collection named `RAG`
- retrieves relevant chunks and sends them to OpenAI chat for an answer

## Notes

- Make sure Qdrant is available at `http://localhost:6333`
- If you want to use a different PDF file or collection name, update `index.py` and `chat.py`
- Ensure `OPENAI_API_KEY` is available in your environment before running either script
