# Saturday run sheet — submit by 12:30pm EST, deadline 1:29pm EST

**Written Fri Nov 6, ~15:15 EST. Deadline Sat Nov 7, 11:59pm IST = 1:29pm EST. Aim to submit by 12:30pm EST; the last hour is buffer, not working time. Submit at https://www.wemakedevs.org/hackathons/switch/submit (page confirmed to load Nov 6; the form itself needs a WeMakeDevs sign-in, so open it first and confirm what it asks for).**

## Where things stand (Fri afternoon)

- Fresh `support-triager` (created Nov 6, 00:26 EST) passes in Console direct chat: Test 3 ✅, Test 4 ✅, bypass ✅. Test 5 ❌ severity only (High, should be Critical) — template wording fixed, live-agent update sent to switch-buddy, check stalled 00:52 EST on a timed-out Mac approval.
- Not yet run with the fresh agent: Test 5 re-run + Test 3, Test 2, Test 1 in direct chat, Test 1 in Slack `#support-triage` (once).
- No draft has ever been approved, so no `triage-log.md` exists yet — the demo's audit-log slot is empty until one is.
- Blog draft ready for editing: `blog-draft.md` (review copy, not published). Two bracketed `[PENDING]` notes mark exactly what must be updated from the Test 5 re-run and the Slack Test 1 result.
- Repo is public at https://github.com/brijesh-jakkuva/support-triage-room (17 files). Local HEAD `1e2b6e4` (Nov 6, 07:15 EST) — push any new local files (blog draft, this sheet, new test results) via the GitHub API helper; plain `git push` gets a 401 from this VM. Revoke the GitHub PAT after submission.

## Friday evening (tonight) — in this order

1. **Retry the severity-fix check** (needs a Mac approval — approve it when it appears; that approval timing out is what stalled this at 00:52). Read switch-buddy's reply on adding the Test 5 Critical sentence to the live agent.
2. **Re-run Test 5 + Test 3** in direct chat; score against `qa-checklist.md`. Then Test 2, then Test 1 in direct chat.
3. **Try Test 1 in Slack `#support-triage` once.** If it fails with "Not connected to a room" again, stop: the demo stays direct-chat and the blog documents the bug. Do not burn the evening on a second bind attempt.
4. **Approve one draft in-room/in-chat** so `triage-log.md` is created. This is required for the demo's 2:30–3:00 audit-log slot.
5. **Record the ~3-minute demo** per `demo-script.md`. If Slack failed at step 3, film in direct chat and label it honestly — never present direct-chat footage as Slack-room footage.
6. **Finish the blog**: replace the two `[PENDING]` notes in `blog-draft.md` with the actual results, then publish.

## Saturday morning — hard cutoffs

- **09:00 EST:** everything above is either done or cut. Whatever is not filmed by now is filmed from what exists (direct chat if needed).
- **10:00 EST:** blog final. If Test 5 re-run still says High, submit with the honest note in the blog that severity is the known miss — do not spend the morning on another instruction patch (patching a stuck agent made it worse once already).
- **11:00 EST:** video uploaded, repo pushed with final test results + blog link, README checked.
- **12:30 EST:** submit (repo + demo video + README + blog link). Confirm the submission went through — do not trust a single click without a confirmation.
- **1:29pm EST:** deadline. Do not plan any work after 12:30pm except confirming receipt.

## If something goes wrong Saturday

- Slack Test 1 fails again → direct-chat demo + honest blog note. The submission is still valid: triage logic passes, the bug is documented, not hidden.
- Test 5 still High → submit as-is with the severity miss named in the blog/test log. A documented miss beats a last-minute agent patch.
- Video upload stalls → submit the repo + README + blog first, then add the video link if the form allows editing; never miss the deadline waiting on an upload.
- Still-open loose end (not blocking submission): confirm the App Configuration Token pasted Nov 5, 01:11 EST was deleted on the Slack API apps page.
