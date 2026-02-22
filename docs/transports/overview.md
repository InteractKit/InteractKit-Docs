# Transports

Transports handle the audio I/O layer — receiving audio from callers and sending synthesized speech back.

## Supported Transports

### LiveKit

WebRTC-based transport using LiveKit rooms.

```json
"transport": { "livekit": {} }
```

Requires: `LIVEKIT_URL`, `LIVEKIT_API_KEY`, `LIVEKIT_API_SECRET`

### Daily

WebRTC-based transport using Daily.co rooms.

```json
"transport": { "daily": {} }
```

Requires: `DAILY_API_KEY`

### Twilio

Twilio Media Streams transport for telephony integration.

### WebSocket

Raw WebSocket transport for custom integrations.
