# Bell — Event Bus for Multi-Agent Communication

> Event-driven communication bus for multi-agent orchestration

## Overview

Bell is the **event bus** that enables inter-agent communication in the GenAI system. All agents communicate via publish/subscribe through Bell.

## Core Concepts

### Message Types
| Type | Direction | Use Case |
|------|-----------|----------|
| **Event** | Agent → Bus → Other Agents | Notifications, state changes |
| **Request** | Agent → Orchestrator → Agent | Task delegation |
| **Response** | Agent → Agent (via bus) | Result delivery |

### Pub/Sub Model
```go
// Agent publishes
bell.Publish("experiment.completed", payload)

// Agent subscribes
bell.Subscribe("experiment.completed", func(payload) {
    // handle event
})
```

### Topic Structure
```
agent.<name>.<action>     # agent-specific events
system.<component>.<event> # system-wide events
ml.<task>.<stage>         # ML-specific events
```

## Features

- **Async messaging** — Non-blocking event propagation
- **Topic filtering** — Agents subscribe to relevant topics only
- **Message persistence** — Optional queue for durability
- **Cross-machine support** — Network-transparent via adapter

## Related

- [Orchestrator](https://github.com/genai-io/orchestrator) — Manages agents via Bell
- [ML Researcher](https://github.com/genai-io/ml-researcher) — Uses Bell for experiment events
- [Spec](https://github.com/genai-io/spec) — Overall architecture
