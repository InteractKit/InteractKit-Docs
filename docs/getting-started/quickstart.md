# Quick Start

## Running with Docker

Pull and run the InteractKit image:

```bash
docker run -p 8888:8888 --env-file .env.local interactkit/interactkit
```

## Environment Variables

Create a `.env.local` file with your API keys:

```env
# Transport (pick one)
LIVEKIT_URL=wss://your-livekit-server
LIVEKIT_API_KEY=...
LIVEKIT_API_SECRET=...

# AI services
DEEPGRAM_API_KEY=...
OPENAI_API_KEY=...

# Runtime paths (included in Docker image)
SILERO_MODEL_PATH=./external/models/silero_vad.onnx
ONNX_RUNTIME_PATH=./external/onnx/libonnxruntime.so
```

## Management UI

Once running, open `http://localhost:8888` to access the management dashboard where you can:

- Configure transport, STT, LLM, and TTS providers
- Manage API keys
- Set up session config and task groups
- Monitor live session logs
- Start/stop the agent
