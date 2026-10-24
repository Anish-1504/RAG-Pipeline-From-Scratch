# Advanced RAG Document Intelligence System

An end-to-end Retrieval-Augmented Generation (RAG) application that ingests documents, retrieves relevant context through semantic search, and generates context-grounded answers using a Groq-hosted language model.

## Features

- **Multi-format document ingestion:** Supports TXT, PDF, CSV, and HTML documents through LangChain document loaders.
- **Document chunking:** Uses `RecursiveCharacterTextSplitter` with a chunk size of 1,000 characters and 200-character overlap.
- **Semantic embeddings:** Generates embeddings with Sentence Transformers using `all-MiniLM-L6-v2`.
- **Persistent vector storage:** Stores and retrieves document embeddings with ChromaDB.
- **Similarity-based retrieval:** Retrieves the most relevant chunks and applies a configurable cosine-similarity threshold.
- **LLM-powered answers:** Uses LangChain's `ChatGroq` integration with a configured Groq-hosted model.
- **Source attribution:** Returns source information and similarity scores to help users inspect the retrieved context.
- **Streaming and summaries:** Supports streamed responses and context-based summarization.
- **Conversation history:** Includes in-memory chat history and citation support.

## Architecture

1. **Load:** Read source documents using LangChain loaders.
2. **Split:** Divide documents into overlapping chunks while preserving metadata.
3. **Embed:** Convert chunks and user queries into vector embeddings.
4. **Index:** Persist document vectors in ChromaDB.
5. **Retrieve:** Search for relevant chunks and filter by similarity.
6. **Generate:** Pass retrieved context to the Groq LLM to produce an answer grounded in the available documents.
7. **Present:** Return the response with source details, similarity scores, and optional streaming.

## Tech Stack

- Python
- LangChain and `langchain-core`
- ChromaDB
- Sentence Transformers
- Hugging Face embedding model: `all-MiniLM-L6-v2`
- Groq API / `ChatGroq`

## Project Structure

Adapt this example to match the actual names of files and folders in your repository.

```text
.
├── data/                 # Source documents (optional)
├── chroma_db/            # Persistent vector database (if configured locally)
├── main.py               # Application entry point (example)
├── requirements.txt      # Python dependencies
└── README.md
```

## Setup

### 1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

### 2. Create and activate a virtual environment

**Windows (PowerShell):**

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

If the repository includes a `requirements.txt` file:

```bash
pip install -r requirements.txt
```

Otherwise, install the core packages used by the project:

```bash
pip install langchain langchain-core langchain-community langchain-groq chromadb sentence-transformers pypdf beautifulsoup4
```

Depending on the loader implementation, CSV and HTML parsing may require additional packages.

### 4. Configure your Groq API key

Create a `.env` file in the project root and add:

```env
GROQ_API_KEY=your_groq_api_key_here
```

Load the variable through your application's configuration. Do not hard-code API keys in source code or commit `.env` to GitHub. Add `.env` and local database/data files to `.gitignore` where appropriate.

## Usage

Run the entry-point file used by your project. For example:

```bash
python main.py
```

If your repository uses a notebook or a different entry point, run that instead. Update this section with the exact command and any required input paths or CLI arguments.

## Configuration

The current implementation uses these settings:

| Component | Configuration |
|---|---|
| Chunk size | 1,000 characters |
| Chunk overlap | 200 characters |
| Embedding model | `all-MiniLM-L6-v2` |
| Vector database | ChromaDB with persistence |
| LLM integration | LangChain `ChatGroq` |
| Temperature | `0.1` |
| Maximum output tokens | `1,024` |

The exact Groq model identifier should match the model available to your Groq API account and the value configured in your code.

## Example Workflow

1. Add supported documents to the configured input location.
2. Run the ingestion process to load, split, embed, and index the documents.
3. Submit a natural-language question.
4. The retriever searches the vector store for relevant chunks.
5. The LLM generates an answer using the retrieved context.
6. Review the answer alongside the source metadata and similarity scores.

## Important Notes

- Answers depend on the quality and coverage of the indexed documents.
- Similarity thresholds may need tuning for your dataset and embedding model.
- In-memory chat history is temporary and is lost when the application process stops unless persistence is implemented.
- Avoid indexing confidential information unless your storage and access controls are appropriate.
- Never commit API keys, secrets, or private source documents to a public repository.

## Future Improvements

- Add a FastAPI backend and a web interface.
- Containerize the application with Docker.
- Add automated tests and retrieval evaluation metrics.
- Implement robust error handling, logging, and configuration management.
- Add authentication and access controls for multi-user deployments.

## License

Add the license you intend to use for this repository. If no license has been selected, remove this section until one is chosen.
