# Local Mattermost server with Docker (Mac, hackathon demo only)

Goal: a Mattermost server on this Mac that Switch Console can connect to,
so the support-triage room can be created. This is a local demo setup,
not production: Mattermost's own Docker docs say Docker on macOS is
supported for testing/development only.

## Simpler alternative: Mattermost Preview (one command)

The full Compose setup below is the durable version, with separate
Postgres and persistent data. The simplest Mattermost version is the
official Preview image — one self-contained container, internal
database, works out of the box:

```sh
docker run --name mattermost-preview -d --publish 8065:8065 mattermost/mattermost-preview
```

Then open http://localhost:8065 and create an account, then a team,
exactly as in steps 5–6 below.

Trade-offs, from Mattermost's own Preview docs: Preview is not for
production — it uses non-production settings, email is disabled,
there is no persistent data (dropping the container removes data
and configuration), and it does not support upgrades. For a
three-day hackathon demo that is usually fine; for anything you
want to keep, use the full Compose setup below instead.

Even simpler than any Mattermost setup, if you already use one of
them, is Telegram or Discord: no server to run at all. Telegram is
a BotFather bot + token in Switch Console; Discord is a bot
application + bot token + server (Guild) ID in Switch Console.
Both connect outbound, so no public URL is needed. The catch to
check before switching: Telegram rooms in Switch are adopted when
the bot is added to a group, not created by Switch in the same way,
so the triage-room flow needs checking there.

Muse cannot run Terminal on this Mac, so these steps are run by you
in Terminal. Do not paste any password into Muse chat or into the
switch-buddy chat — enter passwords only in the Mattermost web UI
and in the Switch Console connection form itself.

## 1. Check Docker is running

Open Terminal on the Mac and run:

```sh
docker --version
docker compose version
```

Docker Desktop must be running. If either command says Docker is not
running, start Docker Desktop first and wait for it to finish starting.

## 2. Get the official Mattermost Docker setup

```sh
git clone https://github.com/mattermost/docker ~/mattermost-docker
cd ~/mattermost-docker
cp env.example .env
```

Source: the official Mattermost Docker deployment guide
(https://docs.mattermost.com/deployment-guide/server/deploy-containers)
and the official repo https://github.com/mattermost/docker

## 3. Edit .env for a local http:// setup

Open `.env` in a text editor and change these lines (leave the rest
alone for now):

```sh
DOMAIN=localhost
MATTERMOST_IMAGE=mattermost-team-edition
MM_SERVICESETTINGS_SITEURL=http://localhost:8065
```

Why these three:
- `DOMAIN` must not stay as `mm.example.com`.
- Team Edition is the free edition, and is what this demo needs.
  The example file defaults to Enterprise Edition.
- The example sets SiteURL to `https://` + DOMAIN. For a local demo
  with no certificate, that would point Mattermost at https://localhost
  and break the login page and the Switch connection. Setting it to
  `http://localhost:8065` keeps the URL, the browser address, and the
  Switch connection all on the same http address.

Also change `POSTGRES_PASSWORD` in `.env` to a password you choose
for the database only. You will not need it again for Switch — do not
share it in chat.

## 4. Start Mattermost (without NGINX)

No NGINX container is needed for a local demo — Mattermost itself
listens on port 8065:

```sh
docker compose -f docker-compose.yml -f docker-compose.without-nginx.yml up -d
```

First start downloads the images and runs database setup, so give it
a few minutes. Check progress with:

```sh
docker compose -f docker-compose.yml -f docker-compose.without-nginx.yml ps
docker compose -f docker-compose.yml -f docker-compose.without-nginx.yml logs -f mattermost
```

Stop the log view with Ctrl-C (that stops the log view, not Mattermost).

### Apple Silicon note

The Mattermost images are built for amd64. On an Apple Silicon Mac,
Docker Desktop normally runs them under emulation. If the pull fails
with a "no matching manifest for linux/arm64" error, that is the
cause — stop and tell Muse the exact error before trying a different
image, rather than switching images at random.

## 5. Create the admin account and a team in Mattermost

1. Open http://localhost:8065 in a browser.
2. Create the first user account. The first user created on a fresh
   Mattermost server becomes the system admin — this is the admin
   account Switch needs. Use an email, username, and password you
   choose for this demo only.
3. Create a team. Note the team name exactly as it appears in the
   URL after you create it — that slug is the "Team Name" Switch asks
   for. Use the team URL Mattermost actually shows you, not a guessed
   one.

You have now got everything Switch Console's Mattermost form asks for.

## 6. Connect it in Switch Console

Back in Switch Console, the Mattermost form you left open (Home >
Messaging apps > Connect > Mattermost) asks for:

- **Name:** something like `Local Mattermost` — this is just the label
  in Switch Console when you pick it for a room.
- **Url:** `http://localhost:8065`
- **Admin User:** the admin username you created in step 5.
- **Admin Password:** the admin password you created in step 5.
  Enter it in Switch Console only, never in a chat.
- **Team Name:** the team slug from step 5.
- **Public Url:** leave blank for a local demo (it is optional, and
  is only needed when the address people use differs from the Url).
- **Default Member:** leave blank unless you want a specific person
  added to every channel this connection creates.
- **Callback Base Url:** leave as Switch suggests unless the form
  requires a value — tell Muse what it shows if it blocks you.

Click Connect. The goal state is: Messaging apps in Switch Console
shows the Mattermost connection as connected.

## 7. Then tell switch-buddy

Once Switch Console shows Mattermost connected, go back to the
switch-buddy chat in Console and tell it Mattermost is connected,
so it can set up the triage agent and the `support-triage` room,
as it said it would.

## Stop / restart

```sh
# Stop Mattermost (keeps its data volumes)
docker compose -f docker-compose.yml -f docker-compose.without-nginx.yml down

# Start it again later
docker compose -f docker-compose.yml -f docker-compose.without-nginx.yml up -d
```

## Checkpoint for Muse

Tell Muse when you reach one of these:
- "Mattermost is up at localhost:8065, admin and team created" — then
  we do step 6 together.
- "Mattermost shows connected in Switch Console" — then we tell
  switch-buddy and verify the support-triage room.
- Any error, pasted exactly as Terminal / the browser shows it.
