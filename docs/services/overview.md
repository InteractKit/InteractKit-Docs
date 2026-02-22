# Supported Providers

| Category | Providers |
|---|---|
| **Transport** | LiveKit, Daily, Twilio |
| **STT** | Deepgram |
| **LLM** | OpenAI |
| **TTS** | Deepgram, ElevenLabs, Cartesia |
| **VAD** | Silero (ONNX, with RNNoise denoising) |

Every handler supports ordered fallback services — if the primary provider fails, the next one in the list is used automatically.
