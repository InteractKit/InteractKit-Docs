# Event Reference

All event types that flow through the InteractKit pipeline.

> Auto-generated from source. Do not edit manually.

## Llm Events

### `LLMGenerateResponseEvent`

```go
type LLMGenerateResponseEvent struct {
}
```

### `LLMResponseStartedEvent`

```go
type LLMResponseStartedEvent struct {

func (e *LLMResponseStartedEvent) GetId() string {
	return "llm.response_started"
}
```

### `LLMResponseChunkEvent`

```go
type LLMResponseChunkEvent struct {
	ConsumeImmediately bool   // If true, the consumer should speak this chunk immediately without buffering.
}
```

### `LLMResponseCompletedEvent`

```go
type LLMResponseCompletedEvent struct {
}
```

### `LLMToolInvocationRequestedEvent`

```go
type LLMToolInvocationRequestedEvent struct {
	Params *map[string]any // Parameters required for the tool invocation.
}
```

### `LLMToolInvocationResultEvent`

```go
type LLMToolInvocationResultEvent struct {
	Result string // Result returned from the tool invocation, typically as a string.
}
```

### `LLMPrepareInterimFillerEvent`

```go
type LLMPrepareInterimFillerEvent struct {
	Context           *core.LLMContext // The current LLM context, which may include previous messages and system instructions.
}
```

### `LLMVariableConfirmRequestEvent`

LLMVariableConfirmRequestEvent is fired by the context handler when an
// autoconfirm variable tool succeeds. The LLM handler intercepts it, bridges
// any already-spoken filler into the confirmation phrase via a small AI call,
// then fires a TTSSpeakEvent with the result. This produces a single natural
// utterance rather than two disconnected spoken fragments.

```go
type LLMVariableConfirmRequestEvent struct {
}
```

## Shared Events

## Stt Events

### `STTInterimOutputEvent`

```go
type STTInterimOutputEvent struct {
}
```

### `STTFinalOutputEvent`

```go
type STTFinalOutputEvent struct {
}
```

## Task Events

### `TaskVariablesEvent`

TaskVariablesEvent is emitted as an IExternalOutputEvent whenever a task
// completes (IsFinal=false) or all tasks in the group finish (IsFinal=true).
// Variables is a flat map of all collected variable values up to that point.

```go
type TaskVariablesEvent struct {
	TaskID    string            `json:"task_id"`
	IsFinal   bool              `json:"is_final"`
	Variables map[string]string `json:"variables"`
}
```

## Transport Events

### `TransportAudioInputEvent`

```go
type TransportAudioInputEvent struct {
}
```

### `TransportVideoInputEvent`

```go
type TransportVideoInputEvent struct {
}
```

### `TransportTextInputEvent`

```go
type TransportTextInputEvent struct {
}
```

## Tts Events

### `TTSOutputEvent`

```go
type TTSOutputEvent struct {
}
```

### `TTSSpokenTextChunkEvent`

```go
type TTSSpokenTextChunkEvent struct {
}
```

### `TTSSpeakingStartedEvent`

started and ended events

```go
type TTSSpeakingStartedEvent struct {
func (e *TTSSpeakingStartedEvent) GetId() string {
	return "tts.speaking_started"
}
```

### `TTSSpeakingEndedEvent`

```go
type TTSSpeakingEndedEvent struct {
func (e *TTSSpeakingEndedEvent) GetId() string {
	return "tts.speaking_ended"
}
```

### `TTSSpeakEvent`

TTSSpeakEvent triggers the TTS to immediately speak the given text,
// bypassing the normal LLM chunk accumulation pipeline.

```go
type TTSSpeakEvent struct {
}
```

## Vad Events

### `VADUserSpeakingEvent`

```go
type VADUserSpeakingEvent struct {

func (e *VADUserSpeakingEvent) GetId() string {
	return "vad.user_speaking"
}
```

### `VADSilenceEvent`

```go
type VADSilenceEvent struct {

func (e *VADSilenceEvent) GetId() string {
	return "vad.silence"
}
```

### `VadInterruptionDetectedEvent`

```go
type VadInterruptionDetectedEvent struct {

func (e *VadInterruptionDetectedEvent) GetId() string {
	return "vad.interruption.detected"
}
```

### `VadInterruptionSuspectedEvent`

```go
type VadInterruptionSuspectedEvent struct {
func (e *VadInterruptionSuspectedEvent) GetId() string {
	return "vad.interruption.suspected"
}
```

### `VadInterruptionConfirmedEvent`

```go
type VadInterruptionConfirmedEvent struct {
func (e *VadInterruptionConfirmedEvent) GetId() string {
	return "vad.interruption.confirmed"
}
```

### `VadUserSpeechEndedEvent`

```go
type VadUserSpeechEndedEvent struct {

func (e *VadUserSpeechEndedEvent) GetId() string {
	return "vad.user_speech.ended"
}
```

### `VadUserSpeechStartedEvent`

```go
type VadUserSpeechStartedEvent struct {

func (e *VadUserSpeechStartedEvent) GetId() string {
	return "vad.user_speech.started"
}
```

## Vectordb Events

### `VectorDBQueryEvent`

```go
type VectorDBQueryEvent struct {
}
```

### `VectorDBQueryResultEvent`

```go
type VectorDBQueryResultEvent struct {
}
```

## Video Events

### `VideoOutputEvent`

```go
type VideoOutputEvent struct {
}
```

## Core Events

### `CriticalErrorEvent`

```go
type CriticalErrorEvent struct {
}
```

### `WarningEvent`

```go
type WarningEvent struct {
}
```

### `EndCallEvent`

EndCallEvent is fired when the agent decides to terminate the session.
// The runner handles it by stopping the pipeline gracefully.

```go
type EndCallEvent struct {
}
```

