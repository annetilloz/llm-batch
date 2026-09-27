# llm-batch

Run a JSONL of prompts through an LLM, results to JSONL

Built for my own use; public in case it helps someone.

## Examples

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## What it does

- Real rate limiting: sliding windows on requests/min and tokens/min
- Progress, token counts and a cost estimate on stderr
- Idempotent: ids already in the output are skipped on a rerun
- 4xx fails fast; 429 and 5xx retry with jittered backoff
- Per-row overrides for model, system, temperature and max_tokens
- JSONL in, JSONL out: the input is streamed line by line
- Failures go to a sidecar file with error type, message and status
- A bad input line is logged and skipped, never fatal

## Getting started

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## Project structure

```text
├── docs/
│   ├── development.md
│   ├── tradeoffs.md
│   └── usage.md
├── examples/
│   └── quickstart.md
├── tests/
│   └── test_smoke.py
├── .gitattributes
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── SECURITY.md
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## Development

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m pytest -q
```

## 说明

个人练习项目, 谨慎用于生产环境。

## License

MIT licensed, see LICENSE.
