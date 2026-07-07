# RIT Triage with Claude Code

This repo contains the `/rit-triage` Claude Code skill for automating PIXAA bug triage during RIT (Rotational Interrupt Team) weeks.

## What it does

The `/rit-triage` skill automates the triage monitor workflow:

1. Fetches bugs from a PIXAA dashboard panel via Jira API
2. Loops through each bug and proposes triage actions:
   - Status transitions (e.g. ASSIGNED with no PRs -> New)
   - Priority assessment (CVE, regression, customer impact)
   - Engineer assignment (load-balanced, expertise-matched)
   - `triaged` label application
3. Records everything in a tracker file (`triaged_bugs_YYYY-MM-DD.md`)

**Key principle: automate the obvious, pause on judgment.** Labels are applied automatically. Priority, assignee, and status changes always get a proposal and wait for confirmation.

## Usage

```
/rit-triage <panel-name>
```

Panel names match the PIXAA Bugs Dashboard:

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

## Dependencies

### 1. Jira MCP Server (required)

The skill uses the Jira MCP server for all bug operations. You need a working Jira MCP connection configured in your Claude Code settings with access to the OCPBUGS project.

Tools used: `jira_search`, `jira_get_issue`, `jira_update_issue`, `jira_transition_issue`, `jira_add_comment`, `jira_get_transitions`, `jira_get_issues_development_info`

### 2. RIT Manual (`rit_manual.md`) (required)

The skill reads `rit_manual.md` from the working directory to get:

- **JQL queries** for each dashboard panel
- **Team roster** with engineer names, Jira account IDs, and areas of expertise
- **Comment templates** for status transitions and priority changes
- **Priority criteria** for bug assessment

You must update this file each rotation with:
- Current RIT rotation engineers (mark PTO engineers)
- Any changes to JQL filters or dashboard panels

### 3. Team Roster in CLAUDE.md (recommended)

For assignee mapping, the skill needs Jira account IDs for each engineer. These can live in either `rit_manual.md` or your `CLAUDE.md`. Example format:

```markdown
| Short name | Full name | Jira Account ID |
|------------|-----------|-----------------|
| alice | Alice Smith | 712020:abc123-... |
| bob | Bob Jones | 557058:def456-... |
```

### 4. Tracker File (auto-created)

The skill creates `triaged_bugs_YYYY-MM-DD.md` on first run. It tracks:
- Bugs triaged this week (key, summary, priority, assignee, status)
- Assignment distribution per engineer
- Bugs closed this week

## Setup

1. Clone this repo into your working directory
2. Configure the Jira MCP server in Claude Code
3. Update `rit_manual.md` with your rotation's team roster and JQL filters
4. Run `/rit-triage <panel-name>` to start triaging

## End-of-Week Cleanup

At end of week, unassign all triaged bugs still in New status:

```
Action: unassign all bugs in triaged_bugs_YYYY-MM-DD.md that are
assigned to read group engineers AND still in New status
```

This ensures the next rotation picks them up fresh and they're visible under "Show triaged (ignore assignee)" in the PIXAA dashboard.

## File Structure

```
RIT/
├── README.md                        # This file
├── rit_manual.md                    # RIT process manual, JQL queries, team roster
├── triaged_bugs_YYYY-MM-DD.md       # Weekly tracker (auto-created)
└── .claude/
    └── skills/
        └── rit-triage/
            └── SKILL.md             # The triage skill definition
```
