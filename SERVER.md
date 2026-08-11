# Run your own Symphony server

Symphony is a private, end-to-end-encrypted space for your family — chat, feed, and calls where only your family can read anything. This bundle lets you run the whole thing on your own Windows PC. Messages relayed through your server are ciphertext: the server never sees what anyone writes, even though you own it.

**Your server, your rules — and your responsibility.** Running a server means you are the operator under the Symphony Terms: you choose who gets invited, and you are responsible for what your server is used for. Operators must be 18 or older.

## What you need

- Windows 10 or 11 (64-bit)
- Node.js 18 or newer — free from https://nodejs.org (pick the LTS version)
- About 15 MB of disk space, plus room for your family's messages

## Quickstart

1. Unzip this folder anywhere you like (for example `C:\Symphony`).
2. Right-click `start-symphony-server.ps1` and choose **Run with PowerShell**. (If Windows shows a safety prompt about a downloaded file, choose Open / Run anyway — or right-click the file, open Properties, and tick Unblock.)
3. The script starts two things: the **relay** (the message server, port 8991) and the **web app** (what browsers load, port 17800). It prints both addresses when everything is up.
4. Open `http://localhost:17800` in your browser — that's Symphony, served from your own PC.
5. To shut down, right-click `stop-symphony-server.ps1` and choose **Run with PowerShell**.

Want different ports? Run from a PowerShell window: `.\start-symphony-server.ps1 -RelayPort 9000 -WebPort 18000`

## How your family joins

Everything in Symphony starts with an **invite**. When you create an invite, the invite code itself carries your relay's address — so anyone who joins through your invite automatically talks to **your** server, not anyone else's. Share invites only with people you trust; an invite is the key to your family's space.

One honest caveat: your family's browsers and phones can only reach your server if it has a **public HTTPS address**. `localhost` only works on the PC running the server. Getting a public address is easier than it sounds — see the next section.

## Sharing your server with the world

Read **share-your-server.md**. It walks through three options, easiest first (the easiest one, Tailscale Funnel, takes about ten minutes and needs no router changes). HTTPS is not optional: the encryption and app features in the browser only switch on over a secure connection.

## Backups

Everything your server stores lives in the `data` folder next to the scripts:

- `data\symphony.db` — the relay's database (encrypted message envelopes in transit, member directory entries).
- `data\pepper.txt` — a random secret created on first run. The member directory is protected with it and it **cannot be recreated**. If you lose it, members may need to re-register.

Copy the whole `data` folder somewhere safe every so often (while the server is stopped is cleanest). That's the entire backup story — no databases to export, no accounts to migrate.

## Files in this bundle

- `symphony-relay.exe` — the relay (message server).
- `web\` — the Symphony web app and its tiny static file server.
- `start-symphony-server.ps1` / `stop-symphony-server.ps1` — start and stop everything.
- `share-your-server.md` — how to get your public HTTPS address.
- `data\` — created on first run; all your server's state lives here.

## Point the app at YOUR relay
Edit `web\config.js` and set your public relay address, for example: `window.SYMPHONY_RELAY='https://relay.your-domain.com';` — then every visitor of your web app (and every invite created there) uses YOUR server instead of the official one. Leave it as `''` to use the official relay.
