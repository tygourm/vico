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
docker exec $ollama ollama pull snowflake-arctic-embed2:568m
docker exec $ollama ollama pull qwen2.5-coder:3b-base
docker exec $ollama ollama pull mistral:7b-instruct
```

## Usage

### Continue

Configure [Continue](https://www.continue.dev) with the models downloaded above.

```yaml
name: VICO
version: 1.6.3
schema: v1
models:
  - name: mistral:7b-instruct
    provider: ollama
    model: mistral:7b-instruct
    apiBase: http://localhost:12302
    roles: [apply, chat, edit]
    defaultCompletionOptions:
      contextLength: 32768
      temperature: 0.2
  - name: qwen2.5-coder:3b-base
    provider: ollama
    model: qwen2.5-coder:3b-base
    apiBase: http://localhost:12302
    roles: [autocomplete]
  - name: snowflake-arctic-embed2:568m
    provider: ollama
    model: snowflake-arctic-embed2:568m
    apiBase: http://localhost:12302
    roles: [embed]
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
