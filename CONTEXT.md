# Jarvis

Glossary for Jarvis — Bjoern's personal all-purpose agent system (assistant, researcher, software factory). One user, no product concerns.

## Language

**Jarvis**:
The front-door role — Bjoern's single point of contact that routes intent into the system and reports back, never performing work itself; filled by an ordinary agent with front-door skills, memory, and paper-trail access.
_Avoid_: orchestrator (Jarvis routes and reports; orchestration of work happens inside blocks), assistant

**Block**:
A piece you could unplug and replace — any size, from a skill to the scheduler; it does one job and fits other pieces through its interface.
_Avoid_: module, element, component

**Agentic**:
Said of a piece with an LLM inside — it can think, judge, and improvise (Jarvis, pods, the Scout, the factory's agents).
_Avoid_: worker

**Mechanical**:
Said of a deterministic piece that just runs its program, like an alarm clock (scheduler, hooks, ticketing block, Storage, Skill Library, dashboard).
_Avoid_: programmatic, scripted, service

**Assembly**:
A group of blocks composed into one large unit with a single job — e.g. the Software Factory; not itself a block, because you take it apart rather than swap it whole.
_Avoid_: monolith

**Canvas**:
A visual communication face — a transparent whiteboard for brainstorming and mind-mapping where Bjoern arranges information and hands regions to Jarvis or pods as work; another way of talking to the system, never something its core depends on.
_Avoid_: canvas workspace block

**Communication contract**:
The standard interface shape every piece must expose so pieces fit each other — like the stud pattern on a Lego brick; an agreement, not a piece.

**Software Factory**:
The assembly that turns an existing spec (PRD / issue backlog) into deployed, verified software via a deterministic, issue-tracker-driven pipeline of blocks (implementer/reviewer agents, hooks, the ticketing block).
_Avoid_: dev pipeline, build system

**Dashboard**:
A view over running work and system state — a visualizer, not a block; anything it shows could equally be asked of Jarvis in chat.
_Avoid_: control center, admin panel

**Skill**:
A reusable, named capability an agent picks up on spin-up from the global skills directory.

**Agent**:
A sandboxed, usually non-persistent worker: a configuration of skills spun up for a task and shut down after.

**Pod**:
A sandboxed, usually short-lived unit of one or a few agents that takes a loose instruction, works chat-style, may grow local skills/scripts if its task recurs, and shuts down when done.
_Avoid_: think tank, research group, sandbox group

**Scout**:
The agent that reads the paper trail and system records for graduation and automation opportunities and pitches proposals to Bjoern; propose-only, never enacts.
_Avoid_: idea manager, watcher, spotter

**Watcher**:
A monitor on an external event source (feed, inbox, market) that fires a trigger into the system; reserved for event-triggers, never the Scout.

**Second Brain**:
The knowledge base block — human-facing plain files (notes, projects, ideas, meeting notes, bookmarks, research deliverables) that Bjoern browses directly; the files are the source of truth, any index over them is derived and rebuildable.
_Avoid_: knowledge store, vault, Obsidian (tool, not the concept)

**Skill Library**:
The library block where all approved skills live; agents pull skills from it at spin-up. A pod's self-grown skills stay local until explicitly promoted into the library.
_Avoid_: skills directory, global skills

**Storage**:
The storage block — the swappable piece where all stored data lives: memories, paper trails, and system records (what exists, what runs, what it costs).
_Avoid_: registry, memory storage, database (implementation word)

**Paper trail**:
A communication log between two entities — agent↔agent or agent↔human; every exchange leaves one.

**Memory**:
What an agent remembers and learns from — outcomes, fixes that worked or failed, important experiences; the raw material of dreaming.

**Dreaming**:
The overnight/idle consolidation process, as in humans: short-term memories from the day are sifted, and important ones are elevated into long-term memory with stronger weighting — at the far end, promoted toward skills.

**Air gap**:
The default-deny rule between pods: no pod talks to another unless Bjoern explicitly approves that connection.

**Schedule entry**:
A recurring trigger bound to a target pod at setup time; when it fires, work drops directly onto that pod, not through Jarvis.

## Relationships

- **Jarvis** routes intent to **Blocks** and reports their status back to Bjoern.
- The **Software Factory** begins where a spec exists; upstream discovery/planning is not its job.
- The **Dashboard** renders what **Jarvis** could report; it owns no work.
- An **Agent** is assembled from **Skills** at spin-up.

## Example dialogue

> **Dev:** "Can **Jarvis** just summarize these emails himself?"
> **Domain expert:** "No — **Jarvis** never works. He hands it to an **Agent** and relays the result. The **Software Factory** doesn't take that job either; it only starts once a spec exists."

## Flagged ambiguities

- "Orchestrator" was used both for the Jarvis front door and for the factory's internal work-driver — resolved: **Jarvis** is the front door; each pipeline block has its own internal orchestrator, unnamed at system level.
- "Research agent" was floated as a top-level block — leaning: it is just an **Agent** configuration, not a block (under discussion).
- "Personal Assistant" was floated as a master block — resolved: it is Jarvis's job description, not a block; errands run as short-lived worker units (name pending) drawing on shared integrations.
- "Research lab" vs "Software Factory" — resolved: one structured-pipeline pattern, instantiated per work type (software, research).
- "Overview agent" vs "watcher" — resolved: the registry is state (what runs, what it costs, the paper trail); the watcher is an agent that reads it and proposes graduations. Never auto-promotes.
