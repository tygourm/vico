# VICO

Local VIbe COding assistant. This acronym was suggested by a LLM and I accepted
it without hesitation.

## Setup

Start the deployment.

```bash
docker compose up
```

Download the models.

```bash
ollama=$(docker ps | grep ollama | awk '{print $1}')
docker exec $ollama ollama pull nomic-embed-text:v1.5
docker exec $ollama ollama pull qwen2.5-coder:7b-base
docker exec $ollama ollama pull qwen2.5-coder:7b
```

## Usage

### Continue

Configure [Continue](https://www.continue.dev), here is an example configuration
with the models downloaded previously.

```yaml
name: VICO
version: 1.3.0
schema: v1
models:
  - name: Qwen2.5-Coder 7B
    provider: ollama
    model: qwen2.5-coder:7b
    roles:
      - chat
      - edit
      - apply
  - name: Qwen2.5-Coder 7B Base
    provider: ollama
    model: qwen2.5-coder:7b-base
    roles:
      - autocomplete
  - name: Nomic Embed Text v1.5
    provider: ollama
    model: nomic-embed-text:v1.5
    roles:
      - embed
context:
  - provider: code
  - provider: docs
  - provider: diff
  - provider: terminal
  - provider: problems
  - provider: folder
  - provider: codebase
```

### Open WebUI

You can interact with the models from your IDE with Continue, but you can also
use the [Open WebUI](https://openwebui.com) instance accessible at
[http://localhost:8080](http://localhost:8080).

### Material for MkDocs

This project uses
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material) as a
documentation framework, the docs are accessible at
[http://localhost:8000](http://localhost:8000).
