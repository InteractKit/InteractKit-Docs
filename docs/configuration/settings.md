# Configuration

## settings.json

The main configuration file for the pipeline. It defines the transport, session config, and all handler/service settings.

## Environment Variables

Sensitive values (API keys) are stored in `.env.local`, never in `settings.json`.

```env
LIVEKIT_URL=wss://your-livekit-server
LIVEKIT_API_KEY=...
LIVEKIT_API_SECRET=...
DEEPGRAM_API_KEY=...
OPENAI_API_KEY=...
```

## Session API

Instead of static config, point to an HTTP endpoint that returns per-caller session configuration. This allows dynamic configuration based on the caller.

## Management UI

A web dashboard served at port 8888 for configuring and monitoring the agent. Protect with `INTERACTKIT_API_TOKEN` environment variable for Bearer token auth.

### API Endpoints

| Endpoint | Method | Description |
|---|---|---|
| `/api/settings` | GET / PUT | Read or write settings.json |
| `/api/keys` | GET / PUT | Read or write API keys |
| `/api/restart` | POST | Restart the agent process |
| `/api/status` | GET | Agent process status and PID |
| `/api/sessions` | GET | List all session logs |
| `/api/sessions/{id}/logs` | GET (SSE) | Stream session log entries |
