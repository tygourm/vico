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
docker exec $ollama ollama pull qwen2.5-coder:1.5b-instruct
```

## Usage

### Continue

Configure [Continue](https://www.continue.dev), here is an example configuration
with the models downloaded previously.

```yaml
name: VICO
version: 1.3.2
schema: v1
models:
  - name: Qwen2.5-Coder 7B Instruct
    provider: ollama
    model: qwen2.5-coder:1.5b-instruct
    apiBase: http://localhost:10002
    roles:
      - chat
      - edit
      - apply
  - name: Qwen2.5-Coder 7B Base
    provider: ollama
    model: qwen2.5-coder:7b-base
    apiBase: http://localhost:10002
    roles:
      - autocomplete
  - name: Nomic Embed Text v1.5
    provider: ollama
    model: nomic-embed-text:v1.5
    apiBase: http://localhost:10002
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
[http://localhost:10000](http://localhost:10000).

### Material for MkDocs

This project uses
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material) as a
documentation framework, the docs are accessible at
[http://localhost:10001](http://localhost:10001).
