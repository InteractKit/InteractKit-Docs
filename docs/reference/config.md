# Configuration Reference

All configuration structs used to set up handlers, services, and the pipeline.

> Auto-generated from source. Do not edit manually.

## Factory Configuration

### `LLMFactoryConfig`

LLMFactoryConfig holds provider-specific configs for LLM service construction.
// Set exactly one provider config; the rest should be left nil.
// All non-OpenAI providers use the OpenAI-compatible protocol and are
// implemented via the same OpenAI service with a custom base URL.

```go
type LLMFactoryConfig struct {
	TogetherConfig   *openaillm.Config `json:"together,omitempty"`
	GroqConfig       *openaillm.Config `json:"groq,omitempty"`
	DeepSeekConfig   *openaillm.Config `json:"deepseek,omitempty"`
	OpenRouterConfig *openaillm.Config `json:"openrouter,omitempty"`
	FireworksConfig  *openaillm.Config `json:"fireworks,omitempty"`
	CerebrasConfig   *openaillm.Config `json:"cerebras,omitempty"`
	XAIConfig        *openaillm.Config `json:"xai,omitempty"`
	MistralConfig    *openaillm.Config `json:"mistral,omitempty"`
	PerplexityConfig *openaillm.Config `json:"perplexity,omitempty"`
}
```

### `PipelineConfig`

PipelineConfig configures a Pipeline's lifecycle behaviour.

```go
type PipelineConfig struct {
}
```

### `SessionTTSConfig`

SessionTTSConfig bundles TTS handler config with primary and optional fallback service factory configs.

```go
type SessionTTSConfig struct {
	HandlerConfig ttshandler.TTSConfig `json:"handler"`
	// ServiceConfig selects and configures the primary TTS provider.
	// Set exactly one provider field inside TTSFactoryConfig.
	ServiceConfig TTSFactoryConfig `json:"service"`
	// FallbackServiceConfigs is an ordered list of fallback providers tried if the primary fails.
	FallbackServiceConfigs []TTSFactoryConfig `json:"fallbacks,omitempty"`
}
```

### `SessionSTTConfig`

SessionSTTConfig bundles STT handler config with primary and optional fallback service factory configs.

```go
type SessionSTTConfig struct {
	HandlerConfig stthandler.STTConfig `json:"handler"`
	// ServiceConfig selects and configures the primary STT provider.
	// Set exactly one provider field inside STTFactoryConfig.
	ServiceConfig STTFactoryConfig `json:"service"`
	// FallbackServiceConfigs is an ordered list of fallback providers tried if the primary fails.
	FallbackServiceConfigs []STTFactoryConfig `json:"fallbacks,omitempty"`
}
```

### `SessionLLMConfig`

SessionLLMConfig bundles LLM handler config with primary, fallback, and optional filler service factory configs.

```go
type SessionLLMConfig struct {
	HandlerConfig llmhandler.LLMHandlerConfig `json:"handler"`
	// ServiceConfig selects and configures the primary LLM provider.
	// Set exactly one provider field inside LLMFactoryConfig.
	ServiceConfig LLMFactoryConfig `json:"service"`
	// FallbackServiceConfigs is an ordered list of fallback providers tried if the primary fails.
	FallbackServiceConfigs []LLMFactoryConfig `json:"fallbacks,omitempty"`
	// FillerServiceConfig optionally selects a lighter, cheaper model used only for filler
	// word generation. When nil, the primary service handles fillers too.
	FillerServiceConfig *LLMFactoryConfig `json:"filler_service,omitempty"`
}
```

### `SessionContextConfig`

SessionContextConfig bundles context-manager and handler-level context configs.

```go
type SessionContextConfig struct {
	// human-like speech style, etc.).
	ManagerConfig contexthandler.LLMContextManagerConfig `json:"manager"`
	// HandlerConfig holds the initial LLM context (system messages + tools) and optional
	// keep-quiet tool settings applied when BuildHandlers is called.
	HandlerConfig contexthandler.ContextConfig `json:"handler"`
	// TaskGroup is an optional dynamic task group loaded into the context manager at
	// startup. When nil the context manager starts with no task group.
	TaskGroup *contexthandler.TaskGroupConfig `json:"task_group,omitempty"`
	// MCPServers is an optional list of MCP servers to connect to at startup.
	// Their tools are discovered and registered as standard InteractKit tools.
	MCPServers []core.MCPServerConfig `json:"mcp_servers,omitempty"`
}
```

### `SessionConfig`

SessionConfig is the top-level configuration for a complete voice-AI session pipeline.
// It groups TTS, STT, LLM, and context configs — each with primary and fallback services —
// and exposes BuildHandlers to construct all ready-to-wire handlers in a single call.

```go
type SessionConfig struct {
	STT     SessionSTTConfig     `json:"stt"`
	LLM     SessionLLMConfig     `json:"llm"`
	Context SessionContextConfig `json:"context"`
}
```

### `APIKeys`

APIKeys holds API credentials for all supported service providers.
// Pass to SessionConfig.InjectAPIKeys after loading from JSON so that
// secrets are never stored in config files.

```go
type APIKeys struct {
	OpenAI     string // Used for OpenAI LLM provider.
	Together   string // Used for Together AI LLM provider.
	Groq       string // Used for Groq LLM provider.
	DeepSeek   string // Used for DeepSeek LLM provider.
	OpenRouter string // Used for OpenRouter LLM provider.
	Fireworks  string // Used for Fireworks AI LLM provider.
	Cerebras   string // Used for Cerebras LLM provider.
	XAI        string // Used for xAI (Grok) LLM provider.
	Mistral    string // Used for Mistral AI LLM provider.
	Perplexity string // Used for Perplexity LLM provider.
	ElevenLabs string // Used for ElevenLabs TTS provider.
	Cartesia   string // Used for Cartesia TTS provider.
}
```

### `SessionAPIConfig`

SessionAPIConfig describes an HTTP endpoint that returns a SessionConfig JSON payload.
// Called per-job to allow dynamic configuration per call.

```go
type SessionAPIConfig struct {
	URL string `json:"url"`
	// Method is the HTTP method. Defaults to "POST" when Body is set, "GET" otherwise.
	Method string `json:"method,omitempty"`
	// Headers are additional HTTP headers to include in the request.
	Headers map[string]string `json:"headers,omitempty"`
	// Body is an optional JSON body to send with the request.
	Body json.RawMessage `json:"body,omitempty"`
}
```

### `SettingsConfig`

SettingsConfig is the top-level config loaded from settings.json.
// It bundles the transport provider config with an optional HTTP endpoint
// for fetching the per-job SessionConfig.

```go
type SettingsConfig struct {
	Transport TransportFactoryConfig `json:"transport"`
	// SessionAPI, when set, is called per-job to fetch the SessionConfig dynamically.
	SessionAPI *SessionAPIConfig `json:"session_api,omitempty"`
	// Session, when set, provides inline session config directly in settings.json.
	Session *SessionConfig `json:"session_config,omitempty"`
}
```

### `STTFactoryConfig`

STTFactoryConfig holds provider-specific configs for STT service construction.
// Set exactly one provider config; the rest should be left nil.

```go
type STTFactoryConfig struct {
}
```

### `LiveKitProviderConfig`

LiveKitProviderConfig holds JSON-serialisable settings for a LiveKit transport provider.
// Secrets (URL, APIKey, APISecret) can be omitted and injected via InjectProviderKeys.

```go
type LiveKitProviderConfig struct {
	APIKey              string `json:"api_key,omitempty"`
	APISecret           string `json:"api_secret,omitempty"`
	AgentName           string `json:"agent_name,omitempty"`
	Version             string `json:"version,omitempty"`
	MaxJobs             uint32 `json:"max_jobs,omitempty"`
	DevMode             bool   `json:"dev_mode"`
	HTTPPort            int    `json:"http_port,omitempty"`
	DrainTimeoutSeconds int    `json:"drain_timeout_seconds,omitempty"`
}
```

### `DailyProviderConfig`

DailyProviderConfig holds JSON-serialisable settings for a Daily.co transport provider.
// Secrets (APIKey) can be omitted and injected via InjectProviderKeys.

```go
type DailyProviderConfig struct {
	APIBaseURL      string `json:"api_base_url,omitempty"`
	RoomName        string `json:"room_name,omitempty"`
	RoomURLPrefix   string `json:"room_url_prefix,omitempty"`
	ExpirySeconds   int    `json:"expiry_seconds,omitempty"`
	MaxParticipants int    `json:"max_participants,omitempty"`
	Port            int    `json:"port,omitempty"`
	Path            string `json:"path,omitempty"`
	AudioSampleRate int    `json:"audio_sample_rate,omitempty"`
	AudioChannels   int    `json:"audio_channels,omitempty"`
	BotName         string `json:"bot_name,omitempty"`
	IsOwner         bool   `json:"is_owner,omitempty"`
}
```

### `TransportFactoryConfig`

TransportFactoryConfig selects and configures a transport provider.
// Set exactly one provider field.

```go
type TransportFactoryConfig struct {
	DailyConfig   *DailyProviderConfig   `json:"daily,omitempty"`
}
```

### `ProviderKeys`

ProviderKeys holds credentials for transport providers.
// Pass to TransportFactoryConfig.InjectProviderKeys after loading from JSON
// so that secrets are not stored in config files.

```go
type ProviderKeys struct {
	LiveKitAPIKey    string
	LiveKitAPISecret string
	DailyAPIKey      string
}
```

### `TTSFactoryConfig`

TTSFactoryConfig holds provider-specific configs for TTS service construction.
// Set exactly one provider config; the rest should be left nil.

```go
type TTSFactoryConfig struct {
	ElevenLabsConfig *elevenlabs.ElevenLabsTTSConfig `json:"elevenlabs,omitempty"`
	CartesiaConfig   *cartesia.CartesiaTTSConfig     `json:"cartesia,omitempty"`
}
```

## Handler Configuration

<!-- source: handlers/context/context_config.go -->
### `LLMContextManagerConfig`

LLMContextManagerConfig holds configuration for LLMContextManager construction

```go
type LLMContextManagerConfig struct {
	HumanLikeSpeech        bool `json:"human_like_speech"`        // If true, a human-like speech style prompt is appended to all system messages.
}
```

### `ContextConfig`

ContextConfig holds configuration for context handler initialization (keep-quiet tool, etc.)

```go
type ContextConfig struct {
	KeepQuietInstructions string           `json:"keep_quiet_instructions"` // Instructions for the "keep quiet" tool, guiding the LLM on when and how to use it.
	Context               *core.LLMContext `json:"context"`                 // The context to be used by the context handler.
}
```

<!-- source: handlers/llm/llm_config.go -->
### `LLMHandlerConfig`

LLMHandlerConfig holds configuration for the LLM handler

```go
type LLMHandlerConfig struct {
	BreakWords           []string     `json:"break_words"`
	PreEmptiveGeneration bool         `json:"pre_emptive_generation"`
	GenerateFillers      bool         `json:"generate_fillers"`
}
```

<!-- source: handlers/stt/stt_config.go -->
### `STTConfig`

STTConfig holds configuration for the STT handler

```go
type STTConfig struct {

// DefaultConfig returns an STTConfig with sensible defaults
func DefaultConfig() STTConfig {
	return STTConfig{}
}
```

<!-- source: handlers/transport/transport_config.go -->
### `TransportConfig`

TransportConfig holds configuration for the transport handler

```go
type TransportConfig struct {
	OutChannels    int                      `json:"out_channels"`     // Number of channels for outgoing audio
	OutAudioFormat core.AudioEncodingFormat `json:"out_audio_format"` // Encoding format for outgoing audio
}
```

<!-- source: handlers/tts/tts_config.go -->
### `TTSConfig`

```go
type TTSConfig struct {
	BreakWords    []string `json:"break_words"`     // Punctuation and linguistic markers that trigger early flushing of buffered text to TTS.
	MinTextLength int      `json:"min_text_length"` // Minimum text length to trigger TTS generation, useful for filtering out very short inputs that may not be meaningful to speak.
}
```

<!-- source: handlers/vad/vad_config.go -->
### `VADConfig`

```go
type VADConfig struct {
	AllowInterruptions                bool    `json:"allow_interruptions"`                   // If true, interruptions from the user while the bot is speaking are detected and handled.
	VadPatienceIncreaseOnInterruption float32 `json:"vad_patience_increase_on_interruption"` // The amount of time (in seconds) to increase the VAD grace period when an interruption is detected.
}
```

<!-- source: handlers/vector_db/vector_db_config.go -->
### `VectorDBConfig`

```go
type VectorDBConfig struct {
}
```

<!-- source: handlers/context/task_group.go -->
### `TaskVariable`

TaskVariable is a piece of information the LLM must collect during a task.
// For each variable the system auto-generates a set_<Name> tool that the LLM
// calls when it has obtained the value from the user.

```go
type TaskVariable struct {
	// Must be unique across the whole task group.
	Name string `json:"name"`

	// Description is shown to the LLM as the tool's description.
	Description string `json:"description"`

	// Regex is an optional Go regular-expression the value must satisfy.
	Regex string `json:"regex,omitempty"`

	// Enum is an optional allow-list; the value must be one of these strings.
	Enum []string `json:"enum,omitempty"`

	// Example is shown to the LLM as an example value in the tool definition.
	Example string `json:"example,omitempty"`

	// AutoConfirm instructs the system to read the captured value back to the
	// caller and ask them to verify it before continuing. Useful for values
	// that must match exactly (phone numbers, addresses, etc.) where a
	// mishearing would be costly. Typically paired with a Regex constraint.
	AutoConfirm bool `json:"autoconfirm,omitempty"`

	// ConfirmPhrases is an optional list of read-back + verification phrases
	// spoken when autoconfirm is true. Use {{value}} as the placeholder for
	// the captured value. When omitted the system falls back to its built-in
	// confirmation phrase pool.
	ConfirmPhrases []string `json:"confirm_phrases,omitempty"`
}
```

### `TaskDef`

TaskDef describes one step in a task group.

```go
type TaskDef struct {
	ID string `json:"id"`

	// Name is a short human-readable label (shown to the LLM in the prompt).
	Name string `json:"name"`

	// Instructions is injected as a system message while this task is active.
	Instructions string `json:"instructions"`

	// Variables are the pieces of information that must be collected.
	// Completing all variables causes the system to advance to the next task.
	Variables []TaskVariable `json:"variables,omitempty"`

	// DisappearAfterTaskID: this task is skipped once the named task completes.
	DisappearAfterTaskID string `json:"disappear_after_task_id,omitempty"`

	// VisibleToolIDs lists extra tools (by ID) that should be visible while
	// this task is active. These must be pre-registered via RegisterTool.
	VisibleToolIDs []string `json:"visible_tool_ids,omitempty"`

	// VisibleAfterTaskID: this task is hidden until the named task completes.
	VisibleAfterTaskID string `json:"visible_after_task_id,omitempty"`
}
```

### `TaskGroupConfig`

TaskGroupConfig is the root descriptor for a dynamic task group.

```go
type TaskGroupConfig struct {
	Namespace string `json:"namespace"`

	// BaseInstructions are prepended to the initial context system message.
	// They describe the overall goal and are always visible to the LLM.
	BaseInstructions string `json:"base_instructions"`

	// InitialTaskID is the ID of the task to start with.
	InitialTaskID string `json:"initial_task_id"`

	// GlobalTools lists tool IDs that are visible during every task.
	// These must be pre-registered via RegisterTool.
	GlobalTools []string `json:"global_tools,omitempty"`

	// Tasks is the ordered list of all tasks in this group.
	Tasks []TaskDef `json:"tasks"`
}
```

