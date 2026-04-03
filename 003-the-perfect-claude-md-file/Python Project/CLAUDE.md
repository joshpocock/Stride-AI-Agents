# Commands
- Install: uv sync
- Dev: uv run python -m app
- Test: uv run pytest
- Test single: uv run pytest -k "test_name"
- Lint: uv run ruff check .
- Format: uv run ruff format .
- Typecheck: uv run pyright

# Code Standards
- All code MUST include type hints
- Public APIs require docstrings (Google style)
- Use uv exclusively - NEVER use pip or pip install
- Maximum function length: 50 lines
- Use f-strings for formatting

# Architecture
- App entry: src/app/main.py
- API routes: src/app/routes/
- Models: src/app/models/
- Utilities: src/app/utils/

# After Every Change
1. uv run pyright
2. uv run pytest
3. uv run ruff check .

# Common Mistakes
- Database connections must be closed in finally blocks
- The /api/v2/ endpoints use async - do not mix sync handlers
- Rate limiter uses sliding window, not fixed window

# Do Nots
- NEVER use pip - use uv add, uv run
- NEVER use print() for logging - use structlog
- NEVER store secrets in code - use environment variables
