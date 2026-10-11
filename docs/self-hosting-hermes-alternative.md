# Self-host an open-source Hermes alternative: the Kortix setup guide

Kortix is the open-source AI Operating System, and you can run it on your own box as one Docker Compose stack. This guide takes a bare Linux server and turns it into an instance your team owns, with your own model keys and the work running on isolated cloud computers. Every command here is the one you type; substitute your own domain and email.

## What you actually run

A self-hosted Kortix is one Docker Compose stack: the frontend, the API, the LLM gateway, and the Supabase distribution. Agent sessions run on a separate sandbox provider, so the control plane and the work stay apart. The default provider is Daytona; Platinum and E2B are also supported. The stack has no Redis and no separate worker.

## Before you start

- A bare Linux box. The one-shot bootstrap script is Linux only. On another operating system, install the CLI directly and use the manual path.
- A domain with an A/AAAA record for the domain and for `api.<domain>`, both pointing at the box's IP.
- Ports 80 and 443 open. The bundled Caddy proxy uses them to issue a TLS certificate.

## Step 1: bootstrap the box in one command

On a clean Linux host, a one-shot bootstrap script installs Docker, installs the `kortix` CLI, and starts the stack. It takes your domain and an email for the TLS certificate. The exact script URL is published in the Kortix self-hosting docs. If you prefer each step by hand, use the manual path next.

## Step 2: the manual path

If you want each step by hand, or you are not on Linux, install the CLI and initialize the instance:

```bash
# Install the CLI
curl -fsSL https://kortix.com/install | bash

# Create the A/AAAA records for your domain and api.<domain>, open ports 80 and 443
kortix self-host init --domain kortix.example.com

# Start the stack
kortix self-host start
```

While the stack starts, `kortix self-host status`, `kortix self-host logs`, and `kortix self-host doctor` show what is happening.

## Evaluation mode with no domain

To try the stack without a domain, start it behind a Cloudflare tunnel instead:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so this mode is for evaluation, not production.

## Step 3: connect the sandbox provider and a model key

After the stack is up, run the interactive configuration prompt:

```bash
kortix self-host configure
```

It asks for the sandbox provider key and, optionally, a managed-git token. Then sign up in the dashboard and connect your own LLM key in the model picker. A self-hosted instance uses your own key by default. The first run asks six things and no model key, GitHub connects in the dashboard under Settings, and models are BYOK in the app.

For models, you can bring any provider with your own keys, use the ChatGPT plan you already pay for, or sign in with your OpenCode Console account for OpenCode Zen and Go. Kortix is model-agnostic, so you pick the model per agent, per session, or per message.

## Raise the API memory limit when you need to

Each API container has a 640 MiB memory limit by default. Keep this default on an 8 GiB host. On a 16 GiB host, raise it to 1 GiB when API traffic reaches the default limit:

```bash
kortix self-host env set KORTIX_API_MEMORY_LIMIT=1024m
docker stats --no-stream
```

## Updates

Every instance updates itself automatically. To pin an exact version instead:

```bash
kortix self-host update --tag 0.9.84
```

Turn the updater off with `--auto-update off`.

## Backups

Kortix has no separate backup system. Each instance stores its data as two directories under `~/.config/kortix/self-host/<instance>/`: `volumes/db/data` holds the Postgres database and `volumes/storage` holds file storage. The instance's `.env` file holds every secret and signing key it uses. Back up all three before you run a destructive command.

## What the stack gives a team that a personal agent does not

Hermes is built for one operator, and its own repository documents the learning loop, the messaging gateway, and the terminal backends that make it good at that. When several people steer the same agent, the questions change. Kortix answers them inside the platform:

- One isolated sandbox per session. Each session has its own isolated machine and branch.
- Per-resource permissions for people and agents. Roles, groups, and an audit trail.
- Approval gates you set. Off until you set them.
- Session work reaches main through a change request. Merge is default-deny for agents.
- SAML 2.0 single sign-on and SCIM 2.0.
- Secrets are encrypted at rest with a key per project.
- 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP. Connector credentials are brokered server-side and never enter the machine.

You set each connector tool to Allow, Ask or Block, down to the arguments of each call. An Ask holds the call until a person approves it, then the agent resumes.

## One thing to plan for: the instance stays reachable

The sandbox provider is remote, so the instance must stay reachable for the sandbox to call back, and `kortix self-host start` pulls its images from docker.io. Plan for a host with outbound network access rather than a fully disconnected one.

## Where a personal agent stops

A personal agent on a laptop shares that person's filesystem and credentials, and its memory is one operator's context. A Kortix session starts clean, runs on its own machine and branch, and lands nothing until a person reviews the change request. The config lives in a repo the company owns, so memory becomes something the team versions rather than something one agent accumulates alone. That boundary is the reason a team self-hosts.
