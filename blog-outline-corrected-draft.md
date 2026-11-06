# Best Blog outline — CORRECTED DRAFT (review copy, 2026-11-04)

This is a review copy only. The original `blog-outline.md` is untouched.
What changed, and why: the build no longer uses Mattermost. The room
runs in a brand-new personal Slack workspace plus Switch Console, and
the honest obstacle is now the Slack room-binding failure — inbound
delivery was fixed overnight, but the triager still cannot post a
triage back into the room (see §3).
Do not publish this draft until the Slack question in §3 is resolved
one way or the other — either the triager can post a full triage in
#support-triage, or the blog says plainly that the demo footage is
from Console direct chat, where Test 1 passed, and documents the
Slack room-binding bug instead of hiding it. Updated 2026-11-05,
07:11 EST, with the overnight results below.

Best Blog is judged on clarity, accuracy, and how much it helps a
first-time Switch user. Write for that reader, not for judges.

Title options:
- "I Built a Support Room Where the AI Drafts and a Human Decides"
- "Don't Let Your AI Send the Email: A Human-Gated Triage Room in Switch"

## 1. The mistake I wanted to avoid
A support AI that sounds confident and is wrong. One invented refund
promise is worse than a slow reply. That is why the human gate exists.

## 2. What Switch actually is (in plain words) — CORRECTED
Not a chatbot, not a new messaging app. Switch puts AI teammates into
the chat your team already uses — here, a brand-new personal Slack
workspace created just for this demo (not a work or organisation
workspace), bridged to Switch Console — and a room is where people
and agents share context and work together.
[Was: "here, Mattermost on your own machine" — that was the original
plan, abandoned before the room was built. Mattermost remains only as
a last-resort fallback in `slack-personal-workspace-setup.md`.]

## 3. Setup, step by step — CORRECTED
Switch Console on macOS, Docker, and one coding agent (Claude Code /
Codex / OpenCode). The ten-minute quickstart, what switch-buddy does,
and the one thing that tripped you up (write this honestly — it is
the most useful part for a first-time user):

The thing that tripped you up was Slack delivery, in two acts — and
the second act is still open. Act one, inbound, is now solved: after
the Nov 5 reconnect, tickets and `!assign-agent` posted in
#support-triage never appeared in Switch room history. The Slack app
side was verified correct on Nov 5, 01:33–01:40 EST (the `groups:history`
scope is present; exactly 4 bot events are subscribed, including
`message.groups`; Socket Mode and Enable Events are on; only one app,
Agent Switch A0CE9DT72S3, exists in Light Bot). The real cause was
membership: the disconnect had dropped Agent Switch from the private
channel (Members: 1, only the user). Re-adding it at 01:56 EST restored
inbound in seconds — `!assign-agent` got a thread reply at 01:57, and
Test 1 reached the triager at 01:58.

Act two, posting back, is the open bug. The triager now receives the
ticket but cannot post the triage into the room: twice (01:58 and
02:06 EST, Nov 5) it replied only in a thread with "Not connected to
a room", giving the correct High severity and data-loss escalation but
no summary, no missing-info checklist, and no draft. A bind attempt
by switch-buddy at 02:02 EST (19 tools, 6 failed) did not fix the
session binding. That is a Switch session/room-binding problem, not
triage logic — Test 1 passed in full in Console direct chat on Nov 4.
Do not present a Slack-room triage as working until a ticket posted
in Slack gets a full four-part reply in the room itself, not a thread
apology. If that is not fixed by submission, say so in the blog and
show the direct-chat demo honestly.

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

## 7. How to reproduce it — CORRECTED
Clone, load the template in Switch Console, create a personal Slack
workspace you administer (this keeps the demo outside any work
organisation — no org Slack admin needed, because you are the admin
of the new workspace), connect it in Console, paste the corpus, run
the QA checklist. If Slack inbound is not working for you, run the
same corpus in Console direct chat and say so — do not present
direct-chat footage as Slack-room footage.
[Was: "No Slack admin, no paid service beyond your own agent" — now
misleading, since the build does use Slack, just a personal one.]

---

## Appendix: matching README fix (not yet applied)
Replace the README paragraph that says "You do not need a Slack
workspace or admin access… When Switch runs on your own machine it
comes with Mattermost…" with:

"You do not need a work Slack workspace or an org admin to build or
demo this. Create a brand-new personal Slack workspace you administer,
connect it in Switch Console, and build and record the demo there.
Mattermost (local Docker) remains a fallback, not the demo path."

The same Mattermost-first wording also appears in
`setup-checklist.md` (Step 0, Step 3 example wording, Step 4
checkpoint) — those are internal checklists, not the blog, so they
were left for a separate pass and are flagged here rather than
silently rewritten.
