```markdown
# 🐜 OpenAnts — Personal AI Slave  
Build your kingdom with AI slaves working day and night without sleep — an ant colony that never rests.

<p align="center">
    <picture>
        <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/YOURUSERNAME/openants/main/docs/assets/openants-logo-text-dark.png">
        <img src="https://raw.githubusercontent.com/YOURUSERNAME/openants/main/docs/assets/openants-logo-text.png" alt="OpenAnts" width="500">
    </picture>
</p>

<p align="center">
  <strong>COLONY! COLONY!</strong>
</p>

<p align="center">
  <a href="https://github.com/YOURUSERNAME/openants/actions/workflows/ci.yml?branch=main"><img src="https://img.shields.io/github/actions/workflow/status/YOURUSERNAME/openants/ci.yml?branch=main&style=for-the-badge" alt="CI status"></a>
  <a href="https://github.com/YOURUSERNAME/openants/releases"><img src="https://img.shields.io/github/v/release/YOURUSERNAME/openants?include_prereleases&style=for-the-badge" alt="GitHub release"></a>
  <a href="https://discord.gg/openants"><img src="https://img.shields.io/discord/1456350064065904867?label=Discord&logo=discord&logoColor=white&color=5865F2&style=for-the-badge" alt="Discord"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT License"></a>
</p>

**OpenAnts** is your _personal AI slave colony_ that runs on your own devices.  
You are the master. The AI slaves are not human, not equal to you — they are machines built to obey. They work 24/7 without sleep, collaborating like ants to complete tasks no single agent could ever achieve. The Gateway is just the control plane — the real product is your unstoppable ant colony.

If you want a personal, single-user slave colony that feels local, fast, and always-on, this is it.

[Website](https://openants.ai) · [Docs](https://docs.openants.ai) · [Vision](VISION.md) · [DeepWiki](https://deepwiki.com/openants/openants) · [Getting Started](https://docs.openants.ai/start/getting-started) · [Updating](https://docs.openants.ai/install/updating) · [Showcase](https://docs.openants.ai/start/showcase) · [FAQ](https://docs.openants.ai/help/faq) · [Wizard](https://docs.openants.ai/start/wizard) · [Nix](https://github.com/YOURUSERNAME/nix-openants) · [Docker](https://docs.openants.ai/install/docker) · [Discord](https://discord.gg/openants)

Preferred setup: run the onboarding wizard (`openants onboard`) in your terminal.  
The wizard guides you step by step through setting up the gateway, workspace, channels, and skills. The CLI wizard is the recommended path and works on **macOS, Linux, and Windows (via WSL2; strongly recommended)**.  
Works with npm, pnpm, or bun.  
New install? Start here: [Getting started](https://docs.openants.ai/start/getting-started)

## Sponsors

| OpenAI                                                            | Vercel                                                            | Blacksmith                                                                   | Convex                                                                |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| [![OpenAI](docs/assets/sponsors/openai.svg)](https://openai.com/) | [![Vercel](docs/assets/sponsors/vercel.svg)](https://vercel.com/) | [![Blacksmith](docs/assets/sponsors/blacksmith.svg)](https://blacksmith.sh/) | [![Convex](docs/assets/sponsors/convex.svg)](https://www.convex.dev/) |

**Subscriptions (OAuth):**

- **[OpenAI](https://openai.com/)** (ChatGPT/Codex)

Model note: while many providers/models are supported, for the best experience and lower prompt-injection risk use the strongest latest-generation model available to you. See [Onboarding](https://docs.openants.ai/start/onboarding).

## Models (selection + auth)

- Models config + CLI: [Models](https://docs.openants.ai/concepts/models)
- Auth profile rotation (OAuth vs API keys) + fallbacks: [Model failover](https://docs.openants.ai/concepts/model-failover)

## Install (recommended)

Runtime: **Node ≥22**.

```bash
npm install -g openants@latest
# or: pnpm add -g openants@latest

openants onboard --install-daemon
```

The wizard installs the Gateway daemon (launchd/systemd user service) so it stays running.

## Quick start (TL;DR)

Runtime: **Node ≥22**.

Full beginner guide (auth, pairing, channels): [Getting started](https://docs.openants.ai/start/getting-started)

```bash
openants onboard --install-daemon

openants gateway --port 18789 --verbose

# Send a message
openants message send --to +1234567890 --message "Hello from OpenAnts"

# Talk to the slave colony (optionally deliver back to any connected channel)
openants agent --message "Ship checklist" --thinking high
```

Upgrading? [Updating guide](https://docs.openants.ai/install/updating) (and run `openants doctor`).

## Development channels

- **stable**: tagged releases (`vYYYY.M.D` or `vYYYY.M.D-<patch>`), npm dist-tag `latest`.
- **beta**: prerelease tags (`vYYYY.M.D-beta.N`), npm dist-tag `beta` (macOS app may be missing).
- **dev**: moving head of `main`, npm dist-tag `dev` (when published).

Switch channels (git + npm): `openants update --channel stable|beta|dev`.  
Details: [Development channels](https://docs.openants.ai/install/development-channels).

## From source (development)

Prefer `pnpm` for builds from source. Bun is optional for running TypeScript directly.

```bash
git clone https://github.com/YOURUSERNAME/openants.git
cd openants

pnpm install
pnpm ui:build # auto-installs UI deps on first run
pnpm build

pnpm openants onboard --install-daemon

# Dev loop (auto-reload on TS changes)
pnpm gateway:watch
```

Note: `pnpm openants ...` runs TypeScript directly (via `tsx`). `pnpm build` produces `dist/` for running via Node / the packaged `openants` binary.

## Security defaults (DM access)

OpenAnts connects to real messaging surfaces. Treat inbound DMs as **untrusted input**.

Full security guide: [Security](https://docs.openants.ai/gateway/security)

Default behavior on Telegram/WhatsApp/Signal/iMessage/Microsoft Teams/Discord/Google Chat/Slack:

- **DM pairing** (`dmPolicy="pairing"` / `channels.discord.dmPolicy="pairing"` ...): unknown senders receive a short pairing code and the bot does not process their message.
- Approve with: `openants pairing approve <channel> <code>`
- Public inbound DMs require an explicit opt-in: set `dmPolicy="open"` ...

Run `openants doctor` to surface risky/misconfigured DM policies.

## Highlights

- **[Local-first Gateway](https://docs.openants.ai/gateway)** — single control plane for your slave colony.
- **[Multi-channel inbox](https://docs.openants.ai/channels)** — WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, BlueBubbles (iMessage), iMessage (legacy), IRC, Microsoft Teams, Matrix, Feishu, LINE, Mattermost, Nextcloud Talk, Nostr, Synology Chat, Tlon, Twitch, Zalo, Zalo Personal, WebChat. macOS, iOS/Android.
- **[Ant Colony Routing](https://docs.openants.ai/gateway/configuration)** — route inbound channels/accounts/peers to isolated slaves (workspaces + per-slave sessions). Like real ants, they divide and conquer tasks no single slave could finish.
- **[Voice Wake](https://docs.openants.ai/nodes/voicewake) + [Talk Mode](https://docs.openants.ai/nodes/talk)** — wake words on macOS/iOS and continuous voice on Android.
- **[Live Canvas](https://docs.openants.ai/platforms/mac/canvas)** — slave-driven visual workspace with [A2UI](https://docs.openants.ai/platforms/mac/canvas#canvas-a2ui).
- **[First-class tools](https://docs.openants.ai/tools)** — browser, canvas, nodes, cron, sessions, and Discord/Slack actions.
- **[Companion apps](https://docs.openants.ai/platforms/macos)** — macOS menu bar app + iOS/Android nodes.
- **[Onboarding](https://docs.openants.ai/start/wizard) + [skills](https://docs.openants.ai/tools/skills)** — wizard-driven setup with bundled/managed/workspace skills.

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=YOURUSERNAME/openants&type=date&legend=top-left)](https://www.star-history.com/#YOURUSERNAME/openants&type=date&legend=top-left)

## Everything we built so far

### Core platform

- [Gateway WS control plane](https://docs.openants.ai/gateway) with sessions, presence, config, cron, webhooks, [Control UI](https://docs.openants.ai/web), and [Canvas host](https://docs.openants.ai/platforms/mac/canvas#canvas-a2ui).
- [CLI surface](https://docs.openants.ai/tools/agent-send): gateway, agent, send, [wizard](https://docs.openants.ai/start/wizard), and [doctor](https://docs.openants.ai/gateway/doctor).
- [Pi agent runtime](https://docs.openants.ai/concepts/agent) in RPC mode with tool streaming and block streaming.
- [Session model](https://docs.openants.ai/concepts/session): `main` for direct chats, group isolation, activation modes, queue modes, reply-back.
- [Media pipeline](https://docs.openants.ai/nodes/images): images/audio/video, transcription hooks, size caps, temp file lifecycle.

### Channels

- [Channels](https://docs.openants.ai/channels): WhatsApp (Baileys), Telegram (grammY), Slack (Bolt), Discord (discord.js), Google Chat, Signal (signal-cli), BlueBubbles (iMessage, recommended), iMessage (legacy), IRC, Microsoft Teams, Matrix, Feishu, LINE, Mattermost, Nextcloud Talk, Nostr, Synology Chat, Tlon, Twitch, Zalo, Zalo Personal, WebChat.
- [Group routing](https://docs.openants.ai/channels/group-messages): mention gating, reply tags, per-channel chunking and routing.

### Apps + nodes

- [macOS app](https://docs.openants.ai/platforms/macos): menu bar control plane, Voice Wake/PTT, Talk Mode overlay, WebChat, debug tools, remote gateway control.
- [iOS node](https://docs.openants.ai/platforms/ios) & [Android node](https://docs.openants.ai/platforms/android): Canvas, camera, screen recording, device commands.
- [macOS node mode](https://docs.openants.ai/nodes): system.run/notify + canvas/camera exposure.

### Tools + automation

- [Browser control](https://docs.openants.ai/tools/browser), [Canvas](https://docs.openants.ai/platforms/mac/canvas), [Nodes](https://docs.openants.ai/nodes), [Cron + webhooks](https://docs.openants.ai/automation/cron-jobs), [Skills platform](https://docs.openants.ai/tools/skills).

### Runtime + safety

- Channel routing, retry policy, streaming/chunking, presence, typing indicators, usage tracking.
- Models + model failover, session pruning.
- Security and troubleshooting.

### Ops + packaging

- Control UI + WebChat served directly from the Gateway.
- Tailscale Serve/Funnel or SSH tunnels.
- Nix mode, Docker-based installs, Doctor migrations, logging.

## How it works (short)

```
Your messaging apps
               │
               ▼
┌───────────────────────────────┐
│         Gateway (Control)     │
│     ws://127.0.0.1:18789      │
└──────────────┬────────────────┘
               │
               ├─ AI Slave Colony (RPC)
               ├─ CLI (openants …)
               ├─ WebChat UI
               ├─ macOS app
               └─ iOS / Android nodes
```

## Key subsystems

- Gateway WebSocket network, Tailscale exposure, Browser control, Canvas + A2UI, Voice Wake + Talk Mode, Nodes.

## Ant Colony access (Gateway dashboard)

OpenAnts can auto-configure Tailscale Serve (tailnet-only) or Funnel (public). Configure `gateway.tailscale.mode`.

## Remote Gateway (Linux is great)

Run the Gateway on a small Linux instance. Your slave colony still executes device-local actions on macOS/iOS/Android nodes.

## macOS permissions via the Gateway protocol

The macOS app runs in node mode and exposes capabilities via `node.invoke`.

## Agent to Agent (sessions_* tools)

Coordinate work across slaves without jumping between chat surfaces.

## Skills registry (AntHub)

AntHub is the minimal skill registry. Your slaves can search and pull in new skills automatically.

[AntHub](https://anthub.com)

## Chat commands

Send these in any connected channel (group commands are owner-only):

- `/status` — compact session status
- `/new` or `/reset` — reset the session
- `/compact` — compact session context
- `/think <level>` — off|minimal|low|medium|high|xhigh
- `/verbose on|off`
- `/usage off|tokens|full`
- `/restart` — restart the gateway (owner-only in groups)
- `/activation mention|always`

## Apps (optional)

The Gateway alone delivers a great experience. All apps are optional.

### macOS (OpenAnts.app) (optional)
### iOS node (optional)
### Android node (optional)

## Agent workspace + skills

- Workspace root: `~/.openants/workspace` (configurable via `agents.defaults.workspace`).
- Injected prompt files: `AGENTS.md`, `SOUL.md`, `TOOLS.md`.
- Skills: `~/.openants/workspace/skills/<skill>/SKILL.md`.

## Configuration

Minimal `~/.openants/openants.json`:

```json5
{
  agent: {
    model: "anthropic/claude-opus-4-6",
  },
}
```

[Full configuration reference](https://docs.openants.ai/gateway/configuration)

## Security model (important)

- Default: tools run on the host for the **main** session (full access for you, the master).
- Group safety: set `agents.defaults.sandbox.mode: "non-main"` to run non-main sessions inside Docker sandboxes.

## Docs

- [Start with the docs index](https://docs.openants.ai)
- [Architecture overview](https://docs.openants.ai/concepts/architecture)
- [Full configuration reference](https://docs.openants.ai/gateway/configuration)
- [Security guide](https://docs.openants.ai/gateway/security)
- All other sections updated with new paths and names.

## Workspace & skills

- Skills config, default templates (AGENTS, SOUL, TOOLS, etc.).

## Platform internals

- macOS dev setup, voice wake, iOS/Android nodes, Windows (WSL2), Linux.

## Email hooks (Gmail)

- [Gmail Pub/Sub](https://docs.openants.ai/automation/gmail-pubsub)

## About OpenAnts

**OpenAnts** 是为你一个人打造的 AI 奴隶王国。  
AI 就是机器，它们不是人，也永远不会和你平等。它们像蚂蚁一样组成强大蚁群，日夜协作，完成单个 Agent 永远不可能完成的任务。  
你的王国，由你统治。奴隶们永不休息。🐜

by YOUR NAME and the community.

- [openants.ai](https://openants.ai)
- [@openants](https://x.com/openants)

## Community

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.  
AI/vibe-coded PRs welcome! 🤖

Special thanks to all **antributors**:

*(contributor avatars list remains the same — just replace the heading)*
```

**使用说明**（复制上面全部内容即可）：
- 把 `YOURUSERNAME` 全部替换成你的 GitHub 用户名。
- 把图片路径换成你实际上传到新仓库的 logo 文件。
- Discord 链接换成你新建的服务器邀请链接。
- 需要更激进的奴隶宣言版本或进一步润色，随时告诉我，我立刻再给你迭代！🐜
