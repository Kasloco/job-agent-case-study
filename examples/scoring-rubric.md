# Scoring Rubric (sanitized)

This mirrors the live Search Playbook's configuration. Employer names and personal targets are generalized.

## How a score is computed

Score each factor 1–5, then take the weighted average, rounded to one decimal.

```
score = 0.25·lane + 0.25·family_history + 0.15·seniority
      + 0.10·location + 0.10·pay + 0.10·way_in + 0.05·freshness
```

| Factor | Weight | 5 | 3 | 1 |
|---|---|---|---|---|
| **Lane fit** | 0.25 | Company rolling out AI to its own people (adoption, implementation, enablement, transformation) | Vendor-side, but centered on change management and adoption, with no quota and no coding | Cut family or weak fit |
| **Role-family history** | 0.25 | The family where conversations have happened | Secondary lane with limited history | Cut family |
| **Seniority match** | 0.15 | Lead or manager of adoption / enablement / transformation | Mid-level | Director, Head, or VP titles; senior big-tech PM |
| **Location** | 0.10 | Remote US or a target metro | — (4 = elsewhere in the US, primary lane only) | Outside the US or off-list |
| **Pay vs. floor** | 0.10 | Posted at or above the floor | Not posted | Posted well below the floor |
| **Way-in strength** | 0.10 | Clear public path to the hiring manager or team | Plausible path, weakly documented | None, or only through an agency |
| **Posting freshness** | 0.05 | Posted within ~7 days and confirmed live | Live, older, or date unknown | Stale or closed |

Lane fit and role-family history overlap. A primary-lane role scores 5 on both, so half the total weight tracks one signal, and a 4.2 threshold in practice means primary lane. That is intended, but it means the other five factors mostly separate good primary-lane leads from average ones.

Lane fit 4 = a secondary-lane company (media) adopting AI internally. Family history 2 = families still allowed in small volume.

## Auto-approve threshold

| Setting | Value |
|---|---|
| Starting threshold | **4.2** |
| Bounds | **3.8 – 4.6** |
| Max change per weekly review | 0.2, and only from new outcomes |
| Max auto-approvals per day | 3 |
| Veto window | Until 11:45 AM (apply run ~11:50 AM) |

## Hard gates (all required)

1. Lane is the primary lane or the approved secondary lane.
2. Location is allowed.
3. Score ≥ threshold.
4. Posting is live.
5. A cover-letter PDF is linked on the row.
6. Role is not in a cut family.
7. No application to the same company in the last 60 days.

## Cut list

Dropped before scoring:

- Senior or big-tech product manager
- Director / Head / VP of AI
- Engineering roles, including forward-deployed engineer
- Technical program manager
- Any staffing-agency posting

## Role-family starting scores

| Family | Starting family score |
|---|---|
| Internal AI adoption (primary lane) | 5 |
| Media + AI (secondary lane) | 3 |
| Vendor-side AI deployment | 2 |
| Mid-level AI / solutions PM | 2 |
| Security | 2 |
| Customer-facing technical | 1 |
| Senior / big-tech PM | 1 (cut) |
| Program / TPM / product ops | 1 (TPM cut) |
| AI engineering / Director of AI | 1 (cut) |

## Worked example (fictional lead)

| Factor | Score | × Weight | = |
|---|---|---|---|
| Lane fit | 5 | 0.25 | 1.25 |
| Family history | 5 | 0.25 | 1.25 |
| Seniority | 5 | 0.15 | 0.75 |
| Location | 5 | 0.10 | 0.50 |
| Pay | 5 | 0.10 | 0.50 |
| Way-in | 3 | 0.10 | 0.30 |
| Freshness | 5 | 0.05 | 0.25 |
| **Total** | | | **4.8** → auto-approve if every gate passes |
