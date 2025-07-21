# VICO

Local VIbe COding assistant. This acronym was suggested by a LLM and I accepted
it without hesitation.

## Setup

Download the models that match the best your performance requirements and your
system capabilities. You can also try other variants, these are just
suggestions. You need an embedding model, a base model and an instruct model.
The models will not be loaded simultaneously.

```bash
ollama=$(docker ps | grep ollama | awk '{print $1}')
docker exec $ollama ollama pull hf.co/nomic-ai/nomic-embed-code-GGUF:Q4_K_M
docker exec $ollama ollama pull qwen2.5-coder:7b-base
docker exec $ollama ollama pull qwen2.5-coder:7b-instruct
```

## Usage

### Continue

Configure [Continue](https://www.continue.dev) with the models downloaded above.

```yaml
name: VICO
version: 1.5.4
schema: v1
models:
  - name: qwen2.5-coder:7b-instruct
    provider: ollama
    model: qwen2.5-coder:7b-instruct
    apiBase: http://localhost:12302
    roles:
      - chat
      - edit
      - apply
  - name: qwen2.5-coder:7b-base
    provider: ollama
    model: qwen2.5-coder:7b-base
    apiBase: http://localhost:12302
    roles:
      - autocomplete
  - name: hf.co/nomic-ai/nomic-embed-code-GGUF:Q4_K_M
    provider: ollama
    model: hf.co/nomic-ai/nomic-embed-code-GGUF:Q4_K_M
    apiBase: http://localhost:12302
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
[http://localhost:12301](http://localhost:12301).
