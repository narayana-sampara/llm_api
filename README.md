# LLM API

A small FastAPI service that sends prompts to an Ollama model and returns the generated response.

## Requirements

- Docker
- Docker Compose

## Run With Docker Compose

Start the API and Ollama:

```bash
docker compose up --build
```

The first run pulls the `qwen2.5:0.5b` model into the Ollama volume.

The API is available at:

```text
http://localhost:8000
```

Ollama is exposed at:

```text
http://localhost:11434
```

## Generate Text

Send a prompt to the API:

```bash
curl -X POST http://localhost:8000/generate \
  -H "Content-Type: application/json" \
  -d '{"prompt":"Write one sentence about Docker Compose."}'
```

Example response:

```json
{
  "response": "Docker Compose helps run multi-container applications with a single command."
}
```

## Configuration

The API reads these environment variables:

| Variable | Default | Description |
| --- | --- | --- |
| `OLLAMA_HOST` | `http://localhost:11434` | Ollama server URL |
| `OLLAMA_MODEL` | `qwen2.5:0.5b` | Model used for generation |

In Docker Compose, `OLLAMA_HOST` is set to `http://ollama:11434` so the API container can reach the Ollama container.

## Local Development

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the app locally:

```bash
python main.py
```

If running locally, make sure Ollama is already running and the model is available:

```bash
ollama pull qwen2.5:0.5b
```

