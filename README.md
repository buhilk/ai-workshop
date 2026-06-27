# ai-workshop

A workshop repo for combining two complementary agent skill ecosystems in one Cursor project:

- **[BMAD Method](https://github.com/bmad-code-org/bmad-method)** — structured agile workflows for analysis, planning, architecture, and delivery
- **[Matt Pocock skills](https://github.com/mattpocock/skills)** — small, composable engineering skills for day-to-day implementation

Skills are installed into `.agents/skills/` and tracked in `skills-lock.json`. Use this repo as a reference layout, or follow the steps below to set up the same combination in your own project.

## Prerequisites

- [Node.js](https://nodejs.org) 20+
- [Git](https://git-scm.com/)
- [Cursor](https://cursor.com/) (or another agent supported by the [skills CLI](https://skills.sh))
- For Matt Pocock engineering flows: [GitHub CLI (`gh`)](https://cli.github.com/) if you use GitHub Issues

---

## BMAD Method

**What it is:** [BMAD](https://docs.bmad-method.org) (Breakthrough Method for Agile AI-Driven Development) is a scale-adaptive framework that guides AI agents through structured agile workflows — from brainstorming and research through PRDs, architecture, and implementation.

**What it covers** (skills prefixed with `bmad-`):

| Area | Examples |
|------|----------|
| **Analysis & discovery** | `bmad-brainstorming`, `bmad-domain-research`, `bmad-market-research`, `bmad-technical-research`, `bmad-product-brief`, `bmad-prfaq` |
| **Planning** | `bmad-prd`, `bmad-spec`, `bmad-create-prd`, `bmad-validate-prd`, `bmad-ux` |
| **Architecture & solutioning** | `bmad-architecture`, `bmad-create-architecture`, `bmad-check-implementation-readiness` |
| **Implementation & delivery** | `bmad-dev-story`, `bmad-quick-dev`, `bmad-code-review`, `bmad-sprint-planning`, `bmad-sprint-status` |
| **Specialist agents** | `bmad-agent-pm`, `bmad-agent-architect`, `bmad-agent-dev`, `bmad-agent-analyst`, `bmad-agent-ux-designer`, `bmad-agent-tech-writer` |
| **Orchestration & help** | `bmad-help`, `bmad-auto`, `bmad-party-mode`, `bmad-advanced-elicitation` |

**Install BMAD skills** (via the [skills CLI](https://skills.sh)):

```bash
# Core BMAD Method skills (~46 skills)
npx skills@latest add bmad-code-org/bmad-method -a cursor --all

# Optional: BMAD Labs supplementary skills (testing, TypeScript, UI, integrations, etc.)
npx skills@latest add bmad-labs/skills -a cursor --all
```

**Full framework install (optional):** If you also want BMAD's `_bmad/` config, output folders, and workflow artifacts — not just the skills — run the official installer and select **Cursor** when prompted:

```bash
npx bmad-method install
```

See the [BMAD install guide](https://docs.bmad-method.org/how-to/install-bmad/) for non-interactive and CI options. After install, invoke `bmad-help` to see what to do next.

**Learn more:** [github.com/bmad-code-org/bmad-method](https://github.com/bmad-code-org/bmad-method) · [docs.bmad-method.org](https://docs.bmad-method.org)

---

## Matt Pocock Skills

**What they are:** Agent skills from [Matt Pocock](https://github.com/mattpocock) (Total TypeScript) — small, composable workflows built for real engineering: alignment before coding, test-driven development, triage, and codebase health.

**What they cover:**

| Area | Examples |
|------|----------|
| **Engineering flow** | `ask-matt` (router), `grill-with-docs`, `to-prd`, `to-issues`, `implement`, `prototype`, `triage` |
| **Code quality** | `tdd`, `diagnosing-bugs`, `improve-codebase-architecture`, `codebase-design`, `domain-modeling` |
| **Productivity** | `grill-me`, `handoff`, `teach`, `writing-great-skills` |
| **Setup** | `setup-matt-pocock-skills` (required once per repo) |

**Install Matt Pocock skills:**

```bash
npx skills@latest add mattpocock/skills -a cursor --all
```

**Learn more:** [github.com/mattpocock/skills](https://github.com/mattpocock/skills) · [skills.sh/mattpocock/skills](https://skills.sh/mattpocock/skills)

---

## Installing Both Together

Use this sequence to get BMAD planning workflows and Matt Pocock engineering skills working side by side in Cursor.

### 1. Clone or create your project

```bash
git clone https://github.com/buhilk/ai-workshop.git
cd ai-workshop
```

Or start from an empty repo and run the install commands below in your project root.

### 2. Install skills from both sources

```bash
# BMAD Method core skills
npx skills@latest add bmad-code-org/bmad-method -a cursor --all

# BMAD Labs extras (optional but included in this workshop repo)
npx skills@latest add bmad-labs/skills -a cursor --all

# Matt Pocock engineering skills
npx skills@latest add mattpocock/skills -a cursor --all
```

Each command writes skills under `.agents/skills/` and updates `skills-lock.json`. Pick individual skills instead of `--all` if you want a smaller set:

```bash
npx skills@latest add mattpocock/skills -a cursor \
  --skill setup-matt-pocock-skills \
  --skill ask-matt \
  --skill grill-with-docs \
  --skill to-prd \
  --skill to-issues \
  --skill implement \
  --skill tdd
```

### 3. (Optional) Install the full BMAD framework

If you need BMAD artifacts (`_bmad-output/`), module config, and guided phase workflows — not just the skills:

```bash
npx bmad-method install
```

Select **Cursor** as your IDE and the **BMM** (BMad Method) module at minimum. This coexists with the skills installed in step 2.

### 4. Configure Matt Pocock skills (required once)

In Cursor, run:

```
/setup-matt-pocock-skills
```

This configures your issue tracker (GitHub, GitLab, or local markdown), triage label vocabulary, and domain doc layout (`CONTEXT.md`, ADRs). The other Matt Pocock engineering skills depend on this setup.

### 5. Verify and start working

- List installed skills: `npx skills@latest list`
- Restore from lock file (e.g. after clone): `npx skills@latest experimental_install`
- **BMAD:** invoke `bmad-help` for workflow guidance
- **Matt Pocock:** invoke `/ask-matt` to route to the right skill

### How they fit together

| Phase | BMAD | Matt Pocock |
|-------|------|-------------|
| Discovery & research | `bmad-brainstorming`, `bmad-market-research`, `bmad-technical-research` | `grill-me`, `grill-with-docs` |
| Planning | `bmad-prd`, `bmad-spec`, `bmad-ux` | `to-prd`, `to-issues` |
| Architecture | `bmad-architecture`, `bmad-create-architecture` | `improve-codebase-architecture`, `codebase-design` |
| Implementation | `bmad-dev-story`, `bmad-quick-dev`, `bmad-code-review` | `implement`, `tdd`, `diagnosing-bugs` |
| Issue intake | — | `triage` |

BMAD excels at structured, phase-gated product development. Matt Pocock skills excel at tight engineering loops once you know what to build. Use BMAD for upfront planning and Matt Pocock skills for shipping and maintaining code.

---

## Official Repositories

| Project | GitHub | Docs |
|---------|--------|------|
| BMAD Method | [bmad-code-org/bmad-method](https://github.com/bmad-code-org/bmad-method) | [docs.bmad-method.org](https://docs.bmad-method.org) |
| BMAD Labs skills | [bmad-labs/skills](https://github.com/bmad-labs/skills) | — |
| Matt Pocock skills | [mattpocock/skills](https://github.com/mattpocock/skills) | [skills.sh/mattpocock/skills](https://skills.sh/mattpocock/skills) |
| Skills CLI | [vercel-labs/skills](https://github.com/vercel-labs/skills) | [skills.sh](https://skills.sh) |

---

## Updating Skills

```bash
# Update all project skills to latest versions
npx skills@latest update -y

# Re-sync BMAD framework after module changes
npx bmad-method install
```

Commit `skills-lock.json` after installs or updates so teammates get reproducible skill versions.
