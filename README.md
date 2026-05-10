# Hybrid Rag Engine

Structured filters plus semantic retrieval in one RAG pipeline.

[![CI](https://github.com/NotPBShaw/hybrid-rag-engine/actions/workflows/ci.yml/badge.svg)](https://github.com/NotPBShaw/hybrid-rag-engine/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Combine metadata filters with vector ranking to narrow candidates before semantic search.

## Why this exists

Pure vector search ignores structured constraints; pure SQL misses semantic similarity. Hybrid retrieval applies both in one call.

## Quickstart

```bash
python -m venv .venv && source .venv/bin/activate
pip install -e .
pytest -q
```

## Usage

```python
from hybrid_rag.pipeline import hybrid_retrieve

rows = [{"team": "platform", "doc": "runbook-a"}]
docs = ["restart procedure", "incident escalation"]
result = hybrid_retrieve({"team": "platform"}, rows, "restart", docs)
print(result["structured"], result["semantic"])
```

## Architecture

- `schema_search.py` — structured filter pass over tabular rows
- `vector_search.py` — semantic ranking over document strings
- `pipeline.py` — orchestrates both passes and returns merged results

## Development

```bash
make check
pytest -q
```

## License

MIT — see [LICENSE](LICENSE).
