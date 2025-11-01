# Deal Evaluator

An AI-powered investment analysis platform that evaluates startups and investment opportunities using advanced language models. The system analyzes investment documents (call transcripts, pitch decks, memos) to score companies based on a comprehensive investment framework.

## Overview

Deal Evaluator combines a Python backend powered by LangChain and OpenAI GPT-4 with a modern React frontend to provide:

- **Automated Document Analysis**: Upload and process PDFs, DOCX, and TXT files
- **AI-Powered Scoring**: Evaluate companies across 19 investment principles in 3 categories (Team, Market, Technology)
- **Interactive Reports**: View detailed analysis with evidence-backed scores and recommendations
- **Investment Framework**: Structured evaluation based on proven VC principles

## Project Structure

This is a monorepo containing two applications:

```
deal_evaluator/
├── deal-evaluation-backend/    # Python/FastAPI Backend
│   ├── src/
│   │   ├── core/               # Configuration, models, database
│   │   ├── services/           # Business logic & LangChain agents
│   │   └── web/                # REST API endpoints
│   ├── cli/                    # Command-line interface
│   ├── data/                   # Input documents & output reports
│   └── scripts/                # Server startup scripts
│
└── pitch-insight-engine/       # React/TypeScript Frontend
    ├── src/
    │   ├── components/         # React UI components
    │   ├── pages/              # Page components
    │   └── lib/                # API client & utilities
    └── package.json
```

## Technology Stack

**Backend:**
- FastAPI + Uvicorn (Python web framework)
- LangChain (LLM orchestration)
- OpenAI GPT-4 (AI analysis)
- ChromaDB (vector database)
- PostgreSQL + SQLAlchemy (data persistence)

**Frontend:**
- React 18 + TypeScript
- Vite (build tool)
- shadcn/ui + Tailwind CSS (UI framework)
- TanStack Query (data fetching)
- React Router (routing)

## Prerequisites

- **Python 3.8+**
- **Node.js 18+** and npm
- **OpenAI API Key** ([Get one here](https://platform.openai.com/api-keys))

## Quick Start

### 1. Backend Setup

Navigate to the backend directory and set up the Python environment:

```bash
cd deal-evaluation-backend

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
cp env.example .env
# Edit .env and add your OpenAI API key:
# OPENAI_API_KEY=your_openai_api_key_here
```

Start the backend API server:

```bash
# Option 1: Using the web server script
python scripts/web_server.py

# Option 2: Using the Railway startup script
python start_server.py
```

The backend API will be available at:
- **API**: http://localhost:8000
- **Docs**: http://localhost:8000/docs (Interactive API documentation)

### 2. Frontend Setup

Open a new terminal, navigate to the frontend directory:

```bash
cd pitch-insight-engine

# Install dependencies
npm install

# Start the development server
npm run dev
```

The frontend will be available at:
- **App**: http://localhost:8080

### 3. Using the Application

1. Open http://localhost:8080 in your browser
2. Upload investment documents (PDF, DOCX, or TXT)
3. Click "Analyze" to process the documents
4. View the detailed evaluation report with scores and recommendations

## Alternative Usage: CLI

The backend also includes a command-line interface for batch processing:

```bash
cd deal-evaluation-backend
source venv/bin/activate

# Process all documents in data/input
python main.py

# Process documents for a specific company
python main.py --company "CompanyName"

# List available documents
python main.py --list

# Clean database
python main.py --clean
```

Reports are saved to `deal-evaluation-backend/data/output/reports/`

## Investment Framework

The system evaluates companies across **19 principles** grouped into 3 categories:

### Team Principles (10)
- Earned Insight
- Missionary Motivation
- Drive from Disadvantage
- Resilience Under Pressure
- Systems Thinking
- Learning Velocity
- Talent Magnetism
- Urgency Bias
- Intellectual Honesty
- Team Complementarity

### Market Principles (4)
- Macro Trends
- Market Size
- Go-to-Market
- Hidden Markets

### Technology Principles (5)
- AI-Native
- Rapid Evolution
- Tech Readiness
- AI-Era Defensibility
- Technical Edge

### Scoring System

Each principle is scored on a **1-4 scale**:
- **4** - Strong signal
- **3** - Positive signal
- **2** - Weak signal
- **1** - No signal

The system provides category averages and an overall investment recommendation.

## API Endpoints

### Core Endpoints

- `GET /` - API information
- `POST /upload` - Upload documents for analysis
- `POST /analyze` - Analyze documents for a company
- `GET /documents` - List all uploaded documents
- `GET /evaluations` - List all evaluations
- `GET /evaluation/{id}` - Get specific evaluation
- `DELETE /documents/{id}` - Delete a document

### Example API Usage

```bash
# Upload a document
curl -X POST "http://localhost:8000/upload" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@document.pdf"

# Analyze documents
curl -X POST "http://localhost:8000/analyze" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "company_name=Example Corp&document_ids=doc1,doc2"

# Get evaluation results
curl -X GET "http://localhost:8000/evaluation/{evaluation_id}"
```

## Development

### Backend Development

```bash
cd deal-evaluation-backend

# Run tests
python -m pytest tests/

# Start server with auto-reload
python scripts/web_server.py
```

### Frontend Development

```bash
cd pitch-insight-engine

# Start dev server with hot reload
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Lint code
npm run lint
```

## Environment Variables

### Backend (.env in deal-evaluation-backend/)

```bash
# Required
OPENAI_API_KEY=your_openai_api_key_here

# Optional
OPENAI_MODEL=gpt-4  # Default model
DATABASE_URL=sqlite:///deal_evaluation.db
VECTOR_DB_PATH=./vector_db
```

## Supported Document Formats

- **PDF** (.pdf) - Pitch decks, investment memos
- **DOCX** (.docx) - Word documents
- **TXT** (.txt) - Plain text files, call transcripts

## Deployment

The project includes Railway deployment configuration:

- `railway.json` - Railway deployment config
- `start_server.py` - Production server startup script

Frontend can be deployed to Vercel, Netlify, or any static hosting provider.

## Troubleshooting

### Backend Issues

**Issue**: ModuleNotFoundError when running scripts
- **Solution**: Make sure you're in the virtual environment and have run `pip install -r requirements.txt`

**Issue**: OpenAI API errors
- **Solution**: Verify your OPENAI_API_KEY is set correctly in `.env`

### Frontend Issues

**Issue**: API connection errors
- **Solution**: Ensure backend is running on port 8000
- Check CORS configuration in `deal-evaluation-backend/src/web/app.py`

**Issue**: Port 8080 already in use
- **Solution**: Change port in `pitch-insight-engine/vite.config.ts`

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## License

Proprietary - All rights reserved

## Support

For issues and questions, please open an issue on the repository.
