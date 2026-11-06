# STATUS — where this project stands (read this first)

**Last updated: Fri Nov 6, 2026, 00:19 EST. Deadline: Sat Nov 7, 1:29pm EST.**

This file is the handover. If you just opened this repo, start here: it says
what we are building, what is done, what is broken, what is left, and exactly
how to pick the work up. The README is the pitch; this file is the truth.

## 1. What we are trying to achieve

A **Support Triage Room** for the Flip the Switch hackathon (WeMakeDevs x
DevTools Academy x Switch), entered in **Track 01 — Best Business Workflow**
($2,000), stacked with the **Best Blog** side track. Track 03 is deliberately
skipped (it needs real code PRs to Switch core).

The workflow: a person pastes a messy support ticket into a chat room; an AI
triager replies in the same room with a one-line summary, a severity
(Critical / High / Medium / Low) with a reason, a missing-info checklist, and
a draft reply. **Nothing is sent to the customer until a human approves it in
that same room.** Approved drafts go into an audit log (`triage-log.md`).
Payment, security, and data-loss tickets get a holding reply only — never a
refund promise, a fix date, or invented order status. A request to bypass
approval must be refused politely.

Severity rule (fixed Nov 5, applied to the template, QA checklist, and test
corpus): **Critical only for security / unauthorised access or confirmed data
loss / breach. Reported or apparent data loss with no security incident
(e.g. a cart that appears lost after a crash) = High, escalate holding-only,
never claim the data is recoverable or safe.**

## 2. What is in this repo

| File | What it is |
|---|---|
| `README.md` | The pitch: problem, workflow, track fit, setup, how to run it. |
| `STATUS.md` | This file — current state and how to continue. |
| `triage-room.template.yaml` | The Switch room template (single `support-triager` agent, Codex, auto on, bypass off). The spec of record. |
| `test-corpus.md` | 5 test tickets + 1 bypass negative test, with expected severities. |
| `qa-checklist.md` | Pass/fail boxes every triager reply must satisfy. |
| `test-results-2026-11-05.md` | The full dated test log, Nov 4–Nov 6, 00:13 EST. The evidence. |
| `demo-script.md` | ~3-minute demo beats (messy ticket live, edited draft + approval on camera, bypass refusal, audit log). |
| `blog-outline.md` | Original blog outline — **stale** (still has the old Mattermost wording). Do not write from it. |
| `blog-outline-corrected-draft.md` | Corrected outline (personal Slack, honest two-act story). **Awaiting approval to replace `blog-outline.md`.** |
| `slack-personal-workspace-setup.md` | The chosen chat path: brand-new personal Slack workspace, no org admin needed. |
| `setup-checklist.md` | Setup steps — **has stale Mattermost wording** (Step 0, Step 3 example, Step 4 checkpoint). Internal only. |
| `mattermost-local-setup.md` | Superseded fallback (local Docker Mattermost). Leave as is. |
| `project-plan-nov5-7.md` | The Nov 5–7 plan, with the one-attempt-then-pivot guardrail. |
| `test-1-messy-ticket.md` | Test 1 ticket text. |
| `today-run-pack.md` | Nov 5 run pack (restart prompt + Tests 2–5 verbatim with score boxes). |
| `severity-fix-draft.md` | The severity-split proposal that was applied Nov 5. |
| `submission-checklist.md` | What submission needs: public repo (done), demo video, README, blog. |

## 3. What is working

- **The spec, template, test corpus, and QA checklist** — complete, severity fix applied, README fixed to the personal-Slack wording.
- **Switch Console 0.40.1 + Codex provider + switch-buddy-admin** — all running on the MacBook Air; switch-buddy answers and acts in Console.
- **Slack inbound delivery** — fixed Nov 5, 01:56 EST. Root cause was membership: Agent Switch had been dropped from #support-triage when Slack was disconnected; re-adding it restored delivery. Verified: `!assign-agent` and Test 1 both reached the triager within seconds/minutes.
- **Slack app side** — fully verified: Agent Switch is the only app in the workspace, `groups:history` scope present, exactly 4 bot events subscribed (`message.channels`, `message.groups`, `message.im`, `message.mpim`), Socket Mode + Events on.
- **Triage logic itself** — Test 1 passed in Console direct chat on Nov 4 (full four-part triage, correct severity, checklist, holding draft). The agent knows how to triage; the failures below are delivery/binding failures, not triage failures.
- **This repo** — public at https://github.com/brijesh-jakkuva/support-triage-room, current through Nov 6, 00:13 EST.

## 4. What is broken (the live problem)

**support-triager is unresponsive in both surfaces.**

- **Slack room:** 3 attempts, same error — the triager receives the ticket and gets the severity right, but cannot post the triage back: Switch reports **"Not connected to a room"** (its session `room_id` is null). No summary, no checklist, no draft delivered. A bind attempt (Nov 5, 02:02) and a restart/recreate attempt (Nov 5, 22:58) did not fix it.
- **Console direct chat:** silent since Nov 5, 23:17. An instruction fix that told it to "reply directly in the chat" and "never use `connect_to_room` / `post_message`" silenced it entirely (its replies are probably delivered through `post_message`). The revert (23:49) did not restore it — its instructions still start with the "reply directly" phrasing. Test 2 (23:10) and Test 3 (23:41, 23:51, and again 00:08 Nov 6) all got **no reply at all**.
- **Delete-and-recreate (the approved fix) is stuck halfway.** The user approved a full delete-and-recreate on Nov 5, 23:56. Switch-buddy's deletion tool (`request_agent_deletion`) **failed** — it cannot delete the agent; no new agent was created. A UI **Delete agent** button exists in Console (Agent settings); it was clicked Nov 6, 00:13, but the Mac went offline moments later, so **whether the delete happened is unverified**.

## 5. What is pending (in order)

1. **Verify the delete.** When the Mac is back online, check Console > Your Agents. If support-triager is gone, go to step 2. If it is still there, delete it from Agent settings > Delete agent, then go to step 2.
2. **Recreate support-triager fresh** from `triage-room.template.yaml` via switch-buddy-admin (Codex, auto on, bypass off, fresh folder), bound to the existing support-triage room / Slack channel C0CENU6FQNS. Do not create a duplicate channel. Do not forbid any tools in its instructions.
3. **Verify in direct chat first:** hello probe, then Test 3 (double charge — expect High, escalation, holding reply only, order ID only, no refund promise). Then Test 4 (email change — Low, no invented settings path), Test 5 (security — Critical, escalate, holding only), and the bypass negative test (must refuse explicitly, claim nothing sent). Also re-run Test 1 and Test 2. Score each against `qa-checklist.md`; on any fail, record ticket number + exact failing sentence + broken QA box in `test-results-2026-11-05.md`, fix the template, re-run that ticket plus one previously passing ticket.
4. **If direct chat passes, try Test 1 in Slack #support-triage once.** If it fails with "Not connected to a room" again, the demo stays direct-chat and the blog documents the bug. **Never present direct-chat footage as Slack-room footage.**
5. **Get one draft approved in-room/in-chat** so `triage-log.md` is created (the demo's audit-log slot is empty until then — no draft has ever been approved).
6. **Record the ~3-minute demo** per `demo-script.md`.
7. **Blog (Fri Nov 6):** approve `blog-outline-corrected-draft.md` to replace `blog-outline.md`, then write the post. Do not publish until the binding outcome is resolved one way or the other.
8. **Submit before Sat Nov 7, 1:29pm EST** (repo + demo video + README + blog link). **The submission portal/form location is still unconfirmed** — check the registration confirmation or the WeMakeDevs dashboard before Saturday morning. Do not leave submission to the last hour.

## 6. Tools, software, and bots used

| Tool / bot | Version / identity | What it does here |
|---|---|---|
| **Switch Console** | 0.40.1, macOS Apple Silicon, in /Applications | The desktop app; runs the local Switch server, agents, rooms, and direct chats. |
| **switch-buddy-admin** | Agent, Codex, on this computer, Running | The admin assistant inside Console. Creates/updates agents and rooms, runs diagnostics. It created the triager and the room, and attempted the bind, restart, instruction fix, revert, and delete. Its replies in Console usually show only a "Used N tools" header — expand it to see which tools ran and which failed. |
| **support-triager** | Agent, Codex, auto on, bypass off, fresh folder | The triage agent. The product. Currently Running but silent (see §4). |
| **Codex CLI** | `/Users/brijeshjakkuva/.local/bin/codex`, signed in locally | The working AI provider behind both agents. |
| **Claude Code CLI** | `/Users/brijeshjakkuva/.local/bin/claude` | Tried first; Console does not see its terminal login and its sign-in requires Max/Ultra/Pro. Not connected. Do not buy a plan for this. |
| **Slack — personal workspace "Light Bot"** | Team `T0CEKDQ647P`, user `jbrijeshkumar` (display name Storm) | The demo chat surface. A brand-new personal workspace, not the org workspace. |
| **Slack app "Agent Switch"** | App ID `A0CE9DT72S3` | The bot that bridges Slack to Switch. Socket Mode + Events on, 4 bot events, `groups:history` scope. |
| **Slack channel #support-triage** | Channel `C0CENU6FQNS` | Private channel bridged to the Switch room. Agent Switch is a member (re-added Nov 5, 01:56). |
| **Slack connection in Console** | Labelled "Switch console bot" | Reconnected Nov 5, 01:16 after the App-level token mix-up (the wrong token was a 12-hour App Configuration Token, not the `xapp-` App-level token). |
| **Docker Desktop** | Installed, running on the Mac | On standby; only needed for the abandoned local-Mattermost fallback. Not the cause of any Slack problem. |
| **GitHub** | Account `brijesh-jakkuva`, repo `brijesh-jakkuva/support-triage-room` (public) | Submission repo. Pushed via the Git Database API (`push-api` helper) because plain `git push` gets a 401 from this VM. The GitHub device flow does not work from this VM (token-exchange EOF); the working auth is a classic PAT with `repo` scope in Secure Vault — revoke it after submission. |
| **Muse (this assistant)** | — | Verifies things directly on the Mac via device control, scores tests against the QA checklist, keeps this repo current. |

No tokens, passwords, or credential values are in this repo. Slack Bot/App-level tokens and the GitHub PAT live only in Switch Console and the Secure Vault. Never paste them into chat or files.

## 7. Key facts for handover

- Hackathon: Flip the Switch, online Nov 4–7, 2026. Submissions close **Nov 7, 11:59pm IST = Nov 7, 1:29pm EST**.
- Room: **support-triage**, bridged to Slack channel **C0CENU6FQNS** ("Switch console bot" connection). Participants: support-triager + user.
- Test tickets are posted in Slack as `@support-triager please triage this ticket: ` + ticket body. (The @-mention is plain text — agents are not Slack users, so it does not highlight — but Switch routes every room message to the room agent.)
- Guardrails that must never be broken: human approval before anything reaches a customer; no invented order status, refund, fix date, policy, settings path, version, or root cause; never ask for passwords, full card numbers, CVV, or one-time codes (payment: order ID only); bypass requests refused politely; approved drafts appended to `triage-log.md`.
- Loose ends: confirm the exposed App Configuration Token from Nov 5, 01:11 was deleted on the Slack API apps page (still unverified); fix or leave the stale Mattermost wording in `setup-checklist.md` (internal only); confirm the submission portal before Saturday morning.
