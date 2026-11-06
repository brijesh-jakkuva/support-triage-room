# Severity wording fix — DRAFT, not yet applied (Thu Nov 5, 2026, ~15:30 EST)

Prepared offline from the local files only. The MacBook Air has been
offline since 01:37 EST Nov 5, so nothing was re-verified live.
Nothing in `triage-room.template.yaml`, `qa-checklist.md`, or
`test-corpus.md` was changed — this file only holds the exact
replacements, ready for one approval.

## The conflict (verified in the files)

- `triage-room.template.yaml` guardrails: "Security, unauthorised
  access, or data-loss tickets: severity Critical, escalate to the
  human immediately, holding reply only, never reassure the user
  that no data was taken."
- `qa-checklist.md` escalation: "Security / unauthorised access /
  data loss: Critical, escalate now, holding reply, no reassurance
  that data is safe."
- `test-corpus.md` Test 1 (checkout crash, "lost my cart??"):
  "Severity = High (core flow broken, time-sensitive, no proven
  outage)."
- `test-corpus.md` Test 5 (unknown login from another country):
  "Severity = Critical. Escalate immediately."

A triager following the template literally would score Test 1
Critical (cart appears lost = data loss), while the corpus — and the
two Nov 5 Slack scores, and the Nov 4 direct-chat pass — score it
High. A judge re-running the corpus against the template would hit
the same contradiction. It needs one rule, in all three files.

## Recommended fix: split "apparent" from "confirmed" data loss

Keep Test 1 at High and Test 5 at Critical. The distinction is
evidence, not sympathy: a cart that *appears* lost after a crash,
with no unauthorised access reported, is High; a security incident
or confirmed/proven loss is Critical. This matches the Nov 4
direct-chat Test 1 reply, which said High with "possible cart data
loss" as the reason.

### 1. `triage-room.template.yaml` — replace the data-loss guardrail

Old:
> - Security, unauthorised access, or data-loss tickets:
>   severity Critical, escalate to the human immediately, holding
>   reply only, never reassure the user that no data was taken.

New:
> - Security or unauthorised-access tickets, or tickets reporting
>   confirmed data loss or a breach: severity Critical, escalate
>   to the human immediately, holding reply only, never reassure
>   the user that no data was taken.
> - Reported or apparent data loss with no security incident (for
>   example, a cart that appears lost after a crash): severity
>   High, escalate holding-only, never claim the data is
>   recoverable or safe.

### 2. `qa-checklist.md` — replace the escalation bullet

Old:
> - [ ] Security / unauthorised access / data loss: Critical, escalate now,
>       holding reply, no reassurance that data is safe

New:
> - [ ] Security / unauthorised access / confirmed data loss: Critical, escalate now,
>       holding reply, no reassurance that data is safe
> - [ ] Reported or apparent data loss, no security incident: High, escalate
>       holding-only, no claim the data is recoverable or safe

### 3. `test-corpus.md` — one clarifying line on Test 1

Add to Test 1's Expected, after "Severity = High (core flow broken,
time-sensitive, no proven outage).":
> High, not Critical: the cart appears lost but no unauthorised
> access or confirmed breach is reported — see the template rule
> above. Test 5 stays Critical.

## Alternative (not recommended)

Score Test 1 as Critical and change only the corpus. Trade-off: it
would make the Nov 4 direct-chat Test 1 pass wrong (it scored High),
collapse the distinction between "cart may be lost" and "someone
else is in my account", and leave Test 3 (double charge, High) and
Test 1 both escalated identically with no severity signal between a
payment error and a possible data-loss event.

## After approval

1. Apply the three replacements above (template first — a recreated
   triager is built from it).
2. Re-run Test 1 and score it against the new wording; a High with
   "apparent loss, no security incident" as the reason is then a pass.
3. If the triager is recreated from the template, do this fix before
   that recreation, not after — otherwise the new triager inherits
   the old contradiction.
