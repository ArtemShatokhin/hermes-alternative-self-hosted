# Self-host a Hermes alternative: Kortix, the open-source AI Operating System

If your team has outgrown Hermes Agent, a personal agent built for one operator, the next step is a platform the whole company owns. Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. You can self-host it for free as one Docker Compose stack.

This repo is the working guide to that move. It covers what Hermes is, where its design stops, what Kortix adds, how to run the stack on your own box, and what changes when you migrate.

- [Self-hosting guide](docs/self-hosting-hermes-alternative.md): the step-by-step path from a bare Linux server to a running instance.
- [Kortix vs Hermes](docs/kortix-vs-hermes.md): the head-to-head and a short decision path.
- [What Hermes Agent is](docs/hermes-agent-what-it-is.md): the entity, its learning loop, and its boundary.
- [Migrate from Hermes](docs/migrate-from-hermes.md): what moves, in what order.
- [FAQ](docs/faq.md): the short answers a team asks before it switches.

## What Hermes Agent is, and where a personal agent stops

Hermes Agent is an open-source personal AI agent from Nous Research. Its repository describes an agent that grows with you: it creates skills from experience, keeps curated memory across sessions, searches its own past conversations, and reaches you from Telegram, Discord, Slack, WhatsApp, Signal, or a terminal. It runs on a $5 VPS, a GPU cluster, or serverless infrastructure, and you switch models with `hermes model` ([Hermes on GitHub](https://github.com/NousResearch/Hermes-Agent)).

That shape is the point when one person wants an always-on agent on their own machine. Hermes is built for one operator, so a team that shares an agent runs into questions it leaves to you. Who may reach which tool? Which model is allowed? What did the agent do last Tuesday, and who approved it? A personal agent answers none of those in the product. A company platform answers them with roles, scoped tools, and a record of every action.

## What Kortix is

Kortix is the open-source AI Operating System. The agents, their skills, the company memory, the connector configuration, and the triggers are files in one git repo the company owns, versioned and diffable like code. Each session runs on its own isolated cloud computer and branch, and what it produces lands through a change request a person approves. It runs on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free. The code is open source: read it, fork it, audit it, at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## How Kortix compares with the agents a team usually evaluates

| Option | Open source | Designed for | Main job |
| --- | --- | --- | --- |
| Kortix | Yes. Read it, fork it, audit it. | Teams and companies. | Agents across a company, from one repo. |
| Hermes | Yes. | One person. | A personal assistant that learns. |
| OpenClaw | Yes, MIT. | One person, or one shared install. | An assistant in your chat apps. |
| OpenWork | MIT core; org control plane source-available. | One person or a sharing team. | Skills and MCP across your tools. |
| Open WebUI | Yes. | A team that wants chat and knowledge. | A self-hosted chat and RAG workspace. |

Rival details come from each project's own repository, checked October 2026: [Hermes](https://github.com/NousResearch/Hermes-Agent), [OpenClaw](https://github.com/openclaw/openclaw), [OpenWork](https://github.com/different-ai/openwork), and [Open WebUI](https://github.com/open-webui/open-webui). [Kortix on GitHub](https://github.com/kortix-ai/suna) is the source for the Kortix column.

OpenClaw and OpenWork sit closest to Hermes: both are built around one person or one shared install, and OpenWork runs as a desktop app on your own files. Open WebUI is a self-hosted interface for chat, retrieval, and tools, with per-user groups and an optional isolated terminal for agents. It fits a chat and knowledge workspace. Kortix is the platform a company owns when the job is agents that take real actions across a team.

## Self-host in three commands

Kortix self-hosting is one Docker Compose stack: the frontend, the API, the LLM gateway, and the Supabase distribution. Agent sessions run on a separate sandbox provider, so the control plane and the work stay apart. The default provider is Daytona; Platinum and E2B are also supported.

```bash
# 1. Install the CLI
curl -fsSL https://kortix.com/install | bash

# 2. Point DNS at the box, then initialize
kortix self-host init --domain kortix.example.com

# 3. Start the stack
kortix self-host start
```

On a bare Linux box, one command installs Docker, installs the CLI, and starts the stack. The full walkthrough, including the one-shot bootstrap, evaluation mode, the sandbox provider key, memory limits, updates, and backups, is in the [self-hosting guide](docs/self-hosting-hermes-alternative.md).

## What you actually own

Self-hosting puts the whole platform on hardware your team controls. The first run asks six things and no model key, and the stack has no Redis and no separate worker. Any model provider with your own keys, or the ChatGPT plan you already pay for, or sign in with your OpenCode Console account for OpenCode Zen and Go. One isolated sandbox per session. Per-resource permissions for people and agents, with roles, groups, and an audit trail. Approval gates you set, off until you set them. Session work reaches main through a change request, and merge is default-deny for agents.

## Where to go next

If you are still choosing between agents, start with the side-by-side [list of open-source Hermes alternatives](https://hermesalternative.com/hermes-alternatives) and who each one fits. The longer [Kortix vs Hermes comparison](https://hermesalternative.com/kortix-vs-hermes) walks each dimension, from tenancy to history. The browser-friendly [self-hosting walkthrough](https://hermesalternative.com/self-hosting-hermes-alternative) repeats the setup on the site. [Migrate from Hermes](https://hermesalternative.com/migrate-from-hermes) covers what moves and in what order. The [Hermes alternative FAQ](https://hermesalternative.com/faq) answers the short questions a team asks before it switches.

Open source · Any model, your keys · Self-host, VPC, or on-prem
