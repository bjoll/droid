# Jarvis — Component Charter

The inventory of Jarvis's top-level pieces, each with purpose, capabilities, and boundary (what it explicitly does not do). Resolved in [ticket #2](https://github.com/bjoll/droid/issues/2); terminology is defined in [CONTEXT.md](../../CONTEXT.md).

**Vocabulary in one breath:** a **block** is a piece you could unplug and replace, at any size; an **assembly** is a group of blocks composed into one large unit; every piece is either **agentic** (LLM inside — thinks, judges, improvises) or **mechanical** (deterministic — runs its program like an alarm clock).

## Agentic pieces

### Jarvis (the front door)

Jarvis is a *role*, filled by an ordinary agent with front-door skills, memory access, and paper-trail access — not special machinery. Purpose: Bjoern's single point of contact — receives intent through any face (chat, CLI, voice, later the canvas), routes it to the right piece, chains stages when a workflow spans pieces (e.g. planning → factory), and answers questions about anything running in the system. Boundary: Jarvis never performs work itself — not even a quick search (that goes to an agent); he is not the system's orchestrator (each pipeline assembly drives its own work), and he is bypassable — Bjoern can dive into any piece directly at any time.

### Pods

The universal small work unit: a sandboxed group of one or a few agents, spun up for a task, working chat-style, shut down when done. Purpose: everything that isn't factory-shaped — one-off errands (email-complaint mining, bookmarking), recurring jobs (the daily newspaper, weekly politician tracker), research one-offs, and system jobs like the dreaming pod. Capabilities: a pod bound to a schedule entry receives fired work directly; a recurring pod self-evolves — noticing repetition, growing *local* skills and scripts (e.g. writing its own scraper to stop burning tokens), and improving from Bjoern's feedback. Boundary: pods cannot talk to other pods unless Bjoern explicitly approves the connection (the air gap); their self-grown skills stay local until explicitly promoted into the Skill Library; a pod that outgrows itself doesn't expand — it graduates (to an app via the factory, or to a pipeline job).

### Software Factory

An assembly: implementer, reviewer, and visual-verifier agents driven deterministically by hooks and the ticketing block (the programmatic issue-tracker piece). Purpose: turn an existing spec — PRD and issue backlog — into deployed, verified software, vertical slice by vertical slice (TDD, lint review, visual review), ending with a run report (cost, duration, obstacles, routes taken). Boundary: it begins where a spec exists — discovery, brainstorming, competitive research, and PRD writing are upstream work Jarvis chains in front of it; it has one job — build software — and its internal orchestrator answers to the factory, not to other pieces.

### Research Lab

A second instance of the Software Factory's pipeline pattern, pointed at research instead of code: a big research goal is split into tickets, worked by specialized agents, and composed into a report by the lab's orchestrator. Boundary: built only when a research job outgrows a pod — small and medium research stays pod-work; it shares the pipeline pattern's machinery rather than duplicating it.

### Scout

Purpose: the opportunity-spotter — reads paper trails and system records, notices graduation candidates ("this one-off keeps recurring — make it a pod," "this pod earned app-hood") and automation opportunities, and pitches proposals to Bjoern. Boundary: propose-only, never enacts; distinct from Watchers (external event monitors); it observes stored data, it does not watch Bjoern's screen.

## Mechanical pieces

### Scheduler

Holds schedule entries — recurring triggers created at setup time (by Jarvis or an agent below him), each bound to its target pod. When an entry fires, the work drops directly onto that pod, not through Jarvis. Boundary: decides nothing and owns no work; it is an alarm clock.

### Watchers

Monitors on external event sources — feeds, inboxes, markets — that fire triggers into the system when something happens. Boundary: a watcher triggers, it doesn't work; the reserved word "watcher" never means the Scout.

### Storage

The swappable home of the system's *operational* data: memories, paper trails, and system records (what exists, what runs, what it costs). Boundary: it holds machine-facing bookkeeping, not human-facing knowledge (that's the Second Brain); how it stores is its own contained business — swapping the storage implementation must never ripple across pieces.

### Second Brain

The knowledge base: human-facing plain files — notes, projects, ideas, meeting notes, bookmarks, and the deliverables of knowledge work (a research pod's summary, the bookmark itself). Bjoern browses and edits it directly in his own tool; agents read and write it through its interface like any other block. Law: the files are the source of truth — any database or index over them is derived and rebuildable, never the master. Boundary: knowledge only; operational data belongs to Storage; it must never become something only Jarvis can read.

### Skill Library

The shelf of approved skills. Every agent pulls its skills from it at spin-up (agents are mostly non-persistent, so this is how capability reaches fresh sandboxes). Boundary: pod-grown skills enter only by explicit, Bjoern-approved promotion — never silently; the library stores capabilities, it doesn't run them.

### Integrations

One block per connection: email, ClickUp, calendar, social accounts, Playwright MCP, LLM providers (each with its configuration). Purpose: give pods and pipelines plug-in access to the outside world, each behind its own swappable interface. Boundary: there is no monolithic "integrations service" — each is its own piece; which pod may use which integration, and how far unattended, is the autonomy-boundaries question (its own ticket).

### Dashboard

A view, not a doer: renders system data out of Storage — running jobs, sub-agent activity "like I'm in the terminal," costs, failures, takeover entry points — and is where Bjoern approves pod-to-pod connections. Boundary: owns no work and holds no state of its own; anything it shows could equally be asked of Jarvis in chat; whether it's web or CLI is deliberately open (dashboard prototype ticket).

## Law, not pieces

- **Communication contract** — the stud pattern: the standard interface shape every piece exposes so pieces fit each other. An agreement, not a piece (its own ticket).
- **Air gap** — default-deny between pods: no pod-to-pod communication unless Bjoern explicitly approves that connection.
- **Graduation ladder** — nothing starts as an app: quick query → one-off pod → recurring pod with local skills/scripts → prototype → app via the factory. Fluid by design; the Scout proposes steps up the ladder, Bjoern approves.
- **Files are truth** — the Second Brain's plain files are the source of truth; indexes are derived and disposable.
- **Explicit promotion** — nothing local becomes global automatically: not skills, not graduations.

## Dissolved from the seed list

- **Personal Assistant** — not a block: it's Jarvis's job description plus pods doing assistant-flavored work through integrations.
- **Learning System** — not a piece: memory (data) + the dreaming pod (scheduled consolidation: short-term memories elevated to long-term, the important promoted toward skills) + Skill Library + Scout, playing together.
- **Research Agent** — just an agent configuration, not a block.
- **Proactive/recurring task runner** — dissolved into Scheduler + Watchers + pods; no runner block exists.
- **Dashboard-as-block** — kept in the inventory but demoted to a view.
- **Canvas** — a communication *face*, not a piece of the core: a visual whiteboard way of handing work to the system. The core must be complete without it; its design is its own later effort.
