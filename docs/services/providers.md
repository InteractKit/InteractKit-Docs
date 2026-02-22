# Service Provider Reference

Configuration options for each supported service provider.

> Auto-generated from source. Do not edit manually.

## Cartesia

### TTS

CartesiaTTSConfig holds configuration for the Cartesia TTS service.

```go
type CartesiaTTSConfig struct {
	BaseURL    string `json:"base_url"`
	ModelID    string `json:"model_id"`
	VoiceID    string `json:"voice_id"`
	Language   string `json:"language"`
	APIVersion string `json:"api_version"`
}
```

## Deepgram

### STT

DeepgramConfig holds configuration options for Deepgram STT

```go
type DeepgramConfig struct {
	BaseURL         string            `json:"base_url"`
	Model           string            `json:"model"`
	Language        string            `json:"language"`
	InterimResults  bool              `json:"interim_results"`
	Punctuate       bool              `json:"punctuate"`
	SmartFormat     bool              `json:"smart_format"`
	Diarize         bool              `json:"diarize"`
	ProfanityFilter bool              `json:"profanity_filter"`
	Redact          string            `json:"redact"`
	Numerals        bool              `json:"numerals"`
	Endpointing     any               `json:"endpointing"` // Can be string, int, or bool
	VadEvents       bool              `json:"vad_events"`
	UtteranceEndMs  any               `json:"utterance_end_ms"`
	Multichannel    bool              `json:"multichannel"`
	Keywords        []string          `json:"keywords"`
	Keyterms        []string          `json:"keyterms"`
	Search          []string          `json:"search"`
	Replace         any               `json:"replace"`
	Callback        string            `json:"callback"`
	CallbackMethod  string            `json:"callback_method"`
	Extra           map[string]string `json:"extra"`
	Tag             []string          `json:"tag"`
	DetectEntities  bool              `json:"detect_entities"`
	Dictation       bool              `json:"dictation"`
	MipOptOut       bool              `json:"mip_opt_out"`
	Version         string            `json:"version"`
}
```

### TTS

DepgramTTSConfig holds configuration for the Deepgram TTS service

```go
type DepgramTTSConfig struct {
	BaseURL string `json:"base_url"`
	Model   string `json:"model"`
}
```

## Elevenlabs

### TTS

ElevenLabsTTSConfig holds configuration for the ElevenLabs TTS service

```go
type ElevenLabsTTSConfig struct {
	BaseURL string `json:"base_url"`
	VoiceID string `json:"voice_id"`
	ModelID string `json:"model_id"`

	// Voice settings
	Stability       float64 `json:"stability"`
	SimilarityBoost float64 `json:"similarity_boost"`
}
```

## Openai

### LLM

## Transports

### Daily

RoomConfig is the request body for POST /rooms.

```go
type RoomConfig struct {
	Privacy    string          `json:"privacy,omitempty"`
	Properties *RoomProperties `json:"properties,omitempty"`
}
```

MeetingTokenConfig is the request body for POST /meeting-tokens.

```go
type MeetingTokenConfig struct {
}
```

Config holds configuration for the Daily.co transport.

```go
type Config struct {
	APIKey string `json:"api_key,omitempty"`

	// Daily API base URL (default: https://api.daily.co/v1).
	APIBaseURL string `json:"api_base_url,omitempty"`

	// Room configuration.
	RoomName        string `json:"room_name,omitempty"`
	RoomURLPrefix   string `json:"room_url_prefix,omitempty"`
	ExpirySeconds   int    `json:"expiry_seconds,omitempty"`
	MaxParticipants int    `json:"max_participants,omitempty"`

	// WebSocket relay server configuration.
	Port            int    `json:"port,omitempty"`
	Path            string `json:"path,omitempty"`
	ReadBufferSize  int    `json:"read_buffer_size,omitempty"`
	WriteBufferSize int    `json:"write_buffer_size,omitempty"`
	MaxMessageSize  int64  `json:"max_message_size,omitempty"`

	// Audio configuration.
	AudioSampleRate int `json:"audio_sample_rate,omitempty"`
	AudioChannels   int `json:"audio_channels,omitempty"`

	// TLS configuration.
	EnableTLS   bool   `json:"enable_tls,omitempty"`
	TLSCertFile string `json:"tls_cert_file,omitempty"`
	TLSKeyFile  string `json:"tls_key_file,omitempty"`

	// Bot participant name in the Daily room.
	BotName string `json:"bot_name,omitempty"`
	// Whether the bot token has owner privileges.
	IsOwner bool `json:"is_owner,omitempty"`
}
```

### Livekit

```go
type Config struct {
	APIKey       string
	APISecret    string
	AgentName    string
	Version      string
	MaxJobs      uint32
	DevMode      bool
	Logger       *core.Logger
	DrainTimeout time.Duration

	// Optional
	JobTypes    []livekit.JobType
	HTTPPort    int
	Permissions *livekit.ParticipantPermission
}
```

### Twilio

Config holds the configuration for Twilio WebSocket services

```go
type Config struct {
	Port int `yaml:"port" json:"port" default:"8080"`

	// WebSocket endpoint path
	Path string `yaml:"path" json:"path" default:"/media-stream"`

	// Enable authentication
	EnableAuth bool `yaml:"enable_auth" json:"enable_auth" default:"false"`

	// Authentication token for webhook validation
	AuthToken string `yaml:"auth_token" json:"auth_token"`

	// Read buffer size for WebSocket connections (bytes)
	ReadBufferSize int `yaml:"read_buffer_size" json:"read_buffer_size" default:"4096"`

	// Write buffer size for WebSocket connections (bytes)
	WriteBufferSize int `yaml:"write_buffer_size" json:"write_buffer_size" default:"4096"`

	// Maximum message size (bytes)
	MaxMessageSize int64 `yaml:"max_message_size" json:"max_message_size" default:"65536"`

	// Audio sample rate (Hz)
	AudioSampleRate int `yaml:"audio_sample_rate" json:"audio_sample_rate" default:"8000"`

	// Enable TLS/SSL
	EnableTLS bool `yaml:"enable_tls" json:"enable_tls" default:"false"`

	// TLS certificate file path
	TLSCertFile string `yaml:"tls_cert_file" json:"tls_cert_file"`

	// TLS key file path
	TLSKeyFile string `yaml:"tls_key_file" json:"tls_key_file"`
}
```

### Websocket

