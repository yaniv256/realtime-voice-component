# realtime-voice-component

React/browser voice controls for tool-constrained UIs built on OpenAI Realtime.

> Warning
> This repository is an open-source reference implementation. It is useful for
> education, demos, and local adoption, but it is not a promise of long-term
> product support or a production-ready UI kit.

## Status

This repo is shared as a GitHub reference implementation. It is licensed under
Apache-2.0, is not currently published to npm, and `package.json` remains marked
as private.

## Requirements

- Node.js 20 or newer
- a React browser app
- a browser runtime with `mediaDevices` and `RTCPeerConnection`
- a backend route that can proxy the browser WebRTC handshake to OpenAI

See [Authentication](./docs/authentication.md) and
[Controller and runtime](./docs/controller-runtime.md) for the runtime details.

## What This Package Is

Use this package when:

- your app defines the exact actions the assistant can take
- tools stay app-owned and narrow
- the UI remains responsible for visible state changes
- you want a React-friendly controller and an optional launcher widget

It is not a general-purpose orchestration framework and it is not a replacement
for raw Realtime transports.

## Choose The Right Layer

Use this package when you want a React/browser layer for voice-driven UI:

- a reusable controller with React bindings
- a packaged launcher widget
- optional visible confirmation via the ghost cursor
- a pattern centered on app-owned tools, not free-form browser automation

Use raw Realtime when you want lower-level transport and session control:

- custom audio handling
- non-React runtimes
- your own UI surface and state model from scratch

Use [`openai-agents-js`](https://github.com/openai/openai-agents-js) when you
need a broader headless SDK:

- agent orchestration and handoffs
- richer hosted-tool and MCP flows
- server-side or multi-runtime agent systems beyond a browser UI package

## Try The Demo

The repo's [`demo/`](./demo) app is the main runnable teaching surface. It shows
a starter theme flow, a multi-step form flow, a shared-state chess flow, shared
controller reuse, and optional wake-word experimentation.

```bash
git clone https://github.com/openai/realtime-voice-component.git
cd realtime-voice-component
npm install
cp demo/.env.example demo/.env.local
# edit demo/.env.local and set OPENAI_API_KEY
npm run demo
```

## Install From A Checkout

The currently supported install path is local checkout installation:

```bash
git clone https://github.com/openai/realtime-voice-component.git
cd realtime-voice-component
npm install
npm run build
```

Then, from your app:

```bash
npm install /absolute/path/to/realtime-voice-component zod
```

Import the package normally:

```ts
import "realtime-voice-component/styles.css";
```

For the first working integration, continue with
[Getting started](./docs/getting-started.md).

## Package Shape

- `defineVoiceTool()` turns a Zod-backed app action into a Realtime function tool.
- `createVoiceControlController()` owns the session, transport, tool execution,
  transcript assembly, and connection lifecycle.
- `useVoiceControl()` binds React to either an external controller or an
  internally owned one.
- `VoiceControlWidget` is a launcher UI on top of the controller.
- `useGhostCursor()` and `GhostCursorOverlay` provide optional visible
  confirmation helpers.

## Recommended Defaults

For most browser apps:

1. proxy the browser SDP plus session config through your own `/session` endpoint
2. register one narrow tool that maps to one real app action
3. start with the theme demo or a small controller-based integration
4. send current UI state back into the session after visible changes

The controller uses Realtime `server_vad` by default. For text and tool-only
sessions, it also sets `interrupt_response: false` so new speech does not cancel
an in-flight text response or tool call.

## Docs

- [Docs overview](./docs/README.md)
- [Getting started](./docs/getting-started.md)
- [Integrating with an existing app](./docs/integrating-with-an-existing-app.md)
- [Architecture choices](./docs/architecture-choices.md)
- [Controller and runtime](./docs/controller-runtime.md)
- [Widget and ghost cursor](./docs/widget-and-cursor.md)
- [Authentication](./docs/authentication.md)
- [Showcase demo architecture](./docs/demo-architecture.md)
- [API reference](./docs/api-reference.md)

## Contributing

Outside contributions are welcome through GitHub issues and pull requests.
Start with [CONTRIBUTING.md](./CONTRIBUTING.md) for the local setup, validation
commands, and the small set of repo conventions that keep the examples and docs
in sync.

Security issues should be reported through the process in
[SECURITY.md](./SECURITY.md), not through public GitHub issues.
