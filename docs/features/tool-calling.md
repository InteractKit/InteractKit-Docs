# Tool Calling

The LLM handler supports function/tool calling. Register tools in the context configuration, and the LLM can invoke them during a conversation. Results are injected back into context and generation re-triggers automatically.

## Configuration

Define tools in `settings.json` under `context.handler.context.tools`:

```json
"tools": [
  {
    "name": "get_weather",
    "description": "Get current weather for a location",
    "parameters": {
      "type": "object",
      "properties": {
        "location": { "type": "string" }
      },
      "required": ["location"]
    }
  }
]
```

Enable tool calls in the LLM handler:

```json
"llm": {
  "handler": {
    "allow_tool_calls": true
  }
}
```
