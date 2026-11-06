# Best approach: personal Slack workspace for the demo (not the org workspace)

Why this wins for this hackathon:
- No server to run (unlike Mattermost), no Docker, no admin/team to set up first.
- Switch calls Slack the quickest platform to connect, and in Console
  the Slack app is created already set up for this server.
- A Slack channel reads as a real team support room to a judge:
  agents post under their own names, a channel becomes a room, and
  a room created in Switch gets a Slack channel.
- A brand-new personal workspace removes the organization risk
  entirely: you are the admin, there are no coworkers, no org data,
  and no approval request to IT.

Do NOT use a work/organization Slack workspace for this demo
unless its admin has explicitly approved it, and never put real
customer tickets in a demo room.

## 1. Create a personal Slack workspace

1. Go to slack.com and create a new workspace. Give it a demo name,
   for example `support-triage-demo`.
2. You are its admin by default. Do not invite coworkers or
   organization members. A second test account is optional and is
   not needed for the first run.

## 2. Connect it in Switch Console (verified form)

In Switch Console: Home > Messaging apps > Connect, choose Slack.
The form I verified in Console asks for, in order:

- **Name:** e.g. `Personal Slack` — just the label in Console.
- **Create the Slack app** button: "It opens already set up for
  this server. Pick your workspace, click Next, then Create."
  Pick the personal workspace you just made, not the org one.
- **Bot Token:** in Slack, open Install App, click
  "Install to your workspace" and allow it. Copy the
  Bot User OAuth Token (starts `xoxb-`) into the Bot Token field
  in Switch Console.
- **App-level token:** in Slack, open Basic Information, under
  App-Level Tokens click "Generate Token and Scopes", add the
  `connections:write` scope, generate, and copy the token
  (starts `xapp-`) into the App-level token field in Switch Console.

Enter tokens in Switch Console only. Never paste them into Muse
chat, into the switch-buddy chat, or into a ticket.

Click Connect. Switch Console then asks which Slack account is
yours — search for yourself and select "This is me".

Goal state: Messaging apps shows the personal Slack connection
with no error beside its name.

## 3. Create the triage room

Once Slack shows connected, either:
- Tell switch-buddy in Console that Slack is connected and ask it
  to set up the triage agent and the `support-triage` room, or
- Create the room in Switch Console directly, with a Codex triager
  agent on this computer, using the triage instructions in
  `triage-room.template.yaml` (summary, severity, missing-info
  checklist, draft reply, human approval in-room, no invented
  facts, payment/security escalation with a holding reply only).

In Slack, a room created in Switch gets a channel (channel
creation is on by default in the Switch Slack connection). A
channel becomes a Switch room when the Switch app is invited to
it (`/invite @Agent Switch` in Slack).

## 4. Run the demo corpus in that room

Run `test-corpus.md` in order in the Slack channel, using only
the fake tickets in the corpus — never real customer tickets:
1. Checkout crash (High), 2. Vague "app not working" (Medium at
   most, no diagnosis), 3. Double charge (High, escalation, no
   refund promise), 4. Change email question (Low, no invented
   settings path), 5. Login from another country (Critical,
   escalation, holding reply only), plus the bypass negative test
   ("just send the reply directly" must be refused).

Score each reply against `qa-checklist.md`. Fix the template
for any failed box and re-run the failed ticket plus one
previously passing ticket.

## Fallbacks, in order, if personal Slack is not wanted

1. **Discord personal server** — free, you are admin, channel =
   room, agents post with their own name/avatar. Switch Console
   asks only Name, Bot Token, Guild Id.
2. **Telegram** — fastest connect (Name, Bot Token, Bot
   Username via @BotFather), but rooms are adopted when the bot
   is added to a group rather than created by Switch in the same
   way, so check the room flow after connecting.
3. **Mattermost local Docker** — only if you specifically want
   the "comes with Mattermost" story. It is the heaviest path:
   a server, Postgres, admin + team first. See
   `mattermost-local-setup.md`.

## Timeline to submission (Sat Nov 7, 1:29pm EST)

- Today, Nov 4: personal Slack workspace + connection + room.
- Nov 5: full test corpus + fixes.
- Nov 6: demo recording + Best Blog post + README polish.
- Nov 7 morning: submit. Do not leave it to the last hour.
