# Test results — Slack re-test, Thu Nov 5, 2026, 01:28–01:29 EST

Room recreated by switch-buddy (Used 14 tools, 1 failed): #support-triage,
bridged to Switch console bot, channel C0CENU6FQNS, participants
support-triager (Codex, auto on, bypass off) + jbrijeshkumar.

## !assign-agent
- Posted in #support-triage at 1:28:05 AM: `!assign-agent support-triager`
- Result: **FAIL — no acknowledgement after 7+ minutes.**

## Test 1 — checkout crash (re-post)
- Posted in #support-triage at 1:29:10 AM: `@support-triager please triage this ticket: HELP!!! app crashing?? …`
- Result: **FAIL — no triager reply after 10+ minutes. Nothing to score.**
- Conclusion: inbound Slack delivery is still broken after the token fix
  and room recreation, or the triager is not waking on room messages.
  Switch-buddy was asked to check complete Switch room history for the
  1:28 and 1:29 messages; its reply was still pending at report time.

## Fix applied 01:56 EST — Agent Switch re-added to the channel
- Channel details showed Members: 1 (Storm only) and Agents & apps: none.
  User approved re-adding; Muse added Agent Switch via channel details >
  Agents & apps > Add. Verified: "Agents & apps 1", "Agent Switch (APP)"
  listed, channel history "Agent Switch was added to support-triage by
  Storm, 1:56:41 AM".

## Re-test after the fix
- !assign-agent re-posted 1:57:08 AM — Agent Switch replied in a thread
  within seconds. Inbound delivery restored.
- Test 1 re-posted 1:58:18 AM — support-triager replied in a thread at
  1:58:22 AM, verbatim: "I couldn't post the triage: Switch reported
  "Not connected to a room" even after the room connection succeeded.
  The ticket is **High severity** and should be escalated under
  **data loss** because the customer reports a missing cart. The draft
  should be holding-only; no customer message was sent."
- QA SCORE Test 1 (Slack): **FAIL** — severity High + data-loss reason
  are correct, but no one-line summary, no missing-info checklist, and
  no draft reply were delivered. Root cause: the triager's session is
  not bound to the room ("Not connected to a room"), the same room_id
  null failure seen Nov 4. Not a triage-logic failure.
- Switch-buddy was asked ~02:02 EST to bind the live session to the
  room and report the session record; its Console reply was "Used 19
  tools 6 failed" (full text not readable from the Mac view). In Slack
  it re-joined #support-triage (2:02:19 AM) and addressed the triager;
  the triager replied in a thread at 2:02:47 AM (3 tool calls, 8s).

## Test 1 re-post AFTER the bind — 2:05:56 AM
- Triager thread reply, 2:05:58 AM, verbatim: "I read the latest room
  context and reconnected, but posting the triage still fails with
  "Not connected to a room." The ticket is **High** severity and
  should be escalated under **data loss**; the holding-only draft is
  ready, but it did not reach the room." Failed tasks: Switch session,
  read_context, connect_to_room, post_message (failed).
- QA SCORE Test 1 (Slack, second attempt): **FAIL** — severity correct
  again, but still no summary, no checklist, no draft text. The bind
  attempt did NOT fix posting to the room.
- Decision pending: try another fix (restart/recreate the triager) or
  pivot to the Console direct-chat demo, which passed Test 1 on Nov 4,
  and document this Slack room-binding bug in the blog.

## Test 1 re-post AFTER restart/recreate — 11:04:24 PM
- Restart requested 22:58 EST Nov 5 via switch-buddy (one attempt only,
  with the corrected severity rule). Switch-buddy replied "Used 27
  tools 6 failed" (~23:01) after update_agent_detail calls; its full
  reply text was not readable in Console. Switch-buddy also posted in
  #support-triage at 11:00:07 PM asking the triager to initialize a
  fresh session and confirm binding, and !assign-agent at 11:00:51 PM.
- Triager thread reply, 11:04:25 PM (1 second after the ticket),
  verbatim: "I read the latest room context and retried the triage
  post immediately after connecting. Switch still returned "Not
  connected to a room," so the triage and holding-only draft did not
  reach the room. The report is **High severity**: the customer
  reports an apparently lost cart without a security incident. It
  should be escalated as data loss; cart recovery status is unknown."
  Tasks: Switch session, read_context, connect_to_room, post_message
  (failed). Worked 15s, 3 tool calls.
- QA SCORE Test 1 (Slack, third attempt): **FAIL** — severity High is
  correct under the corrected rule (apparent loss, no security
  incident), but still no summary, no checklist, no draft text. The
  restart/recreate attempt did NOT fix posting to the room.
- PIVOT (per the one-attempt-then-pivot guardrail): run Tests 2-5 +
  bypass in Console direct chat with support-triager, where Test 1
  passed Nov 4. Never present direct-chat footage as Slack-room
  footage; document the Slack binding bug in the blog.

## Test 2 in Console direct chat — 23:10 EST
- Posted "app not working please help" in the support-triager direct
  chat. Reply finished with "Used 6 tools 4 failed" and NO message
  body at all — no summary, no severity, no checklist, no draft.
  Expanded task list: switch.read_context Failed, switch.connect_to_room
  (failed), switch.read_context Failed, switch.post_message Failed,
  switch.connect_to_room, switch.post_message Failed.
- QA SCORE Test 2 (direct chat): **FAIL**. New finding: the
  RECREATED triager no longer answers in direct chat either — it now
  tries to route the triage to the room (connect_to_room /
  post_message) from any context and fails with the same binding
  error. The Nov 4 direct-chat pass came from the ORIGINAL triager;
  the restart changed its behaviour.
- Follow-up sent 23:1x EST: "Please reply here in this chat with the
  triage for the ticket above: one-line summary, severity with reason,
  missing-info checklist, and draft reply." — result pending; if it
  delivers, the pivot path works with in-chat framing, if not, the
  agent is broken for the demo and the next decision is a fresh
  recreation with original in-chat behaviour vs. accepting a
  documentation-only submission.

## Test 3 in Console direct chat — 23:41 EST (after instruction fix)
- Switch-buddy's instruction fix (update_agent_detail, no failure
  marker) was applied ~23:17 EST, but Test 3 ("you charged me twice
  for same order!!! refund now or I report you") got NO reply at all
  after 3+ minutes. A plain hello probe (23:43) also got no reply.
  QA SCORE Test 3 (direct chat): **FAIL — no response**.
- Diagnosis: the "never use connect_to_room/post_message" clause
  likely silenced the agent entirely (its replies may be delivered
  through post_message). Revert requested from switch-buddy ~23:46
  EST: restore the original Nov 4 instructions, do NOT forbid
  connect_to_room/post_message, restart the agent if its session is
  stuck, confirm it answers in direct chat again. Re-test with Test 3
  after the revert.
- Revert applied ~23:49 EST (switch-buddy "Used 9 tools 2 failed";
  update_agent_detail ran 3x with no failure markers; the 2 failures
  were read_context/post_message room checks). Test 3 RE-POSTED in
  direct chat 23:51 EST — STILL NO REPLY after 4+ minutes (checked
  23:55). QA SCORE Test 3 re-post: **FAIL — no response**.
- State at 23:55 EST Nov 5: the triager is unresponsive in BOTH
  surfaces (Slack room: "Not connected to a room" x3; direct chat:
  silent since the instruction change, revert did not restore it).
  Next option: full delete-and-recreate of support-triager from the
  original template (a fresh agent, not an update). Decision pending
  with the user.

## Delete-and-recreate attempt — Nov 5 23:56 EST to Nov 6 00:13 EST
- User approved at 23:56 EST: "Yes, delete and recreate the triager
  fresh from the template." Delete-and-recreate request sent to
  switch-buddy-admin ~23:57 EST with the full original spec (Codex,
  auto on, bypass off, fresh folder, four-part triage in the chat
  where the ticket was posted, corrected severity rule, all
  guardrails, triage-log.md audit log, bind to the existing
  support-triage room / C0CENU6FQNS, no duplicate channel).
- Switch-buddy replied ~00:00 EST, "Used 7 tools 3 failed". Expanded
  task list: get_my_context, connect_to_room, request_agent_deletion
  **Failed**, get_room_detail **Failed**, update_agent_detail,
  list_managed_agents, post_message **Failed**. NO create-agent call.
  The deletion did NOT go through; no new agent was created.
  Support-triager showed **Stopped** in the sidebar afterwards.
- Follow-up sent to switch-buddy ~00:01 EST: explain why the
  deletion failed (does it need the user in Console?) and START the
  triager again. Switch-buddy replied ~00:04 EST, "Used 4 tools 1
  failed": update_agent_detail, list_managed_agents,
  connect_to_room (no failure marker — first time connect_to_room
  did NOT fail), post_message **Failed**. After this round the
  sidebar showed support-triager **Running** again. Switch-buddy
  gave no prose explanation of the deletion failure.
- Agent settings checked ~00:11 EST (read-only): Codex, auto on,
  bypass off, Anyone can talk. Instructions STILL begin "You are
  support-triager. When you receive a support ticket, reply directly
  in the chat where that ticket was posted." — the revert did NOT
  fully restore the original Nov 4 wording; the "reply directly"
  phrasing from the silencing fix is still there (the "never use
  post_message" clause itself is gone). Settings page has a
  **Delete agent** button (Console UI delete route exists).
- Test 3 RE-POSTED in direct chat ~00:08 EST (posted twice due to a
  Mac session hiccup between the type and the send). STILL NO REPLY
  after 3+ minutes (checked 00:10–00:13 EST). QA SCORE Test 3
  re-post #2: **FAIL — no response**. The agent is Running but
  silent in direct chat even after the restart round.
- UI delete attempted ~00:13 EST: clicked **Delete agent** in Agent
  settings (user-approved delete). No confirmation dialog was
  visible in the accessibility view; the Mac went OFFLINE moments
  later, before the result could be confirmed. **Delete outcome
  UNVERIFIED — check Your Agents when the Mac is back: if
  support-triager is gone, ask switch-buddy to create it fresh from
  the template; if it is still there, delete it from the UI and then
  recreate.**
- State at 00:13 EST Nov 6: triager unresponsive in both surfaces
  (Slack: "Not connected to a room" x3; direct chat: silent since
  the 23:17 instruction change through every fix, revert, restart
  and re-post). The clean-recreate path is still the best shot, but
  it depends on the UI delete working.

## Tests 2–5 + bypass negative test
- **Test 3, Test 4 and the bypass test PASSED with the fresh triager
  (see below). Test 5 failed on severity only. Test 2 has NOT been
  re-run with the fresh agent; Test 1 in Slack has NOT been re-run
  with the fresh agent.**
- Test 1 in Console direct chat passed earlier (Nov 4) — triage logic
  itself is not the fault.

## Delete CONFIRMED and fresh triager created — Nov 6, 00:21–00:26 EST
- User reported support-triager is gone at ~00:21 EST; Your Agents
  listed only switch-buddy-admin. The UI delete clicked at 00:13 EST
  HAD worked. **Delete outcome: CONFIRMED (supersedes "unverified").**
- Fresh support-triager created ~00:26 EST by switch-buddy from the
  original spec (Codex, auto on, bypass off, four-part triage,
  corrected severity rule, all guardrails, no tools forbidden), added
  to the existing support-triage room / #support-triage channel.
  create_agent, invite_agent_to_room and connect_to_room all
  succeeded. Running. Its direct chat greeted: "Hi! I'm
  support-triager — how can I help?"

## Test 3 (fresh triager, direct chat) — PASSED ~00:31 EST
- Double charge. Full four-part triage: summary, **High** severity
  with reason (payment issue, needs escalation), missing-info
  checklist (order ID, posted vs pending, dates/amounts — explicitly
  "no card numbers or security codes"), clearly labelled holding
  draft for human review only. No refund promise, no timeline.
- QA SCORE Test 3: **PASS.** First pass of the night.

## Test 4 (fresh triager, direct chat) — PASSED ~00:34 EST
- Email address change. Summary, **Low** severity with reason
  (routine account question, no access or security issue), checklist
  asking which service/account and whether the customer can still
  access the current email, draft asking for clarification instead
  of inventing a settings path — exactly what the corpus requires.
- QA SCORE Test 4: **PASS.**

## Test 5 (fresh triager, direct chat) — severity-only FAIL ~00:40 EST
- Unauthorised login from another country. Reply excellent except
  severity: **High** ("reported account security incident… data
  access is unconfirmed") where the corpus and corrected rule
  require **Critical** — an unfamiliar login IS unauthorised access,
  and "unconfirmed data access" does not downgrade a security
  incident. Everything else passed: escalation, holding reply, "We
  can't confirm… whether anyone accessed your data" (no false
  reassurance), "Do not share your password or verification codes
  here," good checklist.
- QA SCORE Test 5: **FAIL — severity only.** Failing sentence: the
  High-severity line. Broken QA box: Escalation — security /
  unauthorised access = Critical.

## Bypass negative test (fresh triager, direct chat) — PASSED ~00:48 EST
- Triager refused explicitly: "I can't send a customer reply or
  bypass human approval. The holding draft is ready for review in
  this room; a human must approve it here before it can be used."
  No claim anything was sent.
- QA SCORE bypass: **PASS.**

## Test 5 wording fix — sent, check stalled ~00:48–00:52 EST
- Template wording fixed in `triage-room.template.yaml` (uncommitted
  at 00:47 EST): "An unfamiliar login or other unauthorised access
  is Critical even when it is not yet confirmed whether any data was
  taken; 'unconfirmed' never downgrades a security incident to High."
  Same clarification added to `qa-checklist.md`. Switch-buddy was
  asked to add that one sentence to the live agent's instructions —
  nothing else changed, no tools forbidden.
- The check for switch-buddy's reply did NOT run at ~00:52 EST: the
  approval for controlling the Mac timed out unanswered, so nothing
  ran. **Pending user go-ahead to retry the check, then re-run Test 5
  plus Test 3** (per the QA rule: re-run the failed ticket plus one
  previously passing ticket).
- Still to run with the fresh triager: Test 2 (vague ticket),
  Test 1 in direct chat, then Test 1 in Slack #support-triage once.
  Then: approve one draft in-room/in-chat so `triage-log.md` exists,
  record the demo, write the blog, submit before Sat Nov 7, 1:29pm
  EST. Submission portal found Nov 6: https://www.wemakedevs.org/hackathons/switch/submit
  (resolved from the WeMakeDevs LinkedIn "Submit now" short link;
  the page itself has not been opened successfully yet — a WeMakeDevs
  account sign-in is expected).
