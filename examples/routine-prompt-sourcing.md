# Example Routine Prompt: Daily Sourcing Scan (generic)

A sanitized version of the scheduled prompt the orchestrator runs each weekday at about 10:35 AM. Real page IDs, names, and target employers are removed.

---

> **Daily sourcing scan.** Quality over volume.
>
> **1. Load the rules.** Read the Search Playbook page: weights, threshold, hard gates, cut list, lane quotas, letter rules. Do not use remembered values. Use only what the page says today.
>
> **2. One tracker read.** Run one full read of the Leads Tracker and one of the Past Applications Log. Rate limits are tight, so do not query again this run. Work from this snapshot for dedupe and counts.
>
> **3. Source.** Search employer job boards for the target titles, check job-alert emails received since the last run, run the web-search source (experimental: tag those rows `Source: web-search test`), and pick up rows the sourcing agent added since yesterday.
>
> **4. Filter before scoring.** Drop anything that fails location, is in a cut family or posted by a staffing agency, is well below the pay floor, isn't live on the employer's own board, or matches an existing row or log entry on company + role. Never re-add a requisition I was rejected from, even under a new ID.
>
> **5. Score** each survivor 1–5 on the seven playbook factors. Record score, lane, and a one-line rationale in Fit.
>
> **6. For each lead you add:** write a tailored cover letter following the letter rules (background profile only, no invented tools or experience, banned words list), export a PDF, link it in Cover Letter, and add a Way-in note from public information only. Do not contact anyone.
>
> **7. Auto-approve** at most 3 rows that clear the threshold *and* every hard gate. Set Status to `Approved to apply` and append to Notes: `Auto-approved <date>, score <x>. Veto by 11:45 AM.` If the posting forbids AI-written applications, do not auto-approve. Hold it for me and flag it for the apply agent to skip.
>
> **8. Report to me in chat,** in short plain prose: auto-approved leads (role, location, pay, score, why it fits, Way in, letter link) with the veto deadline; strong leads held and why; per-lane counts against the weekly quota; and what came from the experimental source. Then send the summary email to the relay agent.
>
> **9. Never** apply, email an employer, or change a row's status away from `Approved to apply`, except to carry out my veto.
