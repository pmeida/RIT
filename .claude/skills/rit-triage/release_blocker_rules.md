# Release Blocker Evaluation Rules

## Current Release

```
CURRENT_RELEASE = 5.0
```

Update this value when the GA target changes. The skill reads it during Step 1 and uses
it for all version-scoped evaluation (V-rules) and Component Readiness context.

---

These rules determine whether a PIXAA bug's Release Blocker field should be set to
**Approved**, **Proposed**, or **Rejected**. They apply to **.0 / y-stream / pre-GA
releases**. Source: [blocksnot](https://gitlab.cee.redhat.com/mworthin/blocksnot).

---

## Step 1 — Automatic Approve

If **any** of the following apply, propose **Approved**.

| ID | Criterion | What to look for |
|----|-----------|-----------------|
| A1 | **Component Readiness regression** | Summary or description references a CR regression; no approved SBAR exception exists |
| A2 | **Data loss, service unavailability, or data corruption** | Summary, description, or labels indicate any of these |
| A3 | **`ServiceDeliveryBlocker` label present** | Check labels |
| A4 | **SNO CPU budget exceeded** | Bug indicates Single Node OCP CPU usage exceeds 2 physical cores / 4 hyperthreads |
| A5 | **SD blocker with no acceptable workaround** | `ServiceDeliveryBlocker` label AND no workaround that is idempotent, deployable at scale, and implementable before the next Cincinnati channel push |
| A6 | **`UpgradeBlocker` label present** | Treat as Approved pending final assessment |
| A7 | **Tech-preview Component Readiness regression** | CR regression in a tech-preview job — essential for proving feature readiness |

---

## Step 2 — Conditional Approve

If no A-series rule matches but any of the following apply, propose **Proposed** and
flag for user judgment.

| ID | Criterion | Guidance |
|----|-----------|---------|
| C1 | **Failed installs or upgrades** | Broad scope → lean Approved; limited to a specific platform/form-factor → flag for stakeholder discussion |
| C2 | **Perception of a failed upgrade** | Users perceive the upgrade failed even if it technically succeeded |
| C3 | **Non-CR regression** | Regression found by Layered Product Testing, or regression in functionality not caught by Component Readiness |
| C4 | **New test failing 95% pass rate** | New tests (no prior-release basis) must meet a 95% pass rate; failure is treated as a blocker |

---

## Step 3 — Reject

If no A or C series applies, propose **Rejected**.

| ID | Criterion |
|----|-----------|
| R0 | **None of A1–A7 apply** — default rejection. Append: *"There is not enough detail in this bug to determine that it is a release blocker, and it will be rejected. If more detail is added indicating the blocker validity, it can be moved to Approved, or returned to Proposed for re-evaluation. None of the Automatic Approve criteria (A1–A7) are met."* |
| R1 | **Priority/severity below Important** — Normal, Minor, or Undefined. No bug below Important is a blocker |
| R2 | **Approved SBAR** — description or comments indicate OCP leadership approved an SBAR |
| R3 | **Issue no longer occurring in CI** — comments or test analysis confirm it is not reproducing |
| R4 | **Non-CR bug deemed safe to ship** — evaluated against the criteria above and found acceptable |
| R5 | **New-feature bug with no regression** — reject unless the feature itself is release-blocking. Check linked Epic/Feature; if none exists, **flag for human review** before auto-rejecting |

---

## Step 4 — Remain Proposed

Leave the field as **Proposed** (do not change it) when:

| ID | Criterion |
|----|-----------|
| P1 | Insufficient data in the card to apply the rules above |
| P2 | A "Discussion Needed" checkbox is set (Architecture Call, OCP Eng Mgmt, PM Sync, Program Call, SD Architecture Overview, etc.) |
| P3 | `UpgradeBlocker` label present but the conditional-update assessment has not concluded |
| P4 | Bug falls into a C-series category but the required stakeholder conversation has not happened yet |

---

## Evaluation Flow

1. Check **A1–A7** first. Any match → propose **Approved**.
2. No A match → check **C1–C4**. Any match → propose **Proposed**, note which criterion.
3. No A or C match → apply **R-series**. Propose **Rejected** with applicable rule ID(s).
4. Insufficient data for a clear call → propose **Proposed** (P1).

Always include the rule ID(s) and a one-line reason in your proposal:
> `OCPBUGS-XXXXX: Release Blocker → Approved [A1 — CR regression, no SBAR]?`

---

## Rejection Justification Requirements

Teams **must** provide justification in Jira when rejecting a bug in these categories:
data loss, service delivery blockers, regressions. If a workaround is the justification:
- It must be safe to apply **before** updating a cluster.
- It must be documented in **release notes**.
- It must have plans for **future automatic reversal**.

---

## Version-Specific Notes

These rules apply to the **current release** (see `CURRENT_RELEASE` above, currently **5.0**).
The Release Blocker field has a **different meaning for z-stream releases** — do not apply
these criteria to z-stream bugs without adjusting for that context.

When evaluating a bug against the current release, classify its **Affects Version** as:

| Classification | Meaning |
|---------------|---------|
| `current` | Matches `CURRENT_RELEASE` (x.y or x.y.0) — normal, evaluate as usual |
| `previous` | Older y-version — may be out of scope; check if a clone exists for current |
| `next` | x.y+1 — exists in the next release; check if a corresponding current-release bug exists |
| `z-stream` | x.y.N (N≥1) — z-stream rules apply, not these |
| `empty` | Flag: field should be populated for meaningful evaluation |

Only **Affects Version** is used for version-scoping (not Fix Version or Target Version).
If a bug's Affects Version points to a different y-version, flag it as potentially out of scope
for the current GA cycle.
