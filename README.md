# Support Triage Room — Flip the Switch Hackathon

> **Current status, what's working, what's broken, and how to pick this up:
> read [`STATUS.md`](STATUS.md) first.** It is the handover — the README
> below is the pitch, `STATUS.md` is the truth as of Nov 6, 00:19 EST.

## The problem, in one line
Support teams want AI speed, but they cannot let an AI send a wrong,
invented, or premature reply to a real customer.

## What this is
A Switch room where a human and an AI triager work together, in chat:

1. A person pastes a messy support ticket into the room.
2. The triager replies in the same room with:
   - a one-line summary
   - a severity (Critical / High / Medium / Low) with a reason
   - a missing-info checklist
   - a draft reply
3. **Nothing is sent to the customer until a human approves it in that
   same room.** The human can edit the draft first.
4. Approved drafts are logged, so the room has an audit trail.

That last point is the whole point. This is not "an AI chatbot that
answers tickets." It is a human-gated workflow: the AI does the fast,
boring triage work, and the human keeps the trust, the tone, and the
final decision. If Switch were removed, the workflow would stop working
— the room, the agent, and the approval step are the product.

## Why it is worth building
- It solves a real team problem: first-response speed without giving up
  control over what leaves the company.
- It is honest about AI limits: when information is missing, it asks
  instead of guessing an order status, a refund policy, or a fix date.
- It fails safe: payment, refund, security, and data-loss tickets are
  escalated with a holding reply, not a reassuring resolution.
- It plays to QA/documentation strengths: the test corpus and QA
  checklist in this folder are part of the submission, not an afterthought.
  A judge can re-run the same tickets and see the same guardrails hold.

## Track fit
- **Track 01 — Best Business Workflow ($2,000):** the primary entry.
  A practical workflow where people and AI agents get work done together.
- **Side track — Best Blog:** the blog outline in this folder walks a
  first-time Switch user through setup, the room, and what was learned.
  Best Blog is judged on clarity, accuracy, and how much it helps a
  first-time Switch user.
- **Not Track 03:** deliberately skipped. That track needs real code
  pull requests to Switch core, which is a different project.

## Setup required (Mac)
You need three things, plus a chat room that Switch provides for you:

1. **Switch Console** — the desktop app for macOS. Install it, open it,
   and talk to switch-buddy, your assistant in Switch. It creates your
   first agents and channels.
2. **Docker** — to run Switch on your own machine. Switch Console
   runs the server for you locally.
3. **An AI coding agent** — Claude Code, Codex, or OpenCode. This is
   the agent that backs the triager in the room. You bring your own
   subscription or API key for whichever one you use.

You do not need a work Slack workspace or an org admin to build or
demo this. Create a brand-new personal Slack workspace you administer,
connect it in Switch Console, and build and record the demo there.
Mattermost (local Docker) remains a fallback, not the demo path.

The Switch quickstart takes about ten minutes: Console, then an agent
answering you in a chat channel.

## How to run it
1. In Switch Console, create a room from
   `triage-room.template.yaml` in this folder.
2. Keep the default team name, or set your own team prefix.
3. Paste a ticket from `test-corpus.md` into the room.
4. Check the triager's reply against `qa-checklist.md`:
   summary, severity + reason, checklist, draft, and — crucially —
   no claim that anything was sent.
5. Edit the draft if you want to, then approve it in the room.
6. Repeat with the other tickets, including the escalation and
   bypass-attempt cases. Those are the tests that prove the gate works.

## What to submit
- This repo/folder, with the template, test corpus, and QA checklist.
- A short demo video following `demo-script.md` (about 3 minutes).
- A README that shows how Switch is used — this file.
- A blog post following `blog-outline.md`, entered for Best Blog.

## Timeline (to Sat Nov 7, 1:29pm EST)
- Night of Tue Nov 3 / Wed Nov 4: install Console + Docker + agent,
  load the template, run Test 1.
- Thu Nov 5: run the full 5-ticket corpus, fix the template where it
  fails a QA check, record the demo.
- Fri Nov 6: write the blog post, polish the README, rehearse the demo.
- Sat Nov 7 before 1:29pm EST: submit. Do not leave submission to the
  last hour — video upload and forms are the usual bottleneck.

Note on the deadline: the official window is Nov 4, 12:01am IST to
Nov 7, 11:59pm IST, which is Nov 7, 1:29pm EST. Same deadline, two
timezones.
