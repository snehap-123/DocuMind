# DocuMind — AI-Powered Document Intelligence Platform

DocuMind is an AI-powered document intelligence platform that helps users upload PDF documents, search their contents semantically, ask questions in natural language, and generate document summaries.

The project combines vector-based retrieval with a locally running large language model to provide context-aware answers and relevant source references.

## Features

- **PDF Upload:** Upload and process PDF documents.
- **Semantic Search:** Find relevant content using natural-language queries and vector embeddings.
- **Document Q&A:** Ask questions about document content.
- **Document Summarization:** Generate concise overviews of uploaded documents.
- **Source References:** Retrieve relevant passages and document references to help users verify answers.
- **Vector Search:** Store and retrieve embeddings using PostgreSQL and pgvector.
- **Local LLM Inference:** Use Ollama for local language-model inference.

## Tech Stack

| Component | Technology |
|---|---|
| Frontend | React |
| Backend | Python, FastAPI |
| Database | PostgreSQL |
| Vector Search | pgvector |
| Embeddings | Sentence Transformers, `all-MiniLM-L6-v2` |
| Language Model | Ollama, `gemma3:1b` |
| PDF Processing | PDF extraction and OCR tooling |

## Architecture

1. A user uploads a PDF through the React frontend.
2. The FastAPI backend processes the document and extracts its text.
3. Text is divided into chunks and converted into vector embeddings.
4. Document content and embeddings are stored in PostgreSQL with pgvector.
5. A user's query is embedded and matched against relevant document chunks.
6. Retrieved context is used to generate an answer with the local language model.
7. Relevant source references are returned to support verification.

## Getting Started

### Prerequisites

Install the following before running the project:

- Python 3.10
- Node.js and npm
- Docker Desktop
- Ollama

### 1. Clone the repository

```bash
git clone https://github.com/snehap-123/DocuMind.git
cd DocuMind
```

### 2. Start the database

Start Docker Desktop, then run the database command configured for your project.

If your repository contains a Docker Compose configuration, use the service name and configuration defined in that file.

### 3. Configure the backend

Open a terminal in the backend directory:

```bash
cd backend
python -m venv venv
```

Activate the environment on Windows:

```powershell
.\venv\Scripts\Activate.ps1
```

Install the dependencies using the dependency file included in the backend, if available:

```bash
pip install -r requirements.txt
```

Configure your database connection and other required settings using your local environment configuration. Do not commit passwords, API keys, or `.env` files.

Start the API from the backend directory:

```bash
uvicorn app.main:app --reload
```

API documentation should be available at:

http://127.0.0.1:8000/docs

### 4. Configure the language model

Install and start Ollama, then ensure the model used by the backend is available:

```bash
ollama pull gemma3:1b
```

### 5. Start the frontend

Open a separate terminal and navigate to the frontend directory:

```bash
cd frontend
npm install
npm run dev
```

Open the local frontend URL printed by Vite in the terminal.

> Note: Database service names, environment variables, dependency files, OCR configuration, and startup commands may need to match your local project configuration.

## API Overview

The backend includes endpoints for document management, search, question answering, summaries, and document access.

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/documents/` | List documents |
| GET | `/documents/search` | Search document content |
| GET | `/documents/ask` | Ask questions about documents |
| POST | `/documents/upload` | Upload a document |
| GET | `/documents/{document_id}/summary` | Generate or retrieve a document summary |
| GET | `/documents/{document_id}/file` | Access a document file |
| GET | `/documents/{document_id}` | Retrieve document details |
| GET | `/documents/{document_id}/chunks` | Retrieve document chunks |

See the interactive FastAPI documentation at `/docs` for the actual request parameters and response schemas.

## Project Structure

```text
DocuMind/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── core/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── services/
│   │   └── main.py
│   └── requirements.txt
├── frontend/
├── docker-compose.yml
├── .gitignore
└── README.md
```

The exact files and folders may vary with the current implementation.

## Future Improvements

- Improve retrieval relevance and answer grounding.
- Add automated tests for the API and document-processing pipeline.
- Improve document-processing error handling.
- Add authentication and user-specific document access.
- Add evaluation metrics for retrieval and answer quality.
- Improve deployment and monitoring.

## Author

**Sneha Patil**

GitHub: [@snehap-123](https://github.com/snehap-123)

## License

No license has been specified yet.
