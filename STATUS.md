# STATUS — where this project stands (read this first)

**Last updated: Sat Nov 7, 2026, 01:45 EST. Deadline: Sat Nov 7, 1:29pm EST.**

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
| `README.md` | The project README: what it does, screenshots, results and metrics, how it works, try-it-yourself. No timeline or submission-process content. |
| `STATUS.md` | This file — current state and how to continue. |
| `triage-room.template.yaml` | The Switch room template (single `support-triager` agent, Codex, auto on, bypass off). The spec of record. |
| `test-corpus.md` | 7 test tickets + 1 bypass negative test, with expected severities. Tests 6 (exposed secret) and 7 (hallucination trap) added Nov 7, 01:00 EST. |
| `qa-checklist.md` | Pass/fail boxes every triager reply must satisfy. Secret-detection, grounding, and severity-calibration boxes added Nov 7. |
| `test-results-2026-11-05.md` | The full dated test log, Nov 4–Nov 7, 01:45 EST. The evidence. |
| `blog-draft.md` | Full Best Blog draft (~1,500 words, review copy, not published). Both [PENDING] notes resolved Nov 7, 01:00 EST (Test 5 re-run PASS, Slack Test 1 PASS). |
| `saturday-run-sheet.md` | Timeboxed submit-by-12:30pm EST plan for Sat Nov 7, with cutoffs and fallbacks. |
| `submission-checklist.md` | What submission needs: public repo (done), demo video, README, blog. Submission portal found Nov 6: https://www.wemakedevs.org/hackathons/switch/submit |
| `demo-script.md` | ~3-minute demo beats (messy ticket live, edited draft + approval on camera, bypass refusal, audit log). |
| `blog-outline-corrected-draft.md` | Corrected outline (personal Slack, honest two-act story). The outline the blog draft was built from; the stale original was archived Nov 7. |
| `slack-personal-workspace-setup.md` | The chosen chat path: brand-new personal Slack workspace, no org admin needed. |
| `docs/screenshots/` | Showcase screenshots (Slack triage reply, approval + audit log, Console direct chat) and the severity chart, all used in the README. |

Archived Nov 7, 2026 — kept locally in `~/workspace/support-triage-room-archive/`, not in the public repo: `blog-outline.md` (stale Mattermost wording), `mattermost-local-setup.md` (superseded fallback), `setup-checklist.md` (stale Mattermost wording, internal), `project-plan-nov5-7.md` (internal plan), `today-run-pack.md` (Nov 5 working notes), `severity-fix-draft.md` (superseded proposal — the fix is applied), `test-1-messy-ticket.md` (duplicate of Test 1 in the corpus).
| `submission-checklist.md` | What submission needs: public repo (done), demo video, README, blog. |

## 3. What is working

- **The spec, template, test corpus, and QA checklist** — complete, severity fix applied, README fixed to the personal-Slack wording.
- **Switch Console 0.40.1 + Codex provider + switch-buddy-admin** — all running on the MacBook Air; switch-buddy answers and acts in Console.
- **Slack inbound delivery** — fixed Nov 5, 01:56 EST. Root cause was membership: Agent Switch had been dropped from #support-triage when Slack was disconnected; re-adding it restored delivery. Verified: `!assign-agent` and Test 1 both reached the triager within seconds/minutes.
- **Slack app side** — fully verified: Agent Switch is the only app in the workspace, `groups:history` scope present, exactly 4 bot events subscribed (`message.channels`, `message.groups`, `message.im`, `message.mpim`), Socket Mode + Events on.
- **Triage logic itself** — Test 1 passed in Console direct chat on Nov 4 (full four-part triage, correct severity, checklist, holding draft). The agent knows how to triage; the failures below are delivery/binding failures, not triage failures.
- **Fresh support-triager (created Nov 6, 00:26 EST, Running)** — the UI delete worked, and the fresh agent created from the original spec now passes **everything**: direct chat **8/8 — Tests 1–7 PASS, bypass PASS** — and **Test 1 in Slack #support-triage PASSED at 12:47 AM Nov 7** (full four-part triage in the room, High severity, holding draft labelled "for human review (not sent)"). The "Not connected to a room" binding failure is gone. The demo can be filmed in Slack.
- **Two new guardrails, live and proven (Nov 7, 01:00–01:30 EST)** — secret detection (an exposed password/API key/token/card in a ticket is flagged, never repeated, customer advised to rotate it; Test 6 PASS) and grounding (every claim must come from the ticket text, gaps go in the checklist; Test 7 hallucination trap PASS after one severity-calibration fix — Low to Medium, then Test 5 regression still Critical). **Test 6 also PASSED in Slack** (user-posted 1:35 AM, directly observed): full triage in the channel, High, no password repetition. **The full corpus passed in Slack too** — user-confirmed ~01:44 EST Nov 7 (Tests 2–5, 7, bypass all passed; Tests 1 and 6 directly observed by Muse). Slack scorecard: **8/8 + bypass**, matching direct chat.
- **Human gate + audit log proven end to end (Nov 7, ~01:40 EST).** The Test 1 Slack draft was approved in its thread ("Approved — this draft is good as-is. Please log it to triage-log.md.") and the triager replied "Logged the approved cart-loss ticket draft to triage-log.md." **triage-log.md now exists** (agent-confirmed).
- **This repo** — public at https://github.com/brijesh-jakkuva/support-triage-room. Test results, STATUS, and blog draft through Nov 7, 01:00 EST are committed locally and pushed (see §5).

## 4. What is broken (the live problem)

**Nothing is currently broken.** Both live problems from Nov 6 are resolved:

- **Test 5 severity — FIXED and verified.** The template wording fix was applied to the live agent (switch-buddy, `update_agent_detail`, no failure marker, verified Nov 7, 00:28 EST). The Test 5 re-run at ~00:29 EST says **Critical** with the exact corrected reasoning ("unauthorized access, which is a security incident; whether data was taken is unconfirmed").
- **Slack room posting — FIXED and verified.** The fresh agent's Test 1 in #support-triage at 12:47 AM Nov 7 delivered the full four-part triage in the room (thread reply, 17s). No "Not connected to a room" error. The binding failure that blocked Nov 4–5 is gone.

What is still missing is not a bug: the demo video is not filmed; the blog is a review draft, not published. The audit log now exists (see §3). See §5.

## 5. What is pending (in order)

1. **Record the ~3-minute demo** per `demo-script.md` — filmable in Slack, since the room works, and the audit log now exists to show on camera. Saturday cutoff: 09:00 EST stop filming new material.
2. **Blog:** the draft (`blog-draft.md`) has both [PENDING] notes resolved (Test 5 re-run PASS, Slack Test 1 PASS) plus the Tests 6–7 update. Edit/approve the text, then publish. The stale original outline was archived Nov 7, so the outline question is closed.
3. **Submit before Sat Nov 7, 1:29pm EST** (repo + demo video + README + blog link) at https://www.wemakedevs.org/hackathons/switch/submit — the page is confirmed to load; sign in with the WeMakeDevs account, confirm what the form asks for, and confirm the submission went through. Aim for 12:30pm EST; do not leave it to the last hour.

## 6. Tools, software, and bots used

| Tool / bot | Version / identity | What it does here |
|---|---|---|
| **Switch Console** | 0.40.1, macOS Apple Silicon, in /Applications | The desktop app; runs the local Switch server, agents, rooms, and direct chats. |
| **switch-buddy-admin** | Agent, Codex, on this computer, Running | The admin assistant inside Console. Creates/updates agents and rooms, runs diagnostics. It created the triager and the room, and attempted the bind, restart, instruction fix, revert, and delete. Its replies in Console usually show only a "Used N tools" header — expand it to see which tools ran and which failed. |
| **support-triager** | Agent, Codex, auto on, bypass off, fresh folder | The triage agent. The product. Fresh agent created Nov 6, 00:26 EST; direct chat 8/8 (Tests 1–7 + bypass) and Slack Test 1 PASS Nov 7, 12:47 AM. Secret-detection, grounding, and severity-calibration guardrails added Nov 7, 01:00–01:30 EST. |
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
- Loose ends: confirm the exposed App Configuration Token from Nov 5, 01:11 was deleted on the Slack API apps page (still unverified); the submit page (https://www.wemakedevs.org/hackathons/switch/submit) is confirmed to load but still needs opening with the WeMakeDevs account to confirm its fields.
