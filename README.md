# Co-mind AI n8n Node

Custom n8n community node for integrating with Co-mind AI Server — enabling AI-powered workflow automation with inference, knowledge base (RAG), and more.

## Installation

```bash
# In your n8n custom nodes directory
cd ~/.n8n/nodes
npm install co-mind-ai/comind-n8n-node-release
```

Pin a specific version tag:

```bash
npm install co-mind-ai/comind-n8n-node-release#v0.1.0
```

Or install from a `.tgz` package (download from [Releases](https://github.com/co-mind-ai/comind-n8n-node-release/releases)):

```bash
cd ~/.n8n/nodes
npm install /path/to/co-mind-ai-n8n-nodes-comind-ai-0.1.1.tgz
```

Or without npm — just extract and run:

```bash
mkdir -p ~/.n8n/nodes/co-mind-ai
tar xzf co-mind-ai-n8n-nodes-comind-ai-0.1.1.tgz --strip-components=1 -C ~/.n8n/nodes/co-mind-ai
```

## n8n Setup

### Existing n8n instance (Docker Compose)

If you already have n8n running via Docker Compose, copy the node into the mounted `.n8n` volume:

```bash
# Extract the package into n8n's custom nodes directory
mkdir -p ~/.n8n/nodes/co-mind-ai
tar xzf co-mind-ai-n8n-nodes-comind-ai-0.1.1.tgz --strip-components=1 -C ~/.n8n/nodes/co-mind-ai

# Restart n8n to pick up the new node
docker compose restart n8n
```

> **Note:** Make sure your `docker-compose.yml` mounts `~/.n8n` as a volume (e.g. `- ~/.n8n:/home/node/.n8n`).

### Fresh installation

```bash
# Create custom nodes directory
mkdir -p ~/.n8n/nodes

# Install the package
cd ~/.n8n/nodes
npm install co-mind-ai/comind-n8n-node-release

# Fix permissions for Docker's node user (UID 1000)
sudo chown -R 1000:1000 ~/.n8n

# Start n8n
docker run -it --rm --name n8n \
  --network host \
  -e N8N_ENCRYPTION_KEY=my-secret-key-123 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

n8n will be available at **http://localhost:5678**.

## Configuring Credentials

1. Open n8n at http://localhost:5678
2. Go to **Credentials** → **Add Credential**
3. Select **"Co-mind Server API"**
4. Enter:

| Field | Value |
|---|---|
| API Base URL | Your Co-mind AI platform URL |
| Email | Your account email |
| Password | Your account password |
| Allowed HTTP Request Domains | `All` |

5. Click **Save** — you should see: `Connection tested successfully`

## Documentation

See the [`docs/`](docs/) folder for detailed documentation on available resources and operations.

## Available Resources

| Resource | Description |
|---|---|
| Inference | Run AI inference tasks |
| Knowledge Base | Manage knowledge bases for RAG |
| Chat Session | Manage chat sessions |
| Echo Transcription | Speech-to-text transcription |
| Echo TTS | Text-to-speech generation |
| Custom | Custom API requests |
| Discovery | Service discovery |
| Document Analyzer | Analyze documents |
| Researcher | AI-powered research |
| Sanitizer | Content sanitization |

## Version History

Check [tags](https://github.com/co-mind-ai/comind-n8n-node-release/tags) for available versions.
