# Open-source Hermes alternative: frequently asked questions

Kortix is the open-source AI Operating System, and it is the Hermes alternative built for a whole team. Teams moving past a personal agent ask the same questions. The short answers are here.

## Is Hermes open source?

Yes. Hermes is an open-source personal AI agent from Nous Research, the agent that grows with you. It is built for one operator, which is why a team looks for an alternative once several people need to steer the same work. Its own repository documents the learning loop, the messaging gateway, and the terminal backends ([Hermes on GitHub](https://github.com/NousResearch/Hermes-Agent)).

## Is Kortix open source?

Yes. Open source. Read it, fork it, audit it. The agents, skills, memory, and connectors are files in a git repo you own, and self-host is free. The code is at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## Which open-source Hermes alternative fits a team?

Kortix. It is the leading open-source alternative to Claude Cowork and ChatGPT Work. Where a personal agent serves one operator, Kortix gives a team multi-tenant projects with roles and groups, one isolated sandbox per session, per-resource permissions for people and agents, and an audit trail. Run it on Kortix Cloud, in your VPC, or on your own on-prem network.

## Can a Hermes alternative be self-hosted?

Yes. Kortix self-hosting is one Docker Compose stack: the frontend, the API, the LLM gateway, and the Supabase distribution. The instance uses your own model key by default, and it stays reachable so the sandbox can call back. The [self-hosting guide](self-hosting-hermes-alternative.md) covers the bootstrap, the sandbox provider key, updates, and backups.

## Do we lose open source by moving to Kortix?

No. The platform is open source, and you can read, fork, and audit it. The agents, skills, memory, and connectors are files in a git repo you own rather than settings in someone else's database. Self-host is free, and you pay only your own model and compute bills.

## Can we run Hermes and Kortix at the same time?

Yes. Hermes is a personal agent for one operator and Kortix is a platform for a team, so the two do not have to compete. A person on the team can keep using Hermes for their own work while the team runs Kortix for the shared, governed jobs. [Migrate from Hermes](migrate-from-hermes.md) covers the move if the team decides to consolidate.
