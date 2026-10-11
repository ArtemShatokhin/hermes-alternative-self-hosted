# What Hermes Agent is, and where the open-source Kortix takes over

Hermes Agent is an open-source personal AI agent built by Nous Research, the project behind the Hermes model family. Its repository calls it "the agent that grows with you," and the description matches the design: an agent tuned for one person, on hardware that person controls. Kortix is the open-source AI Operating System a team moves to when that shape no longer fits.

## The learning loop

Hermes is built around a closed learning loop. It creates skills from experience, improves those skills while it uses them, and nudges itself to persist what it learns. It keeps agent-curated memory, searches its own past conversations with full-text search and language-model summarization, and builds a deepening model of who you are across sessions. Its skills are compatible with the agentskills.io open standard, so a skill is a portable file rather than a private artifact ([Hermes on GitHub](https://github.com/NousResearch/Hermes-Agent)).

For one operator, this is the feature that separates Hermes from a plain chat window. The agent accumulates context about a person and the work that person does, and it carries that context forward on its own.

## Where it lives and what it costs to run

Hermes has two entry points. You start the terminal interface with `hermes`, or you run a gateway process and talk to it from a messaging platform. From one gateway it reaches Telegram, Discord, Slack, WhatsApp, Signal, and the CLI, with voice memo transcription and cross-platform continuity. The terminal interface is a full TUI with multiline editing, slash-command autocomplete, conversation history, and streaming tool output.

It runs on a $5 VPS, a GPU cluster, or serverless infrastructure. Seven terminal backends cover local, Docker, SSH, Singularity, Modal, Daytona, and Vercel Sandbox, and the serverless backends hibernate when idle so an agent costs almost nothing between sessions. You can talk to it from Telegram while it works on a cloud VM, so the agent is reachable away from the machine it runs on.

## Which model, and what it can schedule

Hermes is model-agnostic. It works with Nous Portal, OpenRouter, OpenAI, your own endpoint, and others, and you switch with `hermes model` and no code changes. It ships more than 40 tools behind a toolset system, and it can spawn isolated subagents for parallel workstreams. A built-in cron scheduler runs automations in natural language and delivers the result to any platform, so daily reports, nightly backups, and weekly audits run unattended.

## The design boundary: one operator

Everything above is built for a single person. The memory is that person's context, the configuration sits on the machine that person runs, and the security model is command approval and DM pairing. There is no tenancy, no role model, and no shared audit trail, because there is no second person to govern.

That boundary is not a flaw in Hermes. It is the shape of a personal agent, and it is why Hermes is good at being an always-on companion.

## When a team needs a platform

A team that shares an agent needs different things. It needs least privilege, isolation between tasks, a record of who did what, and one place every member's agent can run from. That is the job Kortix is built for, and it is why a team reaches for an alternative once several people steer the same work.

Kortix keeps the open-source values and adds the company layer. The agents, skills, memory, and connectors live in one git repo the team owns. One isolated sandbox per session means a task cannot reach another task. Per-resource permissions for people and agents, roles, groups, and an audit trail answer who may do what. Approval gates you set, off until you set them, and a change request a person approves put a review between an agent and the work that lands. The head-to-head is in [Kortix vs Hermes](kortix-vs-hermes.md), and the stack is in the [self-hosting guide](self-hosting-hermes-alternative.md).

Read the code behind either one: [Hermes on GitHub](https://github.com/NousResearch/Hermes-Agent) and [Kortix on GitHub](https://github.com/kortix-ai/suna). Both are open source: read them, fork them, audit them.
