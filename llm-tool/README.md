# llm tool

A command line tool for interacting with models and offering them via a local API
server. Uses:
* Quantized models from 🤗
* [llama-cpp-python's webserver](https://github.com/abetlen/llama-cpp-python#web-server)

Assumes that models are downloaded to `~/.cache/huggingface/hub/` (the default cache path
used by https://github.com/huggingface/huggingface_hub) and only supports `.gguf` files.

If you're using models from TheBloke and you don't specify a filename, we'll attempt to use
the model with 4 bit medium quantization, or you can specify a filename explicitly.

## Install

```bash
pip install .
```

## Model management

### List downloaded models

```bash
llm models list
```

### Download (or update) a model from 🤗

```bash
# Download the default model from the repo
llm models pull TheBloke/Llama-2-13B-Ensemble-v5-GGUF

# Download a specific model from the repo
llm models pull TheBloke/Llama-2-13B-Ensemble-v5-GGUF --filename llama-2-13b-ensemble-v5.Q4_K_S.gguf
```

### Remove a model

```bash
# Remove all models downloaded from the repo
llm models rm TheBloke/Llama-2-13B-Ensemble-v5-GGUF

# Remove a specific model
llm models rm TheBloke/Llama-2-13B-Ensemble-v5-GGUF --filename llama-2-13b-ensemble-v5.Q4_K_S.gguf
```

## Model serving

### Start serving a model

Will download if not already present.

```bash
# Start serving the default model from the repo
llm serving run TheBloke/Llama-2-13B-Ensemble-v5-GGUF

# Start serving a specific model
llm serving run TheBloke/Llama-2-13B-Ensemble-v5-GGUF --filename llama-2-13b-ensemble-v5.Q4_K_S.gguf
```

### Stop serving a model

```bash
# Stop serving all models from the repo
llm serving kill TheBloke/Llama-2-13B-Ensemble-v5-GGUF

# Stop serving a specific model
llm serving kill TheBloke/Llama-2-13B-Ensemble-v5-GGUF --filename llama-2-13b-ensemble-v5.Q4_K_S.gguf
```

### List running models

```bash
llm serving ps
```

## Develop

```bash
python3 -m venv .llm
source .llm/bin/activate
pip install --editable .
```

### Test

```bash
python3 -m unittest
```