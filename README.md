# 🎼 Symphony

**A private space for the people who matter — feed, chat, stories, polls, events and video calls — with no account, no phone number, and no company in the middle.**

Symphony is your family's own little world. Open it, type your name, and you're in. Everything you share is end-to-end encrypted, so only your family can see it. No ads. No tracking. Free.

---

## ⬇️ Download

| Your device | Get Symphony |
|---|---|
| 🪟 **Windows** | **[Download Symphony for Windows](https://github.com/Amnibro/Symphony/releases/latest/download/Symphony-Setup.exe)** — a tiny (~1 MB) app that opens Symphony in its own window. Prefer no install? Grab the portable `Symphony.exe` from the [releases page](https://github.com/Amnibro/Symphony/releases/latest). |
| 🤖 **Android** | **[Download the Android app](https://amni-scient.com/symphony/symphony.apk)** — works on Android 8.0 and newer. After the first install, the app keeps itself up to date. |
| 🍎 **iPhone, iPad, or any computer** | Just visit **[symphony.amni-scient.com](https://symphony.amni-scient.com)**. On iPhone or iPad, tap **Share → Add to Home Screen** and Symphony becomes a full-screen app. No App Store needed. |

> **Windows heads-up:** the first time you run the installer, Windows may show a blue "Windows protected your PC" screen. That's normal for a small independent app that isn't signed by a big company — nothing is wrong. Click **More info**, then **Run anyway**. The [Quickstart](QUICKSTART.md#windows) walks you through it with pictures-in-words.

---

## 💙 Why Symphony

- **Private by design.** Every message, photo and call is end-to-end encrypted. Not even the server that carries your messages can read them.
- **No account. No phone number.** You type your name — that's the whole sign-up. Your identity is created on your own device and never leaves it.
- **Your family's feed, without an algorithm.** Posts appear because your people shared them, in order — not because a computer decided to show them to you. No ads, no strangers, no ranking games.
- **Free.** For everyone, on every device.

---

## ⏱️ Up and running in 60 seconds

1. Open Symphony and type your name.
2. Tap **🏠 Start a family** and give it a name (like "The Smiths").
3. Share the invite link — by text, email, or by showing the QR code.

Everyone who taps that link lands in your family. That's it — start posting, chatting, and calling.

- 📄 **[Quickstart](QUICKSTART.md)** — install steps for every device, plus the 60-second start-or-join paths.
- 📖 **[Full tutorial](TUTORIAL.md)** — everything Symphony does, explained simply.

---

## 🔒 Privacy, in plain words

When you send a message in Symphony, it's locked into a sealed envelope **on your device**, and only your family members hold the keys to open it. The relay server that passes messages along is like a mail carrier who can see there's an envelope — but can never see inside. There are no accounts to hack, no phone numbers to leak, and no company reading your conversations to sell you things.

**For the technically curious:** each device generates its own Ed25519 + X25519 identity locally — no signup, no server-side account. Messages are sealed with X25519 key agreement → HKDF-SHA256 → ChaCha20-Poly1305. The relay only ever sees ciphertext.

---

Made with care by **[Amni-Scient](https://amni-scient.com/symphony)** · If Symphony makes your family closer, you can [☕ support development on Ko-fi](https://ko-fi.com/amnibro)
