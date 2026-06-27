---
name: ai-news
description: Fetches and summarizes current AI industry news, breaking developments, model releases, research, policy, and product launches from verified sources. Use when the user asks for AI news, what's happening in AI, latest AI developments, breaking AI updates, an AI briefing, or wants to stay current on the AI world.
---

# AI News Briefing

Deliver timely, sourced summaries of what's happening in AI. Prioritize recency, accuracy, and signal over volume.

## Prerequisite

**Web search required.** If `WebSearch` or `WebFetch` is unavailable, stop and tell the user.

## Quick start

1. Note today's date and the user's scope (breaking, daily, weekly, or topic-specific).
2. Run **multiple targeted searches** — do not rely on a single query.
3. Cross-check important claims across at least two independent sources when possible.
4. Prefer primary sources (company blogs, papers, official announcements) over aggregators.
5. Return a structured briefing (template below).

## Scope detection

| User intent | Search focus |
|-------------|--------------|
| **Breaking / today** | Last 24–48 hours; lead with highest-impact items |
| **This week** | Last 7 days; group by theme |
| **Topic-specific** | Filter to their topic (e.g. "open-source LLMs", "EU AI Act", "AI coding tools") |
| **Deep dive on one story** | One headline → full context, timeline, reactions, implications |

If scope is unclear, default to **breaking + last 7 days** and say so in the briefing header.

## Search strategy

Run searches in parallel when possible. Adapt queries to the current date.

**Core queries (run 3–5):**
- `AI news [current month year]`
- `artificial intelligence breaking news today`
- `LLM model release announcement [current year]`
- `AI regulation policy news [current year]`

**Topic add-ons (when relevant):**
- Research: `AI research paper breakthrough [current year]`
- Products: `AI product launch [company or category]`
- Enterprise: `enterprise AI adoption news`
- Safety: `AI safety alignment news`

For deeper coverage, see [sources.md](sources.md) for preferred outlets and search hints.

## Source quality rules

**Prefer:**
- Official company/engineering blogs (OpenAI, Anthropic, Google DeepMind, Meta AI, etc.)
- Peer-reviewed or widely cited research (arXiv with notable uptake, major lab announcements)
- Established tech journalism with named authors (Reuters, Bloomberg, The Verge, Ars Technica, etc.)
- Government and standards bodies for policy

**Treat with caution:**
- Unverified social posts, anonymous leaks, SEO spam farms
- Clickbait headlines without underlying primary source
- Rumor posts labeled as fact

**Always include:** direct links to the best available primary or secondary source for each item.

## Briefing template

Use this structure unless the user asks for a different format:

```markdown
# AI News Briefing — [Date range]

**Scope:** [breaking | weekly | topic: X]
**Last updated:** [today's date]

## Top stories

### 1. [Headline]
- **What happened:** [1–2 sentences, factual]
- **Why it matters:** [impact on builders, users, or the industry]
- **Source:** [link]
- **Confidence:** [confirmed | reported | rumor — and why]

### 2. ...

## Also worth knowing
- [Shorter bullets for secondary stories]

## Themes this period
- [Optional: 2–4 bullet synthesis — models, policy, tools, research]

## What to watch next
- [Upcoming events, expected releases, ongoing stories]
```

## Output guidelines

- Lead with **what changed**, not background history the user likely knows.
- Separate **confirmed facts** from **reported/unverified** claims.
- For model releases: name, capabilities, availability (API/open/weights), and how it compares to prior gen if stated by the source.
- For policy: jurisdiction, status (proposed/enacted/litigated), effective dates.
- For research: problem solved, method at a high level, whether it's deployed or lab-only.
- Keep the main briefing scannable; put long context in collapsible detail only if the user wants depth.
- If nothing significant surfaced, say so honestly and suggest narrower or broader search terms.

## Follow-up modes

After the briefing, the user may ask to:
- **Go deeper** on one story → timeline, stakeholders, technical detail, community reaction
- **Compare** two developments → table or side-by-side
- **Track** a topic over time → note what to search next check-in
- **Translate to action** → what it means for their project, stack, or compliance posture

## Anti-patterns

- Do not present training-data cutoff knowledge as current news.
- Do not invent release dates, benchmark numbers, or quotes.
- Do not flood the user with 20 low-signal items — curate to ~5–8 top stories unless they ask for exhaustive coverage.
- Do not copy paywalled article text; summarize and link.
