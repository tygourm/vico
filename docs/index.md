# VICO

Local VIbe COding assistant. This acronym was suggested by a LLM and I accepted
it without hesitation.

## Setup

Download the models that match the best your performance requirements and your
system capabilities. You can also try other variants, these are just some
suggestions. You need an embedding model, a base/code model and an instruct
model. The models will not be loaded simultaneously.

```bash
docker exec -it $(docker ps | grep ollama | awk '{print $1}') bash

# Embeddings - 4.4 GB
ollama pull hf.co/nomic-ai/nomic-embed-code-GGUF:Q4_K_M

# Qwen 2.5 Coder 3B - 1.9 GB
ollama pull qwen2.5-coder:3b-base
ollama pull qwen2.5-coder:3b-instruct

# CodeGemma 7B - 5.0 GB
ollama pull codegemma:7b-code
ollama pull codegemma:7b-instruct

# Code Llama 13B - 7.4 GB
ollama pull codellama:13b-code
ollama pull codellama:13b-instruct
```

## Usage

### Continue

Configure [Continue](https://www.continue.dev) with the models downloaded above.

#### Qwen 2.5 Coder 3B

```yaml title="config.yaml"
--8<-- "config.qwencoder.yaml"
```

#### CodeGemma 7B

```yaml title="config.yaml"
--8<-- "config.codegemma.yaml"
```

#### Code Llama 13B

```yaml title="config.yaml"
--8<-- "config.codellama.yaml"
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
