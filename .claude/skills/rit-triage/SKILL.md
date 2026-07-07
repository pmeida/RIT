---
name: rit-triage
description: Triage bugs from a PIXAA dashboard panel — assess, prioritize, assign to RIT team, and record
argument-hint: "<panel-name> — e.g. 'With Customer Cases', 'Component Regressions', 'Untriaged'"
allowed-tools: Read, Edit, Write, mcp__jira__jira_search, mcp__jira__jira_get_issue, mcp__jira__jira_update_issue, mcp__jira__jira_transition_issue, mcp__jira__jira_add_comment, mcp__jira__jira_get_transitions, mcp__jira__jira_get_issues_development_info
---

# RIT Triage

Triage bugs from a PIXAA Bugs Dashboard panel. Fetches all bugs, loops through each one, applies triage actions (status transitions, priority, assignee, labels, comments), and records everything in the tracker file.

## Usage

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

The panel name must match one from the "PIXAA Bugs Dashboard JQL Queries" table in `rit_manual.md`.

## Instructions

### Step 1: Load configuration

Read `/Users/jhadvig/Workspace/OpenShift/RIT/rit_manual.md` and extract:

1. **JQL query** — Find the "PIXAA Bugs Dashboard JQL Queries" section. Locate the table row matching the `<panel-name>` argument. Construct the full JQL:
   - Base filter: `filter in (operator-framework-all-bugs, "PIXAA HIVE bugs", "PIXAA CCO bugs", "PIXAA OCPCLOUD bugs", "PIXAA Console bugs", "PIXAA MCP Server Bugs", "PIXAA Serverless Bugs", "All OTA Bugs")`
   - Plus the panel's extra conditions from the table
   - Plus common triage condition: `(labels is EMPTY or labels not in (triaged) or assignee is EMPTY or priority is EMPTY) and (labels not in (ocp-sustaining) or labels is EMPTY)`
   - Plus `statusCategory != done`
   - Plus the panel's sort order

   If the panel name doesn't match any row, tell the user and list valid panel names.

2. **RIT team roster** — Find the "Current RIT Rotation" section. Parse the Engineering table to get: name, email, Jira Account ID, area of expertise, notes (e.g. PTO). Skip engineers marked as PTO.

3. **Comment templates** — Find the "Comment templates for status transitions" section. Load the templates for ASSIGNED->New (reassign), ASSIGNED->New (keep), and priority setting.

4. **Tracker file** — Look for an existing `triaged_bugs_YYYY-MM-DD.md` file in `/Users/jhadvig/Workspace/OpenShift/RIT/` where the date matches the current RIT rotation week start date from the "Current RIT Rotation" heading. If it exists, read the current assignment distribution to know each engineer's current bug count. If it doesn't exist, create it with the standard header and empty tables.

### Step 2: Fetch all bugs

1. Run `mcp__jira__jira_search` with the constructed JQL. Request fields: `summary,status,assignee,priority,labels,components,created,updated`. Set limit to 50.

2. If there are more results (next_page_token), paginate to get all bugs.

3. Batch-fetch development info for all bug keys using `mcp__jira__jira_get_issues_development_info` with `data_type=pullrequest` to check for linked PRs. Do this in batches of 16 keys.

4. Build an in-memory list of all bugs with their full context: summary, status, priority, assignee, labels, components, has_linked_PRs (boolean).

### Step 3: Present summary to user

Show:
- Total bug count
- Grouped by status: how many in New, ASSIGNED, POST, ON_QA, other
- How many need: priority (Undefined), assignee (Unassigned), `triaged` label, status transition (ASSIGNED with no PRs)
- Current RIT team load from tracker file

Ask user: "Proceed with triage? (yes/no)"

If the user says no, stop.

### Step 4: Loop through each bug

Process bugs in priority order (Critical first, then Major, Normal, Minor, Undefined). For each bug:

#### Action 1: Assess status
- If status is POST, ON_QA, or Modified → **skip** this bug (it's progressing through the lifecycle)
- If status is ASSIGNED and the bug has NO linked PRs:
  - Propose: "OCPBUGS-XXXXX is ASSIGNED to [name] but has no linked PRs. Move back to New?"
  - **Wait for user confirmation**
  - If confirmed: transition to New using `mcp__jira__jira_transition_issue` (transition_id=11), add comment using the "ASSIGNED->New (reassign)" template
- If status is New → continue to next actions

#### Action 2: Assess component
- Check if the component is a known PIXAA component (Console, OLM, Hive, Cloud Compute, CCO, CVO, OSUS, Serverless, HyperShift, or subcomponents)
- If obviously not PIXAA → **ask user**: "OCPBUGS-XXXXX component is [component]. This doesn't look like a PIXAA component. Transfer? To which component?"
- If unclear, assume correctly aligned and continue

#### Action 3: Assess release blocker
- Only if the bug appears to be a regression (has `component-regression` label or description mentions regression) AND priority is Critical or Major:
  - Propose: "OCPBUGS-XXXXX looks like a potential release blocker. Set release blocker to Approved or Rejected?"
  - **Wait for user input**

#### Action 4: Set priority
- If priority is Undefined:
  - Read the bug summary, description (via `mcp__jira__jira_get_issue` if needed), and comments to assess
  - Apply the manual's priority criteria:
    - CVE → normally Critical
    - Regression already shipped, customers affected → Major or Critical
    - High customer impact, no workaround → Major
    - Workaround exists, low impact → Normal
    - Cosmetic, no functional impact → Minor
  - Propose: "OCPBUGS-XXXXX: propose [Priority] — [one-line reasoning]"
  - **Wait for user confirmation**
  - If confirmed: update priority via `mcp__jira__jira_update_issue`, add comment using the priority template

#### Action 5: Assign engineer
- If assignee is Unassigned or was just unassigned in Action 1:
  - Match the bug's component to an engineer's expertise area
  - Pick the engineer with the lowest current bug count among matching candidates
  - Propose: "OCPBUGS-XXXXX ([component]): assign to [name] ([expertise], currently [N] bugs)?"
  - **Wait for user confirmation**
  - If confirmed: update assignee via `mcp__jira__jira_update_issue`

#### Action 6: Add `triaged` label
- If the bug doesn't have the `triaged` label:
  - Add it via `mcp__jira__jira_update_issue` (preserve existing labels, append `triaged`)
  - No user confirmation needed

#### Action 7: Handle unclear cases
- If the bug doesn't have enough information to assess (no description, no repro steps, missing logs)
- If the bug looks like a possible duplicate
- If the bug needs SME knowledge beyond the RIT team
- → **Pause and ask user**: "OCPBUGS-XXXXX: [describe the issue]. How do you want to handle this?"

#### Action 8: Record
- Append the bug to the "Triaged This Week" table in the tracker file
- Update the "Assignment Distribution" table with the new assignment
- If the bug was closed, add to the "Closed This Week" table

### Step 5: Final summary

After all bugs are processed, show:
- Total bugs processed
- Breakdown: triaged, skipped (POST/ON_QA), closed
- Updated assignment distribution table
- Any bugs that were paused/skipped for user follow-up

## Important Notes

- **Automate the obvious, pause on judgment** — adding `triaged` labels is auto. Priority, assignee, component, release blocker always get a proposal + user confirmation.
- **Always comment on status/assignee changes** — use the templates from rit_manual.md.
- **Preserve existing labels** — when adding `triaged`, keep all existing labels on the bug.
- **Respect PTO** — skip engineers marked as PTO in the roster.
- **Load balance** — always consider current bug count when proposing assignees.
- **One panel at a time** — the user decides which panel to triage and in what order.
- **If the Jira API can't update a field** (screen configuration error), tell the user to do it manually in the UI and continue with the next action.
