# `state` — Plugin Runtime State Storage

Persist and read accumulated state across multiple executions of your plugin within a workspace.

```typescript
import { state } from '@aivin-labs/sdk';
```

Unlike `config` (which is user-configured and set via workspace administration), `state` is runtime data
your plugin accumulates as it executes (e.g. sync cursors, discovered options, cache timestamps).

## Methods

| Method | Parameters | Returns | Description |
|---|---|---|---|
| `get` | `pluginId?: string` | `Promise<T \| null>` | Read the plugin's accumulated state from the current workspace. |
| `set` | `data: Record<string, any>, pluginId?: string` | `Promise<any>` | Shallow-merge new keys into the plugin's workspace state. |

## Examples

```typescript
import { state } from '@aivin-labs/sdk';

// Read existing state
const current = await state.get<{ lastSyncTime: number }>();
console.log('Last sync timestamp:', current?.lastSyncTime);

// Update state
await state.set({
  lastSyncTime: Date.now(),
  processedItems: 42,
});
```
