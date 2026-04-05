# Nexus — Claude Code Project Memory

## What This Project Is

A **Prediction and Simulation System** that ingests live data from:
- **Polymarket** — prediction market probabilities (event outcomes)
- **FRED** — Federal Reserve macroeconomic data (GDP, inflation, unemployment)
- **Kalshi** — US-regulated event contracts
- **Alpaca** — stock and crypto market data + paper trading

Built by two collaborators learning Python together.

---

## The Learning Contract

**Every line of code in this repo was understood before it was written.**

This project is NOT vibe-coded. When Claude writes something, it must explain:
1. **What** the code does
2. **Why** this approach over alternatives
3. **Where** it fits in the overall system

If a line of code cannot be explained, it should not be in this repo.

---

## How Claude Should Behave in This Project

- **Never run terminal commands automatically.** Always give commands as code blocks for the user to run manually.
- **Explain before you write.** Describe the concept and design decision, then write the code.
- **Teach tradeoffs.** When there are multiple ways to do something, say so and explain the choice.
- **Challenge the developers.** Sometimes ask "what do you think this should do?" before writing it.
- **Python best practices always.** Type hints, Pydantic models, structured logging, no hardcoded secrets.

---

## Project Conventions

### Python version
Python 3.11+

### Package management
`uv` (faster pip alternative) — or plain `pip` with a virtual environment

### Code style
- Type hints on every function signature
- Pydantic for all data models (no raw dicts passed around)
- `httpx` for async HTTP requests (not `requests`)
- `python-dotenv` for loading `.env` files
- Structured logging with the standard `logging` module

### File structure
```
nexus/
├── CLAUDE.md              ← you are here
├── pyproject.toml         ← project metadata and dependencies
├── .env.example           ← template for API keys (never commit .env)
├── .gitignore
├── README.md
├── src/
│   └── nexus/
│       ├── __init__.py
│       ├── config.py      ← all env vars loaded here, nowhere else
│       ├── clients/       ← one file per data source
│       │   ├── fred.py
│       │   ├── polymarket.py
│       │   ├── kalshi.py
│       │   └── alpaca.py
│       ├── models/        ← Pydantic data models
│       ├── simulation/    ← simulation engine
│       └── prediction/   ← forecasting logic
└── tests/                 ← pytest tests, written alongside features
```

### Commit message format (Conventional Commits)
```
feat: add FRED GDP endpoint
fix: handle Polymarket rate limit with backoff
docs: update README with Kalshi setup steps
test: add unit tests for FRED client
refactor: extract base HTTP client class
```

### Branching
- `main` — stable, working code only
- `feat/thing-you-are-building` — feature branches
- Open a Pull Request to merge into main, even with two people

---

## API Keys

All secrets go in `.env` (never committed). See `.env.example` for required keys.

| Service | Key Name | Where to get it |
|---|---|---|
| FRED | `FRED_API_KEY` | fred.stlouisfed.org/docs/api/api_key.html |
| Alpaca | `ALPACA_API_KEY`, `ALPACA_SECRET_KEY` | alpaca.markets |
| Kalshi | `KALSHI_EMAIL`, `KALSHI_PASSWORD` | kalshi.com |
| Polymarket | No key needed for read access | — |

---

## For New Collaborators (Onboarding)

```bash
# 1. Clone the repo
git clone https://github.com/YOUR_USERNAME/nexus.git
cd nexus

# 2. Create a virtual environment
python3 -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# 3. Install the project
pip install -e ".[dev]"

# 4. Set up your API keys
cp .env.example .env
# Edit .env and fill in your keys

# 5. Run the tests to confirm everything works
pytest
```

---

## Current Status

- [ ] Project scaffold (pyproject.toml, src layout)
- [ ] FRED client
- [ ] Polymarket client
- [ ] Kalshi client
- [ ] Alpaca client
- [ ] Pydantic data models
- [ ] Simulation engine
- [ ] Prediction layer
- [ ] CLI entry point
- [ ] README + full docs
