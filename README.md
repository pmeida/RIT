# RIT Triage with Claude Code

This repo contains Claude Code skills for automating the PIXAA RIT (Rotational Interrupt Team)
bug triage workflow. Three skills cover the full rotation lifecycle — from triaging new bugs
during the week, to end-of-week cleanup, to ongoing health checks.

---

## Skills

### `/rit-triage` — Triage incoming bugs

Run throughout the week to triage bugs from any PIXAA dashboard panel.

**What it does:**
- Fetches bugs from a dashboard panel via the Jira MCP server
- Classifies each bug and proposes triage actions:
  - Priority assessment (CVE, regression, customer impact)
  - Release Blocker evaluation (using the A/C/R/P rule framework)
  - Engineer assignment (even load distribution, expertise as tiebreaker)
  - `triaged` label application
  - Ownership check comment for ASSIGNED bugs with no linked PRs
  - PR-closed reset detection (Prow Bot) and notification
- Records all actions in a weekly tracker file (`triaged_bugs_YYYY-MM-DD.md`)

**Key principle:** automate the obvious, pause on judgment. Labels are applied automatically.
Priority, assignee, component checks, and Release Blocker always get a proposal and wait for
confirmation.

```
/rit-triage With Customer Cases
/rit-triage Component Regressions
/rit-triage Untriaged
/rit-triage With Due Date
/rit-triage Release Blockers
/rit-triage With OCPPRIO link
/rit-triage In Progress
/rit-triage All Open
```

Panel names are matched fuzzily — partial names and missing leading words are accepted.

---

### `/rit-end` — End-of-week cleanup

Run once at the end of the rotation week, before the next team starts.

**What it does:**
- Reads the current week's tracker to find bugs assigned by `/rit-triage`
- Skips bugs whose assignee is not in the current RIT roster (external engineers keep their bugs)
- Skips bugs that have progressed (ASSIGNED, POST, etc.), have a linked PR, or were Prow Bot reset
- For remaining stale bugs (still in `New`, no PR, no Prow Bot reset): proposes unassignment
  grouped by engineer, waits for confirmation, then removes assignee and posts a comment
- Result: next rotation's `/rit-triage` picks up unassigned bugs via the `needs_only_assignee`
  fast-path (no re-triage of component/priority/release blocker needed)

```
/rit-end
```

---

### `/rit-sweep` — Health check

Run on-demand (e.g. mid-week or periodically) to catch bugs invisible to the other two skills.

**What it does:**
- Finds triaged, assigned bugs stuck in `New` — these have all fields set so `/rit-triage`
  can't see them, and they may not be in the current week's tracker
- Detects Prow Bot PR-closed resets and posts a notification to the developer
- Detects stale bugs (no activity for N days) and posts a nudge comment
- With `--unassign`: also proposes removing assignments for stale RIT-roster engineers
  after confirmation (never unassigns PR-closed reset bugs or external engineers)

```
/rit-sweep
/rit-sweep --stale-days 30
/rit-sweep --stale-days 30 --unassign
```

Default stale threshold is 14 days. Use `--stale-days 30` or higher before `--unassign`
to avoid cleaning up bugs that are simply slow-moving.

---

## Typical weekly workflow

```
Everyday    /rit-triage Untriaged          ← triage new bugs
            /rit-triage With Due Date
            /rit-triage Component Regressions
            ...

Mid-week    /rit-sweep                     ← health check, PR-closed nudges

Friday EOW  /rit-end                  ← clean up stale assignments
            /rit-sweep --stale-days 30 --unassign   ← optional deeper cleanup
```

---

## Setup

### 1. Jira MCP Server (required)

All three skills use the Jira MCP server. Configure a working connection in your Claude Code
settings with access to the OCPBUGS project.

### 2. Update `rit_manual.md` each rotation (required)

Before running any skill, update the `# Current RIT Rotation` section with:
- The week-start date and pod name in the heading
- RIT Lead in the Non-Engineering table
- All engineers in the Engineering table (name, email, Jira Account ID, expertise, notes)
- Mark PTO engineers in the Notes column

The heading format must be: `# Current RIT Rotation — Week of YYYY-MM-DD (Pod Name)`

`/rit-triage` will stop and warn if this section appears stale (> 7 days old).

### 3. Release blocker rules (already configured)

The `.claude/skills/rit-triage/release_blocker_rules.md` file contains the full A/C/R/P
evaluation framework. Update `CURRENT_RELEASE` at the top of that file when the GA target
changes:

```
CURRENT_RELEASE = 5.0
```

### 4. Tracker file (auto-created)

`/rit-triage` creates `triaged_bugs_YYYY-MM-DD.md` on first run for the week. It records:
- Assignment distribution per engineer
- All bugs triaged this week with actions taken
- Bugs closed during triage

---

## File structure

```
RIT/
├── README.md                          # This file
├── rit_manual.md                      # RIT process manual, JQL queries, team roster, templates
├── triaged_bugs_YYYY-MM-DD.md         # Weekly tracker (auto-created by /rit-triage)
└── .claude/
    └── skills/
        ├── rit-triage/
        │   ├── SKILL.md               # Triage skill definition
        │   └── release_blocker_rules.md  # A/C/R/P release blocker evaluation rules
        ├── rit-end/
        │   └── SKILL.md               # EOW cleanup skill definition
        └── rit-sweep/
            └── SKILL.md               # Health check skill definition
```
