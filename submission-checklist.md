# Submission checklist — Sat Nov 7, 1:29pm EST (Thu Nov 5, ~15:30 EST)

Prepared Thu Nov 5, ~15:30 EST, from the local files plus a fresh
check of the official hackathon pages (DevTools Academy page read
2026-11-05 20:25 UTC; WeMakeDevs page read 20:26 UTC). The MacBook
Air has been offline since 01:37 EST Nov 5, so nothing about Switch
Console, Slack, or the triager was re-verified live. Nothing was
changed on the Mac.

Deadline: Sat Nov 7, 11:59pm IST = **1:29pm EST**. About 46 hours
from this check. Do not leave submission to the last hour — video
upload and forms are the usual bottleneck (project plan).

## What the organisers actually require

DevTools Academy, "What you submit":
- A **public project repository**
- A short demo video of your workflow running
- A README that explains how you used Switch: which agents you
  connected, how the channel is set up, and how to run it
- Optional: a blog post about the build, which also enters Best Blog

Source: https://www.devtoolsacademy.com/hackathons/flip-the-switch
("What you submit", read 2026-11-05 20:25 UTC)

## Status

| Item | Status |
|---|---|
| Public repository | **NOT CREATED.** `~/workspace/support-triage-room/` is not a git repository (checked 20:26 UTC Nov 5: `git status` → "not a git repository"). No GitHub repo for this project is mentioned anywhere in the local files or memory. The project plan says "submit the folder" — the official requirement is a public repo, so a repo still has to be created and the folder pushed to it. |
| Secrets check for pushing | **Clean, as far as a file search goes.** A search of the folder for token patterns found no usable credential values — only token prefixes (`xoxb-`, `xapp-`) in the setup guide and the truncated `xoxe.xoxp-…` reference in the run pack / project plan. Do a final `git status` / diff review before the first push anyway, and never add Console credential files. |
| Demo video (~3 min, `demo-script.md`) | Not recorded. Blocked on Tests 2–5 + bypass passing and on at least one approved draft, so `triage-log.md` exists to show in the 2:30–3:00 slot. No `triage-log.md` in the folder yet (expected — it is only created when a draft is approved). |
| README | Still has the old Mattermost-first setup paragraph. Fix is drafted in `blog-outline-corrected-draft.md` appendix, awaiting approval (already surfaced to the user Nov 5, 12:13 EST; no reply yet). |
| Blog post (Best Blog) | Outline only — corrected draft ready, original untouched. Writing is scheduled Fri Nov 6. Do not publish until the room-binding question resolves one way or the other (full Slack triage, or honest direct-chat demo + documented bug). |
| Tests 2–5 + bypass | Not run anywhere yet. Run pack (`today-run-pack.md`) is ready; already queued for delivery. |
| Fix-or-pivot decision | Still open since 02:08 EST Nov 5: one restart/recreate attempt for support-triager, then pivot to Console direct chat. |
| Severity wording | Contradiction found (template/QA say data loss = Critical; corpus Test 1 expects High). Exact fix drafted in `severity-fix-draft.md`, awaiting approval — apply before recreating the triager. |
| Exposed App Configuration Token | Still unverified whether the `xoxe.xoxp-…` token pasted in chat Nov 5, 01:11 EST was deleted on the Slack API apps page. Mac offline, not re-checked. |
| Submission portal / form | **Not confirmed.** The WeMakeDevs hackathon page's Registration section did not load in the text fetch (read 20:26 UTC: "Loading… One moment. Pulling up this hackathon."). Do not assume a URL. Confirm where to submit from the registration confirmation / WeMakeDevs dashboard before Sat morning. |

## Suggested order (does not need the triager fixed first)

1. **Today / tonight:** create the public GitHub repo and push the
   current folder (it is safe to push as-is on secrets; it can be
   updated after the tests pass). This removes the one submission
   item that needs an account login and cannot be done in the last
   hour.
2. **Today:** approve the severity fix + the README/blog-outline
   replacements, so a recreated triager uses the corrected template.
3. **Fri Nov 6:** write the blog from the corrected draft; record
   the demo once Tests 2–5 + bypass pass.
4. **Sat Nov 7, morning:** submit repo + video + README (+ blog
   link) well before 1:29pm EST, and confirm the submission went
   through — do not trust a single click without a confirmation.
