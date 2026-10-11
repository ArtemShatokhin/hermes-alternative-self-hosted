# Migrating from Hermes to Kortix: what moves, and in what order

Kortix is the open-source AI Operating System, and migrating a team from Hermes to it is not a rewrite. Hermes is a personal agent that accumulates skills and memory for one operator; Kortix is a platform where the same work runs for a team, with the configuration in a repo the team owns. The move is about where the configuration and memory live, and who approves a change.

The order matters. Move the work first, then the connectors, and add the governance layer last, once the agents already run.

## What actually moves

Three things change hands: the prompts and skills, the memory and context, and the connectors. Everything else is new because the team needs it.

## Skills and prompts

Hermes builds skills from experience and stores them as files, and its skills follow the agentskills.io open standard ([Hermes on GitHub](https://github.com/NousResearch/Hermes-Agent)). In Kortix an agent is `agents/<name>.md` for its behavior, plus an `agents.<name>` block in `kortix.yaml` for its governance. The behavior file is markdown, so the body of a prompt moves with edits. The governance block is the new part: it names which connectors the agent may reach and which secrets it may use. Copy the prose, then declare the reach.

## Memory and context

Hermes keeps a deepening model of the person it serves, curated across sessions with periodic nudges. Kortix company memory is the living company brain, plain files today, held in the same repo as the agents. That is the shift from one operator's context to shared context: memory becomes something the team reviews and versions rather than something one agent accumulates alone.

## Connectors

Hermes ships more than 40 tools behind its own toolset system. Kortix reaches 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP, and connector credentials are brokered server-side and never enter the machine. Re-point each connector once. The catalog covers the messaging and work apps a team already runs, so a Hermes tool usually has a home in the same list.

## The governance layer you gain

This is the part Hermes was not built for, and it is the reason a team makes the move. Add it once the agents already run, so the work does not wait on access design.

- One isolated sandbox per session. Each session has its own isolated machine and branch.
- Per-resource permissions for people and agents. Roles, groups, and an audit trail.
- Approval gates you set. Off until you set them.
- Session work reaches main through a change request, and merge is default-deny for agents.
- SAML 2.0 single sign-on and SCIM 2.0.
- Secrets are encrypted at rest with a key per project.

With that in place, the work scales with the team: thousands of agents in parallel on one config, each on its own cloud computer.

## What stays with Hermes

Nothing about the move requires giving Hermes up. It is a fine personal agent: run it on a $5 VPS or a GPU cluster, talk to it from Telegram while it works on a cloud VM, switch models with `hermes model`. A personal agent and a governed company platform are different jobs, and a person on the team can keep using Hermes for their own work while the team runs Kortix.

## Questions about the move

Can we run Hermes and Kortix at the same time? Yes. Hermes is a personal agent for one operator and Kortix is a platform for a team. Nothing about the move stops anyone using Hermes for their own work.

Do our agents have to be rewritten? Most of a prompt carries over. The behavior file in Kortix is markdown, so a prompt body moves with edits. The `kortix.yaml` governance block is the new part.

Where does our memory end up? Company memory is plain files in the git repo you own, versioned and diffable, kept beside the agents.

What should we move first? Prompts and skills, then connectors, then the governance layer, once the work already runs. Start with one job and one repo you own, then bring the rest of the team.
