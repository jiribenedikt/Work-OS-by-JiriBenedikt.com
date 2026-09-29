# Personal assistant – daily brief template

A file-based setup for an AI personal assistant that produces a daily brief from your calendar, email and meeting notes — and gets better at it over time, because it writes down what you tell it.

Everything is plain Markdown. No database, no app. The assistant reads and writes these files.

## What is in here

```
Personal Asistant/
├── DAILY-BRIEF.md      The procedure. The only file you should edit by hand
│                       when you want to change how the brief works.
├── OPEN.md             Open tasks, grouped by project, numbered.
├── FINISHED.md         Completed tasks with proof.
├── LEARNED.md          Rules the assistant has learned from your feedback.
├── NOTES.md            Facts the assistant has picked up along the way.
├── SELF.md             The assistant's own quality assessment of each brief.
└── Daily Log/          One file per brief produced (created on the first run).
```

Who you are lives in the root `AGENTS.md` and the `context/` folder (work profile, projects, tech stack, tool conventions, voice). People you deal with get one file each in `context/people/`.

## How the files relate

`DAILY-BRIEF.md` is the instruction. It is stable — the assistant never edits it automatically.

Everything else is memory, and each kind of memory has one home:

| You tell the assistant… | It goes in |
|---|---|
| "I don't need that in the brief" / "order it this way" | `LEARNED.md` |
| "that's done" | `FINISHED.md`, removed from `OPEN.md` |
| "I still need to do X" | `OPEN.md` |
| "by the way, Anna handles procurement there" | `NOTES.md` |
| "my role is…" / "remember that…" | `context/` files, routed by `AGENTS.md` |

Keeping these separate is what stops the assistant from mixing your preferences with your to-do list.

## Setup

1. **Copy this folder** somewhere your assistant can read and write — a synced folder works well.
2. **Fill in `context/work-profile.md` and the other `context/` files.** Ten minutes here saves a lot of correcting later. Be specific about what counts as urgent and what you never want to see.
3. **Connect your tools.** The procedure expects, at minimum, a calendar and an email tool. A meeting-transcript tool is optional but makes the meeting preparation notes much better.
4. **Run it once.** Ask: "run my daily brief". Expect the first run to be wrong in small ways.
5. **Give feedback in plain language.** "This is too long." "You missed the thing I promised on Friday." "Put client work first." Each correction becomes a rule in `LEARNED.md`, so you only have to say it once.
6. **Optional: schedule it.** Once a few runs feel right, set it to run each weekday morning.

## How it improves

Three loops run at different speeds:

- **Your feedback** → `LEARNED.md`. Immediate, and it takes precedence over the default procedure.
- **Facts it discovers** → `NOTES.md` and `context/people/`. Each run starts better informed than the last.
- **Its own self-assessment** → `SELF.md`. After each brief it scores itself and notes what to do differently.

The rule that keeps this honest: never delete, only append, and always date. When a new rule contradicts an old one, both stay and you decide.

## Making it yours

- Change the section headings in the brief by editing step 12 of `DAILY-BRIEF.md`.
- Change the task groups in `OPEN.md` to match how you actually think about your work.
- If you work in a language other than English, translate the files — the structure matters, the wording does not.
- Delete `SELF.md` and the self-assessment step if you find it noisy.
