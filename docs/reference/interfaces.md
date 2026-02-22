# Interface Reference

Core interfaces that define the InteractKit handler and service contracts.

> Auto-generated from source. Do not edit manually.

## `IEvent`

```go
type IEvent interface {
}
```

## `IExternalOutputEvent`

IExternalOutputEvent is implemented by events that should be routed to the
// ExternalEventHandler instead of flowing up or down the pipeline.

```go
type IExternalOutputEvent interface {
}
```

## `IExternalInputEvent`

IExternalInputEvent is implemented by events that originate outside the
// pipeline. When the ExternalEventHandler receives one, it is pushed to the
// pipeline top so all handlers can observe it.

```go
type IExternalInputEvent interface {
}
```

## `IService`

```go
type IService interface {
		ctx context.Context,
	) error
	Cleanup() error
	Reset() error
}
```

## `IHandler`

```go
type IHandler interface {
		InputChan <-chan *EventPacket,
		outputChan chan<- *EventPacket,
		OutputTopChan chan<- *EventPacket,
		ctx context.Context,
	) error // Initializes the service with the given configuration.
	Start() error // Starts the service's main logic. This is where the service begins processing events.
	HandleEvent(packet *EventPacket) error

	Cleanup() error // Cleans up resources used by the service.
	Reset() error   // Resets the handler to its initial state.
}
```

## `LogWriter`

LogWriter abstracts the destination for session log entries.
// Implementations include SessionLogWriter (file) and WSLogWriter (WebSocket).

```go
type LogWriter interface {
	Close()
}
```

