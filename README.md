# Deploy and Host AI Agent API with Railway

OpenAI agent with tool calling — send a prompt, the model runs tools, you get the answer plus a trace.

## About AI Agent API

A FastAPI service that runs a simple OpenAI agent loop with built-in tools (current time, calculator). Responses include a tool trace so you can see what the model executed. Extend with your own tools in `app/tools.py`.

## About Hosting AI Agent API

Railway keeps your `OPENAI_API_KEY` server-side and exposes a single HTTPS endpoint for agent requests. No database required — deploy, set variables, and call `/v1/agent`.

## Environment Variables

| Variable | Description | Secret | Example/Notes |
| --- | --- | --- | --- |
| `OPENAI_API_KEY` | Your OpenAI API key | Yes | User-supplied at deploy time |
| `OPENAI_MODEL` | Chat model with tool support | No | `gpt-4o-mini` |
| `API_KEY` | Protects `/v1/agent` | Yes | `${{secret(32)}}` — send as `X-API-Key` |
| `MAX_TOOL_ROUNDS` | Safety limit on tool loops | No | `5` |

## Deploy and Host

1. Deploy this repo from GitHub on Railway.
2. Set `OPENAI_API_KEY`, `OPENAI_MODEL`, `API_KEY`, and optionally `MAX_TOOL_ROUNDS`.
3. Enable **public HTTP** and deploy.
4. Confirm `/health` returns OK.
5. Test an agent request:

```bash
curl -X POST https://YOUR-URL/v1/agent \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_KEY" \
  -d "{\"prompt\":\"What is 25 times 4? Use the calculator.\"}"
```

## Common Use Cases

- Prototypes exploring tool-calling agents
- Internal assistants that need server-side API keys
- Backends for chat UIs with observable tool traces
- Starting point for custom agent tools (API calls, DB lookups)

## Dependencies for AI Agent API Hosting

The Railway template includes:

- **AI Agent API** — this GitHub repo (FastAPI + Uvicorn)

## Deployment Dependencies

- [OpenAI function calling docs](https://platform.openai.com/docs/guides/function-calling)
- [FastAPI documentation](https://fastapi.tiangolo.com/)

## Why Deploy AI Agent API on Railway?

Zero infrastructure beyond one service — health checks, HTTPS, and secret management for your OpenAI key out of the box.

## Template Content

| Service | Source |
| --- | --- |
| AI Agent API | GitHub repo (this template) |

## Adding your own tools

Edit `app/tools.py`: add a tool definition to `TOOLS` and handle it in `run_tool`.

## Run locally

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
uvicorn app.main:app --reload --port 8000
```

## Author

romeoxt — herbylegall9@gmail.com

## License

MIT
