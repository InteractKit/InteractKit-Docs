# InteractKit Documentation

Source documentation for the InteractKit SDK — a Go framework for building real-time voice AI agents.

These markdown files are used for generating the official documentation site.

## Structure

```
docs/
├── getting-started/       # Installation, quickstart, prerequisites
├── architecture/          # Pipeline design, handler lifecycle, event system
├── handlers/              # Per-handler reference (VAD, STT, LLM, TTS, etc.)
├── services/              # Provider integration guides (Deepgram, OpenAI, etc.)
├── transports/            # Transport setup (LiveKit, Daily, Twilio, WebSocket)
├── configuration/         # settings.json, env vars, session API
├── features/              # Task groups, fillers, interruption, tool calling
└── deployment/            # Docker, production setup
```
