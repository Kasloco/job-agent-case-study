# Portfolio / LinkedIn Blurb (draft)

## Short (LinkedIn "Featured" or project caption, ~60 words)

I built a multi-agent system that runs my job search, with human approval. One agent sources and scores leads against a written playbook and drafts tailored letters. A second applies only to roles I've approved or didn't veto. A weekly review retunes the scoring from real outcomes. It's built around fit over volume.

## Medium (portfolio card or post, ~150 words)

**Assisted job search: a multi-agent pipeline with human approval**

I treated my job search like an internal AI rollout. Four agents share one Notion tracker, each with a narrow job and narrow permissions. An orchestrator sources leads, scores them on seven weighted factors, writes a tailored cover letter for each, and auto-approves at most three a day. I get a short report and a veto window. An apply agent then submits only the rows that are still approved, and stops and flags me when it hits a login or a question it can't answer. An inbox sync keeps statuses current, and a weekly review retunes the weights within fixed bounds.

The most useful step wasn't automation. It was reviewing my own application history, which showed that targeted internal AI adoption roles were where conversations happened. So the system is built around fit over volume.

Stack: Grok Bot, Claude Code, Notion, Google Drive, Gmail, AgentMail, Firecrawl, Discord.

[Link to repo]

## One-liner (résumé project line)

Designed and run a four-agent, human-in-the-loop job-search pipeline (sourcing, scoring, tailored letters, veto-window auto-apply, outcome-driven weight tuning) on Notion, Grok Bot, and Claude Code.
