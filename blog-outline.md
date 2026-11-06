# Best Blog outline — written for a first-time Switch user

Best Blog is judged on clarity, accuracy, and how much it helps a
first-time Switch user. Write for that reader, not for judges.

Title options:
- "I Built a Support Room Where the AI Drafts and a Human Decides"
- "Don't Let Your AI Send the Email: A Human-Gated Triage Room in Switch"

## 1. The mistake I wanted to avoid
A support AI that sounds confident and is wrong. One invented refund
promise is worse than a slow reply. That is why the human gate exists.

## 2. What Switch actually is (in plain words)
Not a chatbot, not a new messaging app. Switch puts AI teammates into
the chat your team already uses — here, Mattermost on your own machine —
and a room is where people and agents share context and work together.

## 3. Setup, step by step
Switch Console on macOS, Docker, and one coding agent (Claude Code /
Codex / OpenCode). The ten-minute quickstart, what switch-buddy does,
and the one thing that tripped you up (write this honestly — it is
the most useful part for a first-time user).

## 4. The template, explained line by line
What each param does (team, provider, location, bridge), what the
agent instructions enforce, and why the room includes the creator as
the approver. Link the template file.

## 5. Five tickets, five lessons
Walk through the test corpus: checkout crash, vague ticket, double
charge, simple question, security incident. Show a real reply for at
least two, and name what failed on the first run and how you fixed
the instructions.

## 6. What I would do next
Real integrations (a ticket system, a knowledge base), a second agent
for reproduction, and the limits: this room drafts and triages, it does
not resolve billing or security cases on its own — by design.

## 7. How to reproduce it
Clone, load the template in Switch Console, paste the corpus, run the
QA checklist. No Slack admin, no paid service beyond your own agent.
