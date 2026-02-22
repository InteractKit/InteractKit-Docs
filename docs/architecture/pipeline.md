# Pipeline Architecture

## Overview

Audio flows through an ordered handler pipeline:

```
TransportInput → VAD → STT → UserContext → LLM → AssistantContext → TTS → ActivityControl → TransportOutput
```

Each handler runs in its own goroutine. Events flow left-to-right through unbuffered channels, or can be sent to the top of the pipeline to propagate through all handlers.

## Handlers

| Handler | Role |
|---|---|
| **TransportInput/Output** | Receives and sends audio via WebRTC or WebSocket |
| **VAD** | Silero ONNX model detects speech vs. silence |
| **STT** | Streams audio to speech-to-text, emits transcripts |
| **UserContextAggregator** | Appends user messages to LLM context |
| **LLM** | Runs completion with tool calling support |
| **AssistantContextAggregator** | Appends assistant messages, executes tool handlers |
| **TTS** | Converts text chunks to PCM audio |
| **ActivityControl** | Gates audio delivery, handles interruption logic |

## Event System

Handlers communicate through typed events. Each event flows downstream through the pipeline unless a handler consumes it or pushes a new event to the top of the pipeline.
