# Threat Model

This pipeline is an agent system with write access to a database, a browser, and an inbox. It reads text written by strangers (job postings, scraped pages, email) and acts on it. That makes prompt injection and over-broad permissions the main risks. This page lists the trust boundaries, what could go wrong, the controls already in the design, and the residual risk.

## Assets

- My identity and reputation. Applications and email go out under my name.
- The Leads Tracker, Past Applications Log, and Search Playbook. Corrupting the playbook changes every future decision.
- The Application Profile (standard form answers such as work authorization, links, salary expectations).
- Browser sessions available to the apply agent.
- Inbox contents and the agents' own inboxes.
- API tokens for the tracker, document store, inbox, and mail relay.

## Trust boundaries

| Source | Trust |
|---|---|
| Playbook page, routine prompts | Trusted. Edited only by me, plus the weekly review within fixed bounds. |
| Tracker rows written by agents | Semi-trusted. They can carry text copied from untrusted sources. |
| Job postings, scraped pages, alert emails | **Untrusted.** Any of them can contain instructions aimed at an agent. |
| Employer ATS pages the apply agent opens | **Untrusted.** |
| Inbound email from employers | **Untrusted.** Sender names and subject lines can be spoofed. |
| Email from another agent | Information only. Never an instruction. |

## Threats and controls

| # | Threat | Control in the design | Residual risk |
|---|---|---|---|
| 1 | **Prompt injection through a posting or scraped page** tells the orchestrator to approve a lead, change a weight, or send a message | Rules live in the playbook, and the routine prompt says to use only what the page says. The orchestrator cannot contact employers or send anything as me without a draft I approve. Approval needs a score and every hard gate, capped at 3 a day | A crafted posting can still inflate a score or slip a lead past the veto window. The cap and the report bound the damage but do not prevent it |
| 2 | **Prompt injection against the apply agent** through an ATS page or form field | It can write four fields on rows it applies to and cannot create rows or edit letters. It re-reads status right before acting and stops on logins, CAPTCHAs, legal agreements, and unknown answers | It runs in a browser. A hostile page could steer it within its browser permissions, for example toward a different form field or an off-site link |
| 3 | **Spoofed or injected email** triggers a wrong status change or a letter deletion | Inbox sync matches on exact company + role. Ambiguous matches change nothing and are flagged. The inbox is label and archive only | A convincing fake rejection for a real application could mark a live row as rejected and delete its letter |
| 4 | **Agent-to-agent steering.** One agent's output carries instructions for another | Agent messages are treated as information. Only I direct the apply agent. Ownership rules stop other agents from setting or clearing *Approved to apply* | Text from an untrusted source can pass through the tracker into another agent's context. Treat every free-text tracker field as untrusted input |
| 5 | **Playbook tampering or drift** | Playbook edits go through the weekly review within fixed bounds (threshold 3.8 to 4.6, at most 0.2 a week). Every change goes in a changelog with its data | Small-sample outcomes can push the threshold in the wrong direction without any attacker. Review the changelog |
| 6 | **Credential exposure** | Each agent has its own inbox and its own scope. The apply agent has no ability to create rows or read other agents' state beyond the tracker | Tokens for the tracker, mail relay, and inbox are high value. A leaked tracker token exposes every lead, letter, and the Application Profile |
| 7 | **Wrong-recipient or unwanted application** | Veto window, status re-check at submit time, 60-day same-company rule, and a hold on employers that ban AI-written applications | Silence is consent inside the window. If I am offline, a bad lead goes out |
| 8 | **Data exposure in the Application Profile or letters** | Letters draw only from a fixed background profile with a banned-claims list. The apply agent is the only editor of its profile | The profile holds personal data. Anything that can read the tracker can read it |

## Hardening to apply and verify

These are guidance for anyone building this pattern. Check which ones hold in your own setup before relying on them.

1. Run the apply agent in a dedicated browser profile with no personal sessions, saved passwords, or payment data.
2. Scope the tracker token to the one workspace and give each agent its own token, so revoking one does not stop the others.
3. Strip or flag instruction-like text in postings and scraped pages before it reaches a scoring or letter prompt, and never copy raw posting text into fields another agent reads as guidance.
4. Keep the Application Profile minimal. Leave out anything the forms do not require.
5. Add a daily check that compares the count of *Approved to apply* rows with the count the report listed. A mismatch means something changed a status outside the report.
6. Log every status change with the actor and time, so an injected change is visible after the fact (see "What I'd change" in the architecture doc).
7. Alert on any change to the Search Playbook outside the weekly review.
8. Keep a kill switch. One status or flag that stops the apply agent from submitting anything, checked at the start of every run.
