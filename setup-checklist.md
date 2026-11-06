# Switch Console setup checklist — Mac

Goal: get to the checkpoint "switch-buddy answers me in a chat
channel." The official quickstart says that takes about ten minutes
once the downloads are done; budget 30–45 minutes the first time for
Docker + Console downloads.

## Step 0 — What you need
- [ ] A Mac (Switch Console runs on macOS)
- [ ] Docker Desktop for Mac
- [ ] Switch Console, the desktop app
- [ ] One AI coding agent: Claude Code, Codex, or OpenCode — with
      its own subscription or API key. Switch ships no agents or
      models; you bring the one you already use.

You do NOT need a Slack workspace or admin access. Switch on your own
machine comes with Mattermost, a free chat app, for building and
demoing.

## Step 1 — Install and start Docker
1. Download Docker Desktop for Mac, choosing the Apple Silicon build
   for an M-series Mac or the Intel build for an older Mac
   (Apple menu > About This Mac shows which chip you have).
2. Drag Docker to Applications, open it, and wait until Docker is
   fully running (menu-bar icon settled, not still starting).
3. Checkpoint: Docker Desktop opens without an error, and stays running.

Why first: Switch Console runs the Switch server for you locally,
and that server runs on Docker. If Docker is not running, Console
cannot start the server — so start Docker before Console, every time.

Troubleshooting: if Console later says the server cannot start,
quit Console, make sure Docker is fully up, then reopen Console.

## Step 2 — Install Switch Console
Status on Nov 3, 2026: checked /Applications on your Mac — Switch
Console is NOT installed yet. Docker is installed and running.

1. Get Switch Console from the Switch repo's releases for macOS.
   Latest stable at check time: Switch Console 0.40.1.
   Repo releases: https://github.com/sandbox-quantum/switch/releases/latest
2. For your Mac (Apple Silicon, arm64): download
   `switch-console-arm64.dmg`. Intel Macs use
   `switch-console-x64.dmg`. Not sure? Apple menu → About This Mac.
   Both are signed and notarized, so they open without a Gatekeeper
   bypass, and both receive in-app updates.
3. Open the .dmg and drag Switch Console to Applications.
4. Open Switch Console from Applications.

Note on first run: Switch Console collects anonymous usage analytics
by default and tells you on first run; you can turn off "Share usage
data" on that notice, or later in Settings > General. It does not
collect source code, prompts, file paths, or credentials.

## Step 3 — Talk to switch-buddy
Status Nov 4, 00:31 EST: DONE with Codex — switch-buddy-admin is
Running on this computer, with a message input ready. It is not in
any room yet; Step 5 is next.

1. In Console, open switch-buddy — your own assistant in Switch.
2. Say what you want, in plain words, for example:
   > I want to build a support triage room in Mattermost. One agent
   > triages messy tickets and drafts replies, and I approve them
   > in the same room before anything is sent.
3. Let switch-buddy create your first agents and channels. It also
   helps you connect the chat app your team uses, and answers
   questions about Switch itself.

Checkpoint — you are set up when: an agent answers you in a chat
channel. That is the whole quickstart goal. Do not move on to the
triage template until this works; everything else builds on it.

## Step 4 — Connect your coding agent
1. Make sure Claude Code, Codex, or OpenCode is installed and signed
   in on your Mac. These work out of the box through Switch Console.
2. In Console, check that your agent is the one backing your room.
   The triage template defaults to the first installed of
   [claude, codex, opencode].
3. Checkpoint: tag the agent in your Mattermost channel and get a
   reply. If it does not reply, check (a) Docker is running,
   (b) the agent CLI is installed and logged in, and (c) you are
   in the channel Console created for you, not a different workspace.

Security note: sign in to your coding agent through its normal login
flow. Do not paste API keys or passwords into a chat room.

## Step 5 — Load the Support Triage Room (next, after Step 3 works)
1. Save `triage-room.template.yaml` from this folder onto your Mac.
2. In Switch Console, create a room from that template. If Console
   asks for a team name, use a short lowercase prefix
   (letters, digits, hyphens only, e.g. `support`).
3. Paste Test 1 from `test-corpus.md` into the room.
4. Score the reply against `qa-checklist.md`, approve or edit the
   draft in the room, and confirm nothing was claimed as sent.

If the template import wording in Console differs from the above,
ask switch-buddy in Console: "Create a room from this template file"
and share the file with it — switch-buddy is the supported way to
drive Console setup, rather than guessing at buttons.
