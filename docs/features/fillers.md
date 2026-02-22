# Filler Generation

Concurrently generates conversational fillers ("Let me check...", "One moment...") while the real LLM response is being produced. Fillers are prepended to the response if the real answer takes too long.

## Configuration

Enable in `settings.json`:

```json
"llm": {
  "handler": {
    "generate_fillers": true
  }
}
```
