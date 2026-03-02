# Co-mind AI n8n Node

Custom n8n community node for integrating with Co-mind AI Server — enabling AI-powered workflow automation with inference, knowledge base (RAG), and more.

## Installation

### Option 1: Existing n8n Docker Compose instance

If you already have n8n running with Docker Compose (e.g. with a volume like `./n8n_data:/home/node/.n8n`):

1. Download the `.tgz` package from [Releases](https://github.com/co-mind-ai/comind-n8n-node-release/releases)

2. Extract the package into the n8n data volume:

```bash
mkdir -p ./n8n_data/nodes/co-mind-ai
tar xzf co-mind-ai-n8n-nodes-comind-ai-0.1.1.tgz --strip-components=1 -C ./n8n_data/nodes/co-mind-ai
```

3. Install and restart:

```bash
docker compose exec n8n sh -c "cd /home/node/.n8n/nodes && npm install ./co-mind-ai"
docker compose restart n8n
```

### Option 2: Fresh n8n with Docker

```bash
# Create n8n data directory and install the package
mkdir -p ~/.n8n/nodes/co-mind-ai
tar xzf co-mind-ai-n8n-nodes-comind-ai-0.1.1.tgz --strip-components=1 -C ~/.n8n/nodes/co-mind-ai

# Fix permissions for Docker's node user (UID 1000)
sudo chown -R 1000:1000 ~/.n8n

# Start n8n
docker run -it --rm --name n8n \
  --network host \
  -e N8N_ENCRYPTION_KEY=my-secret-key-123 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n

# In another terminal, install the custom node inside the container
docker exec n8n sh -c "cd /home/node/.n8n/nodes && npm install ./co-mind-ai"

# Restart n8n to pick up the node
docker restart n8n
```

n8n will be available at **http://localhost:5678**.

### Option 3: With npm on the host

```bash
cd ~/.n8n/nodes
npm install co-mind-ai/comind-n8n-node-release
```

Or from the `.tgz` directly:

```bash
cd ~/.n8n/nodes
npm install /path/to/co-mind-ai-n8n-nodes-comind-ai-0.1.1.tgz
```

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

Check [Releases](https://github.com/co-mind-ai/comind-n8n-node-release/releases) for available versions.
