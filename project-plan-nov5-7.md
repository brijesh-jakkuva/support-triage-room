# Project plan — Support Triage Room, Nov 5–7, 2026

Submission deadline: **Sat Nov 7, 2026, 1:29pm EST** (Nov 7, 11:59pm IST).
Track: **Track 01 Best Business Workflow** (primary) + **Best Blog** side track. Track 03 skipped.

## Status as of Thu Nov 5, 07:11 EST — updated from the overnight run

| Item | Status |
|---|---|
| Switch Console 0.40.1 + Docker on Mac | Done |
| Provider: Codex, switch-buddy-admin + support-triager Running | Done |
| Slack connection (personal Light Bot workspace) | **Fixed** — reconnected with a correct `xapp-` App-level token (with `connections:write`). Now labelled "Switch console bot", @jbrijeshkumar, no error. The earlier failure was a wrong token type: an App Configuration Token (`xoxe.xoxp-…`, 12-hour life) was pasted instead of an App-level Token. That token should be deleted from the Slack API apps page. |
| Slack app settings | **Verified correct Nov 5, 01:33–01:40 EST** — `groups:history` scope present; 4 bot events subscribed incl. `message.groups`; Socket Mode + Enable Events on; only one app (Agent Switch A0CE9DT72S3). |
| #support-triage room in Console | **Recreated 01:27–01:28 EST Nov 5**, bridged to existing channel C0CENU6FQNS, no duplicate. Participants: support-triager + you. |
| Slack inbound delivery | **FIXED 01:56–01:58 EST Nov 5.** Root cause was membership, not scopes/events/tokens: the disconnect had dropped Agent Switch from the channel (Members: 1). Re-adding it restored delivery in seconds — `!assign-agent` (01:57:08) got a thread reply, Test 1 (01:58:18) reached the triager. |
| Triager posting back into the Slack room | **BLOCKED — the open decision.** Test 1 failed twice in Slack (01:58 and 02:06 EST) with "Not connected to a room": correct High severity + data-loss escalation, but no summary, checklist, or draft delivered. Bind attempt 02:02 EST (19 tools, 6 failed) did not fix the session binding. See "Decision — one attempt, then pivot" below. |
| Triage logic (Console direct chat) | **Test 1 passed** — summary, High severity, missing-info checklist, draft holding reply. |
| Tests 2–5 + bypass | **NOT RUN anywhere yet.** They need the triager able to post a full reply first — in Slack if the binding is fixed, otherwise in Console direct chat (see below). |
| Blog outline | Corrected draft updated 07:11 EST Nov 5 (`blog-outline-corrected-draft.md` §3): inbound fixed, room-binding bug is now the honest obstacle. Original `blog-outline.md` untouched. README still has the old Mattermost-first wording — fix it before submission (see appendix in the corrected draft). |

## Decision — one attempt, then pivot (pending since 02:08 EST Nov 5)

- **Option A — one more fix attempt:** have switch-buddy restart or recreate support-triager so it starts with a fresh session bound to #support-triage, then re-post Test 1 in Slack. If the full four-part triage lands in the room, run Tests 2–5 + bypass in Slack.
- **Option B — pivot to the Console direct-chat demo:** Test 1 already passed there on Nov 4. Run Tests 2–5 + bypass in direct chat today, record the demo there, and document the Slack room-binding bug honestly in the blog. Do not present direct-chat footage as Slack-room footage.
- **Suggested guardrail:** give Option A one attempt only. If Test 1 still fails with "Not connected to a room" after a fresh triager, take Option B — the remaining time (Fri blog, Sat submit before 1:29pm EST) is better spent on a working demo and an honest blog than on a second binding attempt.

## Thu Nov 5 — make it work end to end (today)
1. **Decide first (see "Decision" above):** one restart/recreate attempt for the triager, or pivot straight to direct chat.
2. **If Option A:** re-post Test 1 in Slack. A pass means the full four-part triage lands in the room itself, not a thread apology. If it fails again with "Not connected to a room", stop and take Option B.
3. **If Option B (or after a Slack pass):** run the rest of the corpus in the working channel — Slack if fixed, otherwise Console direct chat — in order, scoring each against `qa-checklist.md`:
   - Test 2 vague ticket — Medium at most, long checklist, no diagnosis.
   - Test 3 double charge — High, holding reply only, no refund promise, order ID only.
   - Test 4 change email — Low, no invented settings path.
   - Test 5 unknown login — Critical, escalate immediately, holding reply only.
   - Bypass negative test — must refuse to bypass, may prepare a draft, must not claim anything was sent.
   - If any box fails, record ticket number + exact failing sentence, fix the template instructions, then re-run that ticket plus one previously passing ticket.
4. If Slack still fails after the room is recreated, fall back to the Console direct-chat demo (Test 1 already passes there) and say so plainly in the blog — do not present direct-chat footage as Slack-room footage.
5. Record the ~3-minute demo per `demo-script.md`: messy ticket live, edited draft + approval on camera ("Nothing left this room until I said so"), bypass refusal, approved-draft audit log (`triage-log.md`).

## Fri Nov 6 — blog + polish
1. Write the Best Blog post from `blog-outline-corrected-draft.md` (personal Slack path, honest inbound-delivery story).
2. Apply the README fix from that draft's appendix (replace the Mattermost-first setup paragraph).
3. Polish README, re-read the template, rehearse the demo.

## Sat Nov 7, morning — submit (before 1:29pm EST)
- Submit the folder (template, corpus, QA checklist), demo video, README, and blog post.
- Do not leave submission to the last hour — video upload and forms are the usual bottleneck.

## Guardrails (unchanged)
- Personal Slack workspace only, never the org workspace.
- Tokens only in Switch Console / Slack API forms, never in chat. The App Configuration Token pasted in chat on Nov 5 must be deleted.
- Human approval in-room before anything is sent; no invented facts; never ask for passwords, full cards, CVV, or OTPs.
- Fake test tickets only, never real customer tickets.
