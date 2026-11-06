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
| Public repository | **LIVE.** https://github.com/brijesh-jakkuva/support-triage-room — public, main branch. Test results through Nov 6, 00:52 EST and the Test 5 template fix are committed locally Nov 6, 07:15 EST and awaiting push (push via the GitHub API helper; plain `git push` gets a 401 from this VM). |
| Secrets check for pushing | **Clean, as far as a file search goes.** A search of the folder for token patterns found no usable credential values — only token prefixes (`xoxb-`, `xapp-`) in the setup guide and the truncated `xoxe.xoxp-…` reference in the run pack / project plan. Do a final `git status` / diff review before the first push anyway, and never add Console credential files. |
| Demo video (~3 min, `demo-script.md`) | Not recorded. Blocked on Tests 2–5 + bypass passing and on at least one approved draft, so `triage-log.md` exists to show in the 2:30–3:00 slot. No `triage-log.md` in the folder yet (expected — it is only created when a draft is approved). |
| README | **Fixed Nov 5, 22:36 EST** — Mattermost-first paragraph replaced with the personal-Slack wording; pushed to the public repo. |
| Blog post (Best Blog) | Outline only — corrected draft ready, original untouched. Writing is scheduled Fri Nov 6. Do not publish until the room-binding question resolves one way or the other (full Slack triage, or honest direct-chat demo + documented bug). |
| Tests 2–5 + bypass | **Mostly done with the fresh triager (Nov 6, 00:31–00:48 EST): Test 3 ✅, Test 4 ✅, bypass ✅, Test 5 ❌ severity only (High, should be Critical — template wording fixed, re-run pending). Test 2 not yet re-run with the fresh agent; Test 1 in Slack not yet tried with it.** |
| Fix-or-pivot decision | **Resolved.** Pivot to Console direct chat happened Nov 5, 23:10 EST; fresh triager recreated Nov 6, 00:26 EST passes Tests 3, 4 and bypass there. Slack Test 1 with the fresh agent is the one remaining try. |
| Severity wording | **Fixed and applied Nov 5, 22:36 EST** (Critical only for security/confirmed loss; apparent loss = High). Test 5 refinement added Nov 6, 00:47 EST ("unconfirmed never downgrades"); re-run pending. |
| Exposed App Configuration Token | Still unverified whether the `xoxe.xoxp-…` token pasted in chat Nov 5, 01:11 EST was deleted on the Slack API apps page. Mac offline, not re-checked. |
| Submission portal / form | **FOUND Nov 6, 07:12 EST.** https://www.wemakedevs.org/hackathons/switch/submit — resolved from the WeMakeDevs LinkedIn post's "Submit now" short link (lnkd.in/gPvrWnUZ). The page itself has not been opened successfully yet, so its fields are unverified — sign in with the WeMakeDevs account and check it before Saturday morning. |

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
