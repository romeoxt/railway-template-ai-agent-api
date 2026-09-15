# Railway Template Composer Setup

## Marketplace listing

- **Title:** Deploy and Host AI Agent API with Railway
- **Short description:** OpenAI agent with tool calling — prompt in, answer and tool trace out.
- **Category:** AI
- **Overview:** paste `README.md`

## Services

| Service | Source | Volume | Public HTTP |
| --- | --- | --- | --- |
| AI Agent API | GitHub repo (this folder) | — | Yes |

## Variables — AI Agent API

| Variable | Value | Secret | Description |
| --- | --- | --- | --- |
| `OPENAI_API_KEY` | (user supplied) | Yes | OpenAI API key |
| `OPENAI_MODEL` | `gpt-4o-mini` | No | Model with tool support |
| `API_KEY` | `${{secret(32)}}` | Yes | `X-API-Key` for `/v1/agent` |
| `MAX_TOOL_ROUNDS` | `5` | No | Max tool loop iterations |

## Settings — AI Agent API

- Healthcheck: `/health`
- Mark `OPENAI_API_KEY` as **required** at deploy time
