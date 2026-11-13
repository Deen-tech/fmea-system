# Pressure Equipment FMEA Intelligent Assessment System

> A cleaned portfolio snapshot of a 2026 China Jiliang University "Challenge Cup" team project.

This repository contains the FastAPI/CrewAI-based intelligent assessment engine for pressure-equipment FMEA evaluation. The project explores a safety-critical AI design in which an LLM is used only for information extraction, while risk scoring and review decisions remain deterministic and auditable.

## Why this project exists

Manual FMEA assessment of pressure equipment is slow, difficult to update, and dependent on expert experience. Inspection reports are largely unstructured, while end-to-end LLM scoring introduces hallucination, non-determinism, and auditability problems.

The system addresses this with a **perception-decision separation** design:

1. **Perceive**: one LLM pass extracts structured defect fields.
2. **Decide**: a deterministic Python rule engine calculates S/O/D scores and risk classifications.
3. **Account**: high-risk or incomplete cases are intercepted for human review before persistence.

## Repository scope

Included:

- FastAPI API service
- CrewAI-based defect extraction workflow
- Three-layer deterministic rule engine
- Rule and failure-case knowledge base
- PWHT knowledge modules
- Review-gate and evidence-chain logic
- Portfolio documentation

Not included in this snapshot:

- The separate Spring Boot / MySQL seven-step FMEA management platform
- Production deployment configuration
- Enterprise or confidential inspection data
- Original team commit history

## Key technical features

- 20+ extracted defect fields with schema validation
- Multi-level fallback parsing for malformed LLM output
- 132 expert rules and 198 traceable failure cases in the included data
- `rule_id`, adjustment text, and standard reference attached to scoring evidence
- Server-side review gate for high-risk or incomplete cases
- Celery/Redis task orchestration
- Knowledge retrieval and PWHT parameter support
- API-key middleware for service access

## Tech stack

- Python 3.12
- FastAPI, Pydantic
- SQLAlchemy, Alembic, SQLite
- Celery, Redis
- CrewAI, LangChain
- FAISS / sentence-transformers
- OpenAI-compatible LLM endpoint

## Quick start

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
```

Edit `.env` and set your own `LLM_API_KEY` and `API_KEYS`. Never commit the real `.env` file.

```bash
alembic upgrade head
uvicorn app.main:app --reload
```

Open `http://localhost:8000/docs` for the API documentation. Protected endpoints require the `X-API-Key` header.

Redis is required for Celery-based asynchronous tasks. The exact worker command should be checked against `app/celery_app.py` before deployment.

## Project documentation

- [Project overview](docs/project_overview.pdf)
- [Architecture notes](docs/ARCHITECTURE.md)
- Workflow diagram: `docs/fmea_workflow.png`

## Evidence and limitations

- This is a laboratory-stage prototype.
- The reported evaluation-time and consistency figures are **internal project metrics**, not independent external validation.
- The included demonstration uses a limited case set and should not be treated as production validation.
- The repository is shared as a portfolio snapshot; it does not by itself establish individual contribution boundaries.

## Team and attribution

- Institution: China Jiliang University, College of Management Science and Engineering
- Project context: 2026 "Challenge Cup" student innovation competition, Technology Invention Category B
- Original team repository: https://github.com/hxleason/hxlcrewai-defect-ai
- Portfolio snapshot maintained by: Liu De'en

This is a team project. No open-source license is granted by this snapshot. Contact the project maintainers before redistribution or commercial use.

## Security

Do not commit `.env`, API keys, access tokens, real inspection records, or confidential standards. See [SECURITY.md](SECURITY.md).
