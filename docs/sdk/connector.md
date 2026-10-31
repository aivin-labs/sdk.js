# `connector` — Connected Account Credentials

Credential broker connecting your plugin to third-party integrations (Stripe, Google Workspace,
Notion, GitHub, etc.) that the workspace administrator has authenticated.

```typescript
import { connector } from '@aivin-labs/sdk';
```

## Methods

| Method | Parameters | Returns | Description |
|---|---|---|---|
| `getToken` | `params: { provider: string; scopes?: string[]; purpose?: string }` | `Promise<CredentialResult>` | Resolve a connected credential token (ambient/shared within the workspace). |
| `requestAccess` | `params: { provider: string; scopes?: string[]; purpose?: string }` | `Promise<CredentialResult>` | Request credential access with an explicit user confirmation/consent prompt. |

## Return Type: `CredentialResult`

```typescript
export interface CredentialResult {
  status: 'ok' | 'needs_auth' | 'needs_scope_upgrade' | 'rate_limited' | 'error';
  provider: string;
  token?: string;
  refresh_token?: string;
  expires_at?: number;
  auth_url?: string;
  metadata?: Record<string, any>;
  error?: string;
}
```

## Examples

### Resolving a token for an API call

```typescript
import { connector } from '@aivin-labs/sdk';

const cred = await connector.getToken({ provider: 'stripe' });

if (cred.status !== 'ok' || !cred.token) {
  throw new Error(`Stripe connection not available: ${cred.status}`);
}

// Use cred.token directly with the provider SDK or HTTP client
```

### Explicit user confirmation for sensitive operations

```typescript
import { connector } from '@aivin-labs/sdk';

const cred = await connector.requestAccess({
  provider: 'google',
  scopes: ['https://www.googleapis.com/auth/calendar.events'],
  purpose: 'Schedule a customer onboarding meeting',
});

if (cred.status === 'ok') {
  // Access approved by the user
}
```
