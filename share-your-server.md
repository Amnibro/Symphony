# Give your Symphony server a public address

Your server runs on `localhost`, which only works on the PC it runs on. For family on other devices you need a **public HTTPS address**. HTTPS is required, not a nicety: browsers only enable the service worker and the WebCrypto encryption APIs on a secure connection, so a plain `http://` address will simply not work outside your own PC.

You need public addresses for **both** halves:

- the **web app** (port 17800) — what everyone's browser loads
- the **relay** (port 8991) — what the app talks to for messages

(A future update will let the relay share the web app's address — "same-origin mode". Until then, plan on two hostnames.)

Three ways to do it, easiest first.

## A. Easiest: Tailscale Funnel (free, ~10 minutes, no router changes)

Tailscale gives your PC a stable public HTTPS address that works even behind carrier-grade NAT, with zero router configuration.

1. Install Tailscale from https://tailscale.com/download and sign in (free personal account).
2. Enable HTTPS certificates and Funnel for your tailnet when prompted (the commands below will link you to the right admin page the first time).
3. In a PowerShell window, expose the web app:

   ```
   tailscale funnel --bg 17800
   ```

   That prints your stable public address, something like `https://your-pc.your-tailnet.ts.net`.
4. The relay needs exposing too. Funnel can serve a second port on the same hostname under different ports (443/8443/10000), for example:

   ```
   tailscale funnel --bg --https 8443 8991
   ```

   Your relay is then `https://your-pc.your-tailnet.ts.net:8443`.

No port forwarding, no domain to buy, survives reboots (`--bg` persists). The address only changes if you rename the machine or tailnet.

## B. Own domain: Cloudflare Tunnel (free, needs a domain you control)

If you own a domain (say `example.com`), `cloudflared` gives you clean hostnames with automatic HTTPS.

1. Add your domain to a free Cloudflare account (they walk you through pointing your domain at their nameservers).
2. Install cloudflared: https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/
3. Log in and create a tunnel:

   ```
   cloudflared tunnel login
   cloudflared tunnel create symphony
   ```

4. Create `config.yml` (cloudflared tells you where it lives, typically `C:\Users\you\.cloudflared\`):

   ```yaml
   tunnel: symphony
   credentials-file: C:\Users\you\.cloudflared\<tunnel-id>.json
   ingress:
     - hostname: symphony.example.com
       service: http://localhost:17800
     - hostname: chat.example.com
       service: http://localhost:8991
     - service: http_status:404
   ```

5. Point DNS at the tunnel (once per hostname), then run it:

   ```
   cloudflared tunnel route dns symphony symphony.example.com
   cloudflared tunnel route dns symphony chat.example.com
   cloudflared tunnel run symphony
   ```

`https://symphony.example.com` is your web app, `https://chat.example.com` is your relay. Install cloudflared as a Windows service (`cloudflared service install`) so it starts with the PC.

## C. Classic: port forwarding + reverse proxy + certificates

The traditional route — most control, most steps, and it does not work behind carrier-grade NAT (if your ISP does not give you a real public IP, use option A or B).

1. Get a domain name and point two hostnames (e.g. `symphony.example.com`, `chat.example.com`) at your home IP (a dynamic DNS updater helps if your IP changes).
2. Forward port 443 on your router to the PC running Symphony.
3. Run a reverse proxy on the PC that terminates HTTPS and routes by hostname — Caddy is the least painful on Windows (https://caddyserver.com), because it fetches and renews Let's Encrypt certificates automatically. A complete `Caddyfile`:

   ```
   symphony.example.com {
     reverse_proxy localhost:17800
   }
   chat.example.com {
     reverse_proxy localhost:8991
   }
   ```

4. Prefer nginx? Same idea, but you manage certificates yourself with certbot (https://certbot.eff.org) and renew them every 90 days.

## After any of the three

- Open your public web address in a browser on a phone (not on the server PC) and check it loads.
- Check `https://<your relay address>/health` in a browser — it should say `ok`.
- Create invites once you're connected through the public address, so the invite carries the public relay address (not `localhost`) and everyone who joins lands on your server.
