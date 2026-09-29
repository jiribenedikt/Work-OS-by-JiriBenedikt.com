---
name: newsflash
description: Personal AI and product-features newsfeed for scheduled tasks. Produces a concise, current, categorized "Newsflash", shows it in full in chat, saves it to the News Log, and self-improves from feedback and relevance ratings. Trigger on "run my newsflash", "newsflash", "AI news digest", or on schedule.
---

# Newsflash SOP

Goal: on request or on schedule, produce a short, current, categorized digest of AI and product news relevant to the user. Every item must be genuinely recent and verified with a live source. The output is shown in full in chat and saved to the News Log. The newsflash improves over time from the user's feedback (`LEARNED`) and per-item relevance ratings in the logs (`SELF-IMPROVE`).

This document is both the instructions and the configuration. Edit the CONFIG blocks to change what each section covers, which topics to include or exclude, and which sources to use. New sections can be added by copying the section template at the bottom.

## 1. Files & folders

All paths are relative to the project root.

1. `Newsflash SOP` – this file. The stable procedure and config. Path: `agents/Newsflash/Newsflash SOP.md`
2. `News Log` – every generated newsflash is saved here as one file per run. Path: `agents/Newsflash/News Log/` (create it on the first run if it does not exist)
3. `LEARNED` – log of feedback the user gives after a newsflash (what to include or exclude, tone, format, ordering, sources). **Always read and applied before generating a newsflash.** Path: `agents/Newsflash/LEARNED.md`
4. `SELF-IMPROVE` – conclusions drawn from the user's per-item relevance ratings in past logs, plus improvement ideas for the process. Path: `agents/Newsflash/SELF-IMPROVE.md`

## 2. Global rules

- **Language:** use the language set in the Preferences section of `AGENTS.md`. If none is set, use English.
- **Apply `LEARNED` first.** Read `LEARNED` at the start of every run and honor it. Its rules take precedence over the general guidance in this SOP where they conflict.
- **Personalize.** Read `context/work-profile.md` and `context/tech-stack.md` so relevance is judged against the user's field, audience, and the AI products they actually use.
- **Recency is mandatory.** Use web search and web fetch for every section. Do not rely on memory or training knowledge for what is "new". If you cannot confirm an item is recent from a live source, drop it.
- **Recency window:** by default include only items published or announced in the **last 7 days** (measured from today's date). If a scheduled run has a known cadence, use that cadence as the window instead. State the window at the top of the output.
- **Verify dates.** For each item, confirm the publication or announcement date. Never present an old item as new. If an item is a re-announcement or a wider rollout of something older, say so explicitly.
- **Deduplicate.** Merge multiple sources reporting the same thing into one item with the best source link.
- **Cite sources.** Every item ends with a source link. Prefer primary sources (official blog, release notes, changelog) over secondary coverage.
- **Signal over volume.** Keep it tight. Aim for the most relevant 3-6 items per section, not an exhaustive list. If a section has nothing genuinely new in the window, say "Nothing new this period" for that section rather than padding.
- **No hype.** Neutral, factual tone. One or two sentences per item explaining what it is and why it matters to the user.
- **Chat = file.** The newsflash shown in chat is the **full** newsflash, identical to the file saved in the News Log, **including all source links**. Never post a shortened or teaser version in chat and save the full one only to disk.

## 3. Sections

Process the sections in the order listed. Each section has a CONFIG block controlling its scope. Respect include/exclude topics and the source list.

### 3.1 AI News

All new, interesting developments in AI: model releases, major research, notable product launches, funding and industry moves, regulation, and capability breakthroughs.

```config
INCLUDE:
  - New frontier or notable model releases (any major lab)
  - Significant research results and capability breakthroughs
  - Major industry and business moves (funding, acquisitions, partnerships, leadership)
  - AI regulation, policy, and safety developments
  - Practical tools and agents relevant to the user's work (see context/work-profile.md)
EXCLUDE:
  - Pure crypto or token projects
  - Low-quality "listicle" content and rumor with no primary source
  - Minor incremental version bumps with no user-visible impact
SOURCES (starting points, not exhaustive – always web-search fresh):
  - Official lab blogs: Anthropic, OpenAI, Google DeepMind, Meta AI, Mistral
  - The Batch (deeplearning.ai), Import AI, TLDR AI
  - TechCrunch AI, The Verge AI, Ars Technica
  - Hacker News front page (news.ycombinator.com) filtered for AI
```

### 3.2 New features

New, concrete features shipped in the AI assistants the user uses, as listed in `context/tech-stack.md`. If that file lists none, cover the major general-purpose assistants (Claude, ChatGPT, Gemini, Microsoft 365 Copilot). This section is about shipped, user-usable features and changelog items, not general company news.

Where a product has separate consumer and business editions or license tiers, cover the edition the user works with, and label each item with the edition or tier it applies to. If the tier is unclear from the source, state that it is unconfirmed rather than guessing.

```config
PRODUCTS & SCOPE:
  - Each assistant listed in context/tech-stack.md: new features across web, desktop, and mobile apps, and API-level features that reach end users
INCLUDE:
  - Shipped, user-facing features and changelog entries
  - Meaningful rollouts to new regions or plans that change who can use a feature
EXCLUDE:
  - Editions of a product the user does not use
  - Pure pricing or marketing announcements with no feature change
  - Closed betas not available to normal users (mention only if highly relevant, and flag as "not yet generally available")
SOURCES (starting points – always web-search fresh):
  - The official release notes, changelog, or product blog of each product
  - Vendor help-center release notes and admin or roadmap pages
```

### 3.3 Beyond the horizon

Forward-looking signals: pre-release research, announced-but-not-shipped capabilities, roadmap hints, and emerging trends that are not yet products but are worth watching. This is the "what's coming" section, clearly separate from what shipped.

```config
INCLUDE:
  - Announced-but-unreleased models, features, and research previews
  - Roadmaps, leaks with credible sourcing, and official "coming soon" statements
  - Emerging techniques and trends likely to matter in 3-12 months
  - Longer-horizon shifts relevant to the user's field (see context/work-profile.md)
EXCLUDE:
  - Baseless speculation and rumor with no credible source
  - Anything already generally available (that belongs in AI News or New features)
SOURCES (starting points – always web-search fresh):
  - Official lab research pages and "coming soon" posts
  - arXiv (cs.AI, cs.CL) highlights, conference announcements
  - Credible analysts and newsletters
```

## 4. Procedure

1. Read this SOP, including all CONFIG blocks (they may have been edited since the last run).
2. Read `LEARNED` and apply every rule in it to this run.
3. Read `AGENTS.md` and the relevant files in `context/`.
4. Determine today's date and the recency window (default: last 7 days, or the scheduled cadence).
5. For each section in order (AI News, New features, Beyond the horizon, then any added sections):
   a. Web-search the section's sources and topic queries for items within the window.
   b. For each candidate, verify the publication or announcement date from a live source. Discard anything outside the window or unverifiable.
   c. Apply the section's INCLUDE/EXCLUDE rules.
   d. Deduplicate and keep the top 3-6 items by relevance to the user.
6. Assemble the newsflash using the output format in section 5. Number every item (1, 2, 3 within each section) so the user can reference items when rating them.
7. **Save** it to `agents/Newsflash/News Log/` as `YYYY-MM-DD Newsflash.md`. If a file already exists for that date, append ` (2)`, ` (3)`, etc.
8. **Show the full newsflash in chat** – the exact same content that was saved, including all source links. Do not shorten it.
9. Run the self-improvement pass in section 6.
10. If the user gives feedback in chat after the newsflash, log it to `LEARNED` per section 6.

## 5. Output format

Use this structure. Markdown. Number items within each section.

```markdown
# Newsflash – {DATE}
_Window: {recency window, e.g. last 7 days} · Generated {DATE}_

## AI News
1. **{Headline}** – {1-2 sentence what & why it matters}. ({Source name}, {date}) [link]
2. ...
_(or: "Nothing new this period.")_

## New features
**{Product}**
1. **{Feature}** – {what it does}. ({Source}, {date}) [link]
2. ...

**{Next product}**
1. ...

## Beyond the horizon
1. **{Signal}** – {what's coming and why to watch}. ({Source}, {date}) [link]
2. ...
```

## 6. Self-improvement & feedback

### 6.1 Feedback log (`LEARNED`)
When the user gives feedback in chat after a newsflash (something was irrelevant, missing, mis-ordered, wrong tone, length, or format, a source they trust or dislike, a topic to add or drop), append an entry to `LEARNED` in this format, newest at the end:

```markdown
## YYYY-MM-DD – Short context
- **Context:** which newsflash / section / item the feedback was about.
- **Issue:** what the user disliked or found missing.
- **Preference:** what the user wants instead (as a rule to apply next time).
```

`LEARNED` is read and applied at the start of every run (section 4, step 2). Treat it as standing instructions.

### 6.2 Relevance ratings pass (`SELF-IMPROVE`)
At the end of every run, review the **previous newsflash file(s) in the News Log** and look for relevance ratings or notes the user added to individual items (for example a score, a "not relevant", a strike-through, or a comment next to an item). Then:

1. Read the previous log file(s) since the last self-improvement pass (at minimum the most recent one; if several are unreviewed, cover them).
2. Collect the per-item ratings and feedback and look for patterns: which topics, sources, sections, or products are rated high versus low.
3. Draw concrete conclusions (for example "downweight X source", "regulation items are consistently rated low", "more feature detail wanted for product Y").
4. Append these conclusions to `SELF-IMPROVE`, dated, in this format:

```markdown
## YYYY-MM-DD – Self-improvement pass
- **Logs reviewed:** {which dates}.
- **Ratings observed:** {summary of what was rated high or low}.
- **Conclusions:** {patterns identified}.
- **Actions to apply:** {concrete changes to make next time – topics to add or drop, sources to up- or downweight, ordering}.
```

5. Where a conclusion is a stable, repeatable rule, also promote it into `LEARNED` (or propose editing the relevant CONFIG block in this SOP) so future runs apply it automatically.

Never rewrite `Newsflash SOP` automatically. Only `LEARNED` and `SELF-IMPROVE` are updated automatically; CONFIG blocks in this SOP are edited only on the user's confirmation.

## 7. Adding a new section

To add a section, copy this template below the existing sections in part 3, give it a number and a name, write a one-line purpose, and fill in the CONFIG block. It is then automatically picked up by the procedure in section 4.

````
### 3.x {Section name}

{One-line description of what this section covers.}

```config
INCLUDE:
  - ...
EXCLUDE:
  - ...
SOURCES:
  - ...
```
````

## 8. Never do

- Never present old news as new, and never include an item whose date you could not verify.
- Never leave an item without a source link.
- Never skip saving to the News Log, and never post a shortened version in chat – chat must match the saved file, links included.
- Never ignore `LEARNED` – it is applied on every run.
- Never pad sections – "Nothing new this period" is a valid and preferred result over filler.
