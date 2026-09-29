# Work OS

A plain-Markdown operating system for working with an AI agent. Point your agent at this folder and it knows who you are, how you write, which tools you use, what you are working on, and where to store what it learns.

No database, no app, no lock-in. Everything is a text file that you and the agent both read and edit.

## How it works

1. **`AGENTS.md` is the rulebook.** The agent reads it first, before every task. It contains the global rules, your standing preferences, a quality bar, and a routing map.
2. **The routing map decides what else to read.** The agent opens only the context files that matter for the current task instead of loading everything.
3. **Durable knowledge lives in `context/`.** When you tell the agent something worth keeping, it stores it in the right file, dates it, and marks anything uncertain.
4. **Repeatable workflows live in `agents/`.** Each workflow is a written procedure with its own memory files, so it improves from your feedback over time.

## Folder structure

```
Work OS/
├── AGENTS.md                  Rulebook and routing map. Read first, every time.
├── context/
│   ├── work-profile.md        Your role, expertise, clients, channels
│   ├── voice.md               Tone, language, and writing conventions
│   ├── tool-conventions.md    Rules for apps, files, spreadsheets, automations
│   ├── tech-stack.md          Devices, software, services, integrations
│   ├── projects.md            Active projects and a decisions log
│   └── people/                One file per person who matters to your work
├── agents/
│   ├── Personal Asistant/     Daily brief from calendar, email, and meetings
│   ├── Newsflash/             Weekly AI news and product-features digest
│   └── Context update/        Weekly proposal of context changes for approval
└── tasks/                     Output of tasks that have no other home
```

## Quick start

1. **Copy or fork this repository** into a folder your AI agent can read and write. A cloud-synced folder works well.
2. **Connect the folder to your agent.** Use any agent that can read local files and follow written instructions, for example Claude, ChatGPT, or a coding agent.
3. **Fill in the context files**, starting with `context/work-profile.md`. Ten minutes here saves a lot of correcting later. You can also just tell the agent about yourself and let it write the files.
4. **Adjust the Preferences section of `AGENTS.md`** with your language, formatting rules, and operating system.
5. **Work normally.** Ask for tasks, give feedback in plain language, and let the agent file what it learns.

## The agents

### Personal Asistant

Produces a daily brief from your calendar, email, and meeting notes: today's meetings with preparation notes, what needs work, what you are waiting on, and what is coming up. It keeps open tasks in `OPEN.md`, completed ones in `FINISHED.md`, and your feedback rules in `LEARNED.md`. Start with its [README](agents/Personal%20Asistant/README.md). Run it by asking for your daily brief.

### Newsflash

Produces a short, verified digest of AI news, new features in the assistants you use, and signals of what is coming. Every item needs a live source and a confirmed date. Scope, topics, and sources are configured in the SOP itself. See [`Newsflash SOP.md`](agents/Newsflash/Newsflash%20SOP.md).

### Context update

Scans email, calendar, and meeting transcripts for information that should change your context files, then saves a concrete proposal to an Update Log. Nothing is written to your context until you approve it. See [`CONTEXT-UPDATE.md`](agents/Context%20update/CONTEXT-UPDATE.md).

## How it improves

- **Your feedback** is appended as dated rules to each workflow's `LEARNED.md`. These rules take precedence over the default procedure.
- **Facts the agent discovers** go into `NOTES.md`, `context/`, and `context/people/`, so each run starts better informed than the last.
- **Self-assessment** is recorded in `SELF.md` and `SELF-IMPROVE.md`, so the agent can notice its own patterns.

Rules are only ever appended and always dated. When a new rule contradicts an old one, both stay and you decide.

## Customizing

- Add a context file by creating it in `context/` and adding a row to the routing map in `AGENTS.md`.
- Add a workflow by creating a folder in `agents/` with a procedure file and, if it should learn, a `LEARNED.md`.
- Edit the quality bar in `AGENTS.md` to match the standard you expect.
- Delete any agent you do not need. Nothing else depends on it.

## Privacy

Everything stays in your own files. Do not store passwords, access tokens, or other credentials in this folder, and think twice before committing personal or client information to a public repository. Keep a repository with real data private.

## Author

Created by [Jiri Benedikt](https://jiribenedikt.com).
