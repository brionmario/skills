---
name: thunderid-integrate-react
description: Add ThunderID authentication to a React application using the official @thunderid/react SDK. Use when asked to "integrate ThunderID into React", "add auth to my React app", or "connect ThunderID with React".
license: Apache-2.0
allowed-tools: Bash(npm:*), Bash(npx:*), Bash(pnpm:*), Bash(yarn:*), Bash(bun:*), Read, Write, Edit
metadata:
  author: thunderid
  version: 0.1.0
---

# ThunderID — React Integration

Assumes ThunderID is running at `https://localhost:8090`. If not, run `/install` first.

## Step 1 — Register an Application

1. Open `https://localhost:8090/console` and sign in as `admin` / `admin`
2. Navigate to **Applications → New Application**
3. Fill in:
   - **Name**: your app name
   - **Type**: Single Page Application
   - **Authorized Redirect URL**: `http://localhost:5173/callback`
4. Copy the **Client ID**

### Via the API

First obtain a system API token from the ThunderID console, then:

```bash
curl -kL -X POST https://localhost:8090/applications \
  -H 'Authorization: Bearer <your-system-token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "my-react-app",
    "inboundAuthConfig": [{
      "type": "oauth2",
      "config": {
        "grantTypes": ["authorization_code", "refresh_token"],
        "responseTypes": ["code"],
        "redirectUris": ["http://localhost:5173/callback"],
        "tokenEndpointAuthMethod": "none",
        "publicClient": true,
        "pkceRequired": true
      }
    }]
  }'
```

## Step 2 — Get Your Client ID

Open the ThunderID console at `https://localhost:8090/console`, navigate to **Applications → your app**, and copy the **Client ID**.

## Step 3 — Install

Detect the package manager from lockfiles: `pnpm-lock.yaml` → `pnpm add`, `yarn.lock` → `yarn add`, `bun.lockb` → `bun add`, else `npm install`.

```bash
npm install @thunderid/react
```

## Step 4 — Wrap with Provider

Edit `src/main.jsx` (or `src/main.tsx`), replacing `<your-client-id>` with the Client ID you copied:

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { ThunderIDProvider } from '@thunderid/react'
import App from './App.jsx'
import './index.css'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <ThunderIDProvider
      clientId="<your-client-id>"
      baseUrl="https://localhost:8090"
    >
      <App />
    </ThunderIDProvider>
  </StrictMode>
)
```

## Step 5 — Add Auth UI

```jsx
import {
  SignedIn, SignedOut,
  SignInButton, SignOutButton, Loading,
} from '@thunderid/react'

function App() {
  return (
    <>
      <Loading>
        <div>Loading authentication...</div>
      </Loading>
      <SignedOut>
        <SignInButton>Sign In</SignInButton>
      </SignedOut>
      <SignedIn>
        <SignOutButton>Sign Out</SignOutButton>
      </SignedIn>
    </>
  )
}
```

## Step 6 — Display User Profile

```jsx
import {
  SignedIn, SignedOut,
  SignInButton, SignOutButton, Loading, User,
} from '@thunderid/react'

function App() {
  return (
    <>
      <Loading><div>Loading...</div></Loading>
      <SignedOut><SignInButton>Sign In</SignInButton></SignedOut>
      <SignedIn>
        <SignOutButton>Sign Out</SignOutButton>
        <User>
          {(user) => user && (
            <div>
              <h2>Welcome, {user.name}!</h2>
              <p>{user.email}</p>
            </div>
          )}
        </User>
      </SignedIn>
    </>
  )
}
```

## Step 7 — Run and Verify

```bash
npm run dev
```

Click **Sign In** — you should be redirected to `https://localhost:8090` and returned after login.

## Troubleshooting

**Certificate error** — Visit `https://localhost:8090` in your browser and accept the warning once.

**React 19 Strict Mode double-render** — Expected in development; the SDK handles it internally.
