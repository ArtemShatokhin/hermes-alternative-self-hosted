# Kortix vs Hermes: an open-source team platform or an open-source personal agent

Kortix is the open-source AI Operating System, and Hermes is an open-source personal AI agent from Nous Research. The choice between them turns on three things: how many people steer the agent, how much you must control what it touches, and whether its history has to survive a review.

Both are open source, both let you bring your own model, and both run on hardware you choose. The difference is scale. Hermes is built for one operator; Kortix is built so a whole team can run agents, govern what they reach, and keep the record.

## Kortix and Hermes, feature by feature

| Dimension | Kortix | Hermes |
| --- | --- | --- |
| Open source | Yes. Read it, fork it, audit it. | Yes. |
| Designed for | Teams and companies. | One person. |
| Tenancy | Multi-tenant projects with roles and groups. | Single operator. |
| Tool policy | Set each tool to Allow, Ask or Block. | Command approval and DM pairing. |
| Isolation | One isolated sandbox per session. | Docker, SSH, or Modal backend. |
| Where config lives | In a git repo you own. | On the machine you run it on. |
| Where it runs | Kortix Cloud, your VPC, or on-prem. | A $5 VPS, a GPU cluster, or serverless. |

Hermes facts come from [its own repository](https://github.com/NousResearch/Hermes-Agent), checked October 2026. Kortix facts come from [Kortix on GitHub](https://github.com/kortix-ai/suna) and the Kortix docs.

## Where Hermes is the right answer

Hermes is a strong personal agent, and its repository is clear about who it serves. It is a self-improving agent with a learning loop: it creates skills from experience, improves them during use, keeps agent-curated memory, and searches its own past sessions for context ([Hermes on GitHub](https://github.com/NousResearch/Hermes-Agent)). It reaches you from Telegram, Discord, Slack, WhatsApp, Signal, or a terminal through a single gateway process. It runs on a $5 VPS, a GPU cluster, or serverless infrastructure, and you switch models with one command.

If one person wants an always-on agent on their own machine, Hermes is built for exactly that, and it does it without asking you to run a company platform.

## Where Kortix takes over

The moment more than one person steers the agent, Hermes's shape works against you. Kortix answers the questions a team has to ask, and each answer sits in the product rather than in a wiki.

Who may reach which tool? You set each tool to Allow, Ask or Block, down to the arguments of each call, and an Ask holds the call until a person approves it. Where does the work run? One isolated sandbox per session, each on its own branch, so a session can install, run and break anything while only what it commits survives. What happened, and who signed off? Session work reaches main through a change request, and every action is recorded. Who is allowed in? Roles, groups, and an audit trail, with SAML 2.0 single sign-on and SCIM 2.0.

The configuration is the other half. In Kortix the company is one git repo you own: the agents, their skills, the memory, the connector configuration, and the triggers are files, versioned and diffed like code. In Hermes the configuration sits on the machine you run it on, which is one operator's machine.

## The line, stated plainly

Choose Hermes when the user is a person: a private agent on your own machine, in your own chat apps, improving its own skills. Choose Kortix when the user is a team or a company: shared projects with roles, scoped tools, isolation per session, and a reviewed history.

They are two sizes of the same idea, an agent for one and a platform for many. A person can run Hermes while the team runs Kortix; the two do not have to compete. When the team side is the side that matters, Kortix is the open-source platform to run on Kortix Cloud, in your VPC, or on your own on-prem network, with self-host free.

## A short decision path

If you are one person and want an agent on your own machine, use Hermes. If two or more people will steer the agent, or its history has to survive a review, move to a platform. Self-host Kortix or run it on the cloud, and keep every change reviewed. The [self-hosting guide](self-hosting-hermes-alternative.md) covers the stack, and [migrating from Hermes](migrate-from-hermes.md) covers the move.
