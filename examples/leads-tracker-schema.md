# Leads Tracker Schema

The working database. One row per lead. All agents read it, and each writes only the fields in its scope.

| Field | Type | Purpose | Written by |
|---|---|---|---|
| Company | Title | Employer name | Orchestrator, Sourcing agent |
| Role | Text | Exact posting title | Orchestrator, Sourcing agent |
| Link | URL | Posting on the employer's own board, not a mirror | Orchestrator |
| Location | Text | City / hybrid / remote | Orchestrator |
| Salary | Text | Posted range, or "not posted" | Orchestrator |
| Posted | Text | Posting date if known | Orchestrator |
| Source | Text | Where the lead came from (board, alert, web search, sourcing agent, inbox) | Orchestrator, Sourcing agent |
| Fit | Text | Score, lane, and a one-line rationale | Orchestrator |
| Rank | Text | Priority within the day's batch | Orchestrator |
| Red flags | Text | e.g. "bans AI-written applications", "on-site only", "7+ yrs required" | Orchestrator |
| Cover Letter | URL | Link to the tailored letter | Orchestrator |
| Resume version | Select: A–E | Which resume variant to send | Orchestrator |
| Apply route | Text | Which ATS, or direct email | Orchestrator |
| Status | Select | See below | See below |
| Date applied | Date | Set when submitted | Apply agent, Orchestrator (inbox sync) |
| Next step | Text | What happens next, or why it's blocked | All, within scope |
| Notes | Text | Audit lines: auto-approval tag, "Applied by apply agent", Way-in note | All, append-only |
| Archive | Checkbox | Hides rejected rows from the working view after 2 days | Relay agent |

## Status options

| Status | Meaning | Who sets it |
|---|---|---|
| Not applied | Sourced, scored, letter attached, awaiting a decision | Orchestrator, Sourcing agent |
| Approved to apply | Approved by me, or auto-approved and not vetoed | Me; Orchestrator (auto-approve only) |
| Needs human | Apply agent blocked; reason in Next step | Apply agent |
| Applied | Submitted | Apply agent; Orchestrator from confirmation emails |
| Phone screen | Recruiter screen scheduled or done | Orchestrator (inbox sync) |
| Interviewing | Later rounds | Orchestrator (inbox sync) |
| Offer | Offer received | Orchestrator (inbox sync) |
| Rejected | Declined by employer | Orchestrator (inbox sync) |
| Withdrawn | I withdrew | Me |
| Posting Closed | Posting no longer live | Orchestrator (liveness), Apply agent |
| Passed | I passed or vetoed | Me; Orchestrator (carrying out a veto) |
| Fix link | Link broken or a mirror | Apply agent, Orchestrator |

## Past Applications Log

| Field | Type |
|---|---|
| Company | Title |
| Role | Text |
| Posting URL | URL |
| Final Status | Select: Rejected, Posting Closed, Withdrawn, Passed |
| Date applied | Date |
| Rejected/closed date | Date |
| Removed on | Date |
| Notes | Text |
