# Multi-Agent Research Assistant

A Python-based research assistant combining FastAPI, Gemini, and local JSON storage for rapid MVP iteration.

## Overview

This project implements a research workflow with:
- a FastAPI backend for orchestration and data access
- a multi-agent pipeline for search, summarization, fact-checking, and report generation
- Gemini AI for content generation
- JSON file storage for projects, reports, users, and caches
- a Streamlit frontend for easy local exploration

## What the system does

- Accepts research briefs via REST API or Streamlit
- Creates a local JSON-backed project record
- Uses a Search Agent to gather source content
- Uses a Summarization Agent to extract insights and structure
- Uses a Fact-Check Agent to verify claims across sources
- Uses a Report Agent to build a polished Markdown report
- Saves outputs under `data/projects/` and `data/reports/`

## Core Architecture

```
User Query
   ↓
FastAPI Controller
   ↓
Search Agent
   ↓
Summarization Agent
   ↓
Fact-Check Agent
   ↓
Report Agent
   ↓
JSON Storage
   ↓
Streamlit / API Client
```

## Project Structure

```
AI_Research_Agent/
├── main.py                 # FastAPI application entry point
├── controller.py           # Orchestration workflow
├── requirements.txt        # Python dependencies
├── README.md               # Project documentation
├── streamlit_app.py        # Streamlit frontend UI
├── agents/
│   ├── searchAgent.py      # Search and content extraction
│   ├── summarizeAgent.py   # Content summarization
│   ├── factCheckAgent.py   # Claim verification
│   └── reportAgent.py      # Report generation
├── services/
│   ├── geminiService.py    # Gemini API integration
│   └── storageService.py   # JSON persistence layer
├── routes/
│   └── researchRoutes.py   # API route definitions
├── utils/
│   └── jsonDB.py           # Storage abstraction
└── data/
    ├── users/              # User JSON documents
    ├── projects/           # Project JSON documents
    ├── reports/            # Generated report JSON documents
    └── cache/              # Cached search results
```

## Dependencies

- `fastapi`
- `uvicorn`
- `google-generativeai`
- `requests`
- `beautifulsoup4`
- `pydantic`
- `python-dotenv`
- `aiofiles`
- `streamlit`

## Installation

### Prerequisites
- Python 3.10+
- Google Gemini API key

### Setup

1. Clone the repository.
2. Install dependencies:

```bash
python3 -m pip install -r requirements.txt
```

3. Create a `.env` file in the project root:

```env
GEMINI_API_KEY=your_gemini_api_key_here
```

4. Create the data folders if they do not already exist:

```bash
mkdir -p data/users data/projects data/reports data/cache
```

## Running the backend

Start the FastAPI app:

```bash
python3 main.py
```

or:

```bash
python3 -m uvicorn main:app --reload
```

The API will be available at `http://localhost:8000`.

## Running the Streamlit frontend

In a separate terminal:

```bash
streamlit run streamlit_app.py
```

The Streamlit app can:
- start a new research project
- refresh project status
- load saved JSON project files from `data/projects/`
- display sources, summary, fact checks, and final report in readable format

## API Endpoints

### Start Research

```http
POST /api/research
Content-Type: application/json

{
  "user_id": "user_001",
  "query": "Impact of AI agents on startup productivity"
}
```

Response:

```json
{
  "project_id": "<project-id>",
  "status": "started",
  "message": "Research project started successfully"
}
```

### Get Project Data

```http
GET /api/project/{project_id}
```

Returns the full project JSON, including status, sources, summary, fact checks, and final report.

### Get Report

```http
GET /api/report/{report_id}
```

Returns the saved report JSON document.

### List User Projects

```http
GET /api/projects/{user_id}
```

Returns all projects for the given user.

## Data Storage

Project and report data are persisted as JSON files in `data/projects/` and `data/reports/`.
Each document includes metadata like `_id`, `_created_at`, and `_updated_at`.

## Notes

- The search agent currently uses static example content and web scraping for MVP behavior.
- The Gemini service is configured via `GEMINI_API_KEY` and uses `gemini-2.5-pro` and `gemini-1.5-flash` models.
- Local JSON storage is intentionally simple for fast iteration and debugging.

## Extending the system

- Add or improve search integrations in `agents/searchAgent.py`
- Refine summarization prompts in `agents/summarizeAgent.py`
- Improve verification logic in `agents/factCheckAgent.py`
- Add new API endpoints in `routes/researchRoutes.py`

## License

This project is open source. See LICENSE file for details.


Research results are automatically saved to `research_output.txt` with:
- Timestamp of when the research was conducted
- Full research output
- Append mode to maintain research history

## Error Handling

The application includes robust error handling:
- JSON parsing failures default to raw response output
- Tool execution errors are caught and reported
- Invalid queries are handled gracefully

## Requirements

See `requirements.txt` for the complete list of dependencies and their versions.

## Notes

- Ensure your Anthropic API key has sufficient quota
- Internet connection required for web search and Wikipedia queries
- Research outputs accumulate in `research_output.txt`; consider archiving or clearing periodically

## Future Enhancements

Potential improvements:
- Support for additional search providers
- Custom knowledge base integration
- Advanced query preprocessing and understanding
- Multi-query research workflows
- Result summarization and comparison
