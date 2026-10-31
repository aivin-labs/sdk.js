# `signal` — Proactive Reaction & Cognitive Synapse

Inject cognitive signals into the agent's proactive reaction network to trigger autonomous behaviors.

```typescript
import { signal } from '@aivin-labs/sdk';
```

## Methods

| Method | Parameters | Returns | Description |
|---|---|---|---|
| `emit` | `nodeId: string, energy?: number` | `Promise<{ accepted: boolean }>` | Emit an energy impulse to a cognitive node to trigger proactive behaviors. `energy` is clamped to $\le 1$. |
| `stimulate` | `nodeId: string, energy?: number` | `Promise<{ accepted: boolean }>` | Stimulate a cognitive node in the synapse perception network. |

## Examples

```typescript
import { signal } from '@aivin-labs/sdk';

// Signal a critical event to the perception engine
await signal.emit('order.fraud_alert', 0.9);

// Stimulate a cognitive topic node
await signal.stimulate('support.urgent_queue');
```
