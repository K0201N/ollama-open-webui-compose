# Ollama Web UI with Docker Compose

This repository provides a Docker Compose setup for running Ollama with Open WebUI, making it easy to deploy and manage an open-source LLM interface.

## Setup and Usage

### Starting the Services

To start both Ollama and Open WebUI services:

```bash
docker compose up -d
```

This will start both services in detached mode. Once running, you can access the Open WebUI interface at http://localhost:3000.

### Stopping the Services

To stop all services:

```bash
docker compose down
```

## GPU Configuration

This Docker Compose setup has GPU support disabled by default.

### Using GPU

If you want to use NVIDIA GPU acceleration, uncomment the deploy section in the ollama service in `compose.yml`:

```yaml
deploy:
  resources:
    reservations:
      devices:
        - driver: nvidia
          count: all
          capabilities: [gpu]
```

**Prerequisites:**

- NVIDIA Container Toolkit must be configured

## Open WebUI Features

Open WebUI provides a user-friendly interface for interacting with Ollama models:

- **Chat Interface**: Intuitive chat interface similar to modern AI assistants
- **Model Selection**: Easy switching between different models
- **Conversation History**: Save and restore previous conversations
- **Parameter Adjustments**: Control temperature, context size, and other generation parameters
- **System Prompts**: Configure custom system prompts for specialized model behavior
- **File Uploads**: Share files with models that support file processing
- **Responsive Design**: Works well on desktop and mobile devices

The WebUI is accessible at <http://localhost:3000> after starting the services.

## Ollama Command Examples

Here are examples of using Ollama commands inside the Docker container:

### Model Management

```bash
# List available models
docker exec -it ollama ollama list

# Download models
docker exec -it ollama ollama pull llama2
docker exec -it ollama ollama pull mistral
docker exec -it ollama ollama pull gemma:2b

# Remove a model
docker exec -it ollama ollama rm llama2
```

### Running Models

```bash
# Basic execution (interactive mode)
docker exec -it ollama ollama run llama2

# One-shot query
docker exec -it ollama ollama run llama2 "Write a weather forecast"

# Run with parameters
docker exec -it ollama ollama run llama2:latest "Write a short story" --temperature 0.7
```

### Model Customization

```bash
# Create a custom model
docker exec -it ollama ollama create mymodel -f Modelfile

# Specify system prompt
docker exec -it ollama ollama run llama2 --system "You are a helpful AI assistant"

# Change context size
docker exec -it ollama ollama run llama2 --context 4096 "Summarize this long passage..."
```

## Resources

- [Ollama Official Website](https://ollama.com)
- [Ollama GitHub Repository](https://github.com/ollama/ollama)
- [Open WebUI GitHub Repository](https://github.com/open-webui/open-webui)
