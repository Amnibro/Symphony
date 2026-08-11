# Symphony Privacy Policy

**Effective: August 11, 2026**

Symphony is built so that we know as little about you as technically possible. This page explains exactly what that means.

## What we never have

- **No account.** No email, no phone number, no username registered with us, no password.
- **No content.** Messages, photos, voice notes, files, and calls in your families are end-to-end encrypted on your device (Ed25519 + X25519 identity; X25519 → HKDF-SHA256 → ChaCha20-Poly1305). The relay stores sealed envelopes it cannot open. We cannot read your content, and neither can anyone who compromises the relay.
- **No ads, no trackers, no analytics.** The apps contain no advertising SDKs, no tracking pixels, and phone home for nothing except the messages you send and an app-update version check.

## What the relay does hold

- **Device keys**: your public keys (never private keys — those exist only on your devices) and, if you enable notifications, a push token.
- **Encrypted envelopes**: sealed messages waiting for delivery. They are deleted when your device collects them.
- **Encrypted media and backups**: encrypted blobs with a limited retention period. Encryption keys travel inside your sealed messages — we never have them.
- **Delivery metadata**: the relay necessarily sees which public key sent an envelope to which public key, and when. It does not see names, content, or family structure (those live inside the encryption).

## The public Community

The Community tab is a **public space** built on public relays. Treat posts there like posts on a public forum — they are not private, and deletion cannot be guaranteed once distributed.

## Your identity

Your identity is a keypair generated on your device. We can't reset it, recover it, or link it to you. If you use the optional recovery code or password lock, those protections are applied on your device.

## Self-hosted instances

If your family uses a self-hosted Symphony server, that operator — not us — holds the items described above for your family. Ask them about their practices.

## Adults only

The Service is intended for users 18 and older. We do not knowingly provide the Service to anyone under 18, and we do not knowingly collect information from minors — by design, we collect almost nothing from anyone.

## Changes

Updates to this policy appear on this page with a new effective date.

Questions? Open an issue on [GitHub](https://github.com/Amnibro/Symphony/issues).
