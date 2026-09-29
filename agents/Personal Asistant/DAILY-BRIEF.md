---
name: daily-briefing
description: Personal assistant that reviews email, calendar and meeting notes to produce a daily agenda summary — what needs attention today, what's coming up, what to keep in mind. Trigger on "summarize my day", "what's on my agenda", "daily briefing", "brief me". Self-improving skill.
---

# 1. Daily briefing (self-improving)

Goal: on request, review calendar, email, meeting transcripts and produce a short, actionable summary of the day. Not a full dump of everything — only what is relevant to act on.

Even if a brief was already produced for that day, do not produce a delta. Always run the full brief.

## 1.1 Files and sources

Each resource has a name, a description and a path relative to this file. Refer to resources by their **name** (in backticks) later in this document, not by their path.

| Name                | Purpose                                                                                                                                                           | Path             |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| `DAILY-BRIEF`       | This file. Stable procedure. Never edited automatically.                                                                                                          | `DAILY-BRIEF.md` |
| `ROOT RULES`        | Project instructions and routing map for selecting the relevant context files.                                                                                  | `../../AGENTS.md` |
| `CONTEXT FILES`     | Relevant files selected from `ROOT RULES`, including work profile, projects, tech stack, tool conventions and voice when applicable.                              | `../../context/`  |
| `OPEN`              | All open loops — things the user still has to do. Grouped by project, numbered so they are easy to refer to in chat.                                              | `OPEN.md`        |
| `FINISHED`          | Completed tasks, logged with a date and proof.                                                                                                                    | `FINISHED.md`    |
| `LEARNED`           | Process and style rules learned from user feedback (what to include, how to order, tone, format).                                                                 | `LEARNED.md`     |
| `NOTES`             | Factual context useful for producing a better brief — gathered during runs or shared by the user.                                                                 | `NOTES.md`       |
| `SELF-IMPROVEMENTS` | Automated self-assessment of brief quality and ideas for improvement.                                                                                             | `SELF.md`        |
| `PEOPLE`            | One file per person with meaningful relevance to the user's work, as directed by `ROOT RULES`.                                                                    | `../../context/people/` |
| `DAILY LOG`         | Archive of every brief produced, one file per run.                                                                                                                | `Daily Log/`     |

## 1.2 Procedure

1. Read `LEARNED` — process and style rules from prior feedback. **These take precedence over the general guidance below.**
2. Read `ROOT RULES`, then the relevant `CONTEXT FILES` according to its routing map. 
3. Read `NOTES` — accumulated factual context.
4. Read `OPEN` — previously logged open loops.
5. Read `FINISHED` — so completed items are not resurfaced.
6. Read the last 7 days of files in `DAILY LOG`.
7. Check the calendar for the **next 7 days**, using whatever calendar tool is available. Include all-day events.
8. Check unread and recent email, using whatever email tool is available. Focus on items requiring action or a reply — not newsletters or notifications.
9. Check the meeting-transcript tool (if available) for meetings relevant to open tasks. Also scan meetings from the last 7 days and extract open action items.
10. For each person with meaningful relevance to the user's work found in the calendar, email or meeting notes, check whether they have a file in `PEOPLE`. If yes, read it for context.
11. Verify status rather than copying it. For each open item, check the actual latest message in the thread before reporting it as still open.
12. Produce a summary structured as:
    - **Today's meetings** — time, who with, what it is about, and a short *Preparation* note for each
    - **Needs work** — tasks and emails requiring action, ordered by urgency
    - **Waiting on others** — items where the ball is not in the user's court, worth watching
    - **Coming up** — deadlines or events in the next few days worth keeping in mind now
    - **Nothing urgent** — only if there genuinely is nothing else; say so briefly instead of leaving an empty section
13. Save the summary in `DAILY LOG` as `YYYY-MM-DD daily brief.md`. If one already exists for that day, create a new file and append a number.
14. For each person mentioned in the brief who has meaningful relevance to the user's work, update or create their file in `PEOPLE` according to `ROOT RULES`. Log important context — what was discussed, tasks, meetings, commitments — dated, newest on top.
15. Add any open task not already in `OPEN` to the project it belongs to. If there is no matching project, create one.
16. Output the summary to the chat.

## 1.3 Never do

- Never send emails or respond to invitations without the user's explicit, in-the-moment confirmation.
- Never quote sensitive or personal email content verbatim — paraphrase the substance.
- Never dump everything found. The summary should be short, not a complete log.
- Never write preferences or style rules into `OPEN` — those belong in `LEARNED`.
- Never write unconfirmed facts into `CONTEXT FILES`. Follow `ROOT RULES` when updating durable context.
- Never edit `DAILY-BRIEF.md` itself automatically. The brief workflow may update `LEARNED`, `OPEN`, `FINISHED`, `NOTES`, `SELF-IMPROVEMENTS`, `PEOPLE` and routed `CONTEXT FILES` according to `ROOT RULES`.

## 1.4 Self-improvement

Ask for feedback after sharing the brief. The user can use it to change the workflow, edit open tasks or add context.

### Improving the workflow

If the user says something was missing, irrelevant, mis-ordered, or that they want a different format or tone ("I don't care about this", "you should have included that", "order it like this instead", "this is too long"):

1. Add an entry to `LEARNED` in the right section, using this format:

   ```markdown
   ## YYYY-MM-DD – Short context

   - **Context:** What the summary covered or what the feedback was about.
   - **Issue:** What the user disliked or found missing.
   - **Preference:** What they want instead.
   ```

2. Preserve existing entries. Never delete or rewrite them — only append. If a new rule conflicts with an existing one, add it as a dated addendum and let the user decide.

### Updating open tasks

If the user says a task is finished, extended, changed, or gives additional detail, edit `OPEN` to reflect it. Anything the user confirms as finished goes to `FINISHED` with a date and short proof.

### Adding context notes

If the user mentions something useful — which person belongs to which project, additional information about a project, any other context not already known — store it in `NOTES`.

### Self-assessment

After producing the brief, assess it. Score it 0–10 on five criteria of your choice (for example: capture of new signals, verification of thread status, brevity, accuracy of stored data, meeting preparation). For every criterion scoring below 10, suggest a concrete improvement. Append to `SELF-IMPROVEMENTS`, starting with the date, then the scoring with reasoning, then the ideas.

If the same observation recurs across several runs without being acted on, stop repeating it silently. Raise it with the user directly as a decision to make.

## 1.5 Output format

Go straight into the structured summary. No preamble.
