# 72Hours ⏳

> **If you go missing, the truth goes public.**

72Hours is a dead man's switch platform for journalists, activists, whistleblowers, and anyone whose safety depends on the world knowing what they know. Upload your evidence — video, audio, documents, photos — set your timer, enter your secret phrase regularly to reset it. If 72 hours pass without your check-in, everything publishes automatically.

---

## The Problem

People who expose corruption, document crimes, or speak truth to power are silenced every day. Evidence dies with them — deleted, confiscated, buried. There is no system that lets an ordinary person say: *"If something happens to me, the world will know."*

72Hours is that system.

---

## How It Works

```
User records evidence  →  Uploads to 72Hours vault  →  Sets timer (default: 72hrs)
        ↓
Every X hours, user enters their secret phrase to reset the clock
        ↓
If the clock hits zero (user is missing, detained, or unable to check in)
        ↓
Content auto-publishes to: 72Hours public feed + connected news outlets + social APIs
```

### The Secret Phrase
- Only the user knows their secret phrase
- Entering it resets the timer (can extend by 24hr increments)
- Wrong phrases or no check-in = timer continues counting down
- Even 72Hours staff cannot reset or cancel a publish without the phrase
- Optional: designate a trusted second person as backup keyholder

---

## Core Features

### 🔒 Vault
- End-to-end encrypted file storage
- Supports video, audio, documents, images, PDFs
- Files are encrypted at rest with user's key derived from secret phrase
- Files stored across distributed locations (no single point of deletion)

### ⏱️ Dead Man's Switch
- Configurable countdown timer (default 72 hours, max 30 days)
- Check-in via web, mobile app, SMS, or email
- Multiple check-in methods so one failure doesn't trigger false publish
- Grace period warnings sent at: 24hrs, 12hrs, 6hrs, 1hr before zero
- Emergency override: trusted contact system

### 📢 Auto-Publish Engine
- Publishes to the 72Hours public news feed
- Webhooks to connected platforms (Telegram channels, Signal groups, email lists)
- Optional: publish to connected journalist networks
- Optional: notify specific people (lawyers, family, NGOs) on trigger
- Content goes live simultaneously across all channels — hard to suppress

### 📰 Public News Feed
- Live blog/news site showing all published cases
- AI-assisted tagging, categorization, and translation
- Search by country, case type, date, person
- Community verification system (flag, corroborate, add context)
- Cases stay published permanently — immutable once live

### 🤖 AI Integration
- Auto-transcribe audio and video on upload
- Auto-generate case summaries for the news feed
- Detect faces/locations (for user's choice to blur or highlight)
- Translate content to multiple languages on publish
- AI moderation to filter out spam/abuse of the system

---

## Use Cases

| Scenario | How 72Hours Helps |
|---|---|
| Journalist in a dangerous country | Upload investigation, check in daily — if arrested, it publishes |
| Kidnapping victim (pre-recorded) | Records proof of kidnapping — kidnappers know release = no publish |
| Whistleblower | Uploads corporate/government evidence before coming forward |
| Activist in authoritarian state | Creates leverage: "If I disappear, people will know why" |
| Witness to a crime | Deposits evidence safely before going to authorities |
| Anyone threatened into silence | "I've already uploaded it. You can't stop it now." |

---

## Project Structure

```
72Hrs/
├── index.html          # Landing page (HTML + CSS + JS)
├── README.md           # Project documentation
└── LICENSE             # MIT License
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Static HTML5 + Vanilla JavaScript |
| Styling | Custom CSS (CSS Variables, Grid, Flexbox) |
| Icons | Inline SVG |
| Fonts | Google Fonts (Bebas Neue, DM Serif Display, DM Mono, Outfit) |
| Hosting | Any static host (Netlify, Vercel, Cloudflare Pages, GitHub Pages) |

---

## Getting Started

### View Locally

```bash
# Open directly in browser
open index.html
```

Or serve with any static server:

```bash
# Python
python3 -m http.server 3000

# Node.js
npx serve .
```

---

## Security Model

72Hours is designed so that **even we cannot suppress a publish.**

- Secret phrases are **never stored** — only a salted hash
- Files are encrypted **before** leaving the user's device
- The publish trigger is a **scheduled job** that runs autonomously — it doesn't wait for a human to approve
- Even if our servers are seized, files stored on distributed CDN nodes publish on schedule
- All publish targets (Telegram, email lists, webhooks) are set up by the user and stored encrypted
- Open source: anyone can audit that we haven't built a backdoor

---

## Roadmap

### Phase 1 — MVP (Months 1–2)
- [ ] User auth (email + passphrase)
- [ ] Basic vault (upload files, set timer)
- [ ] Secret phrase check-in (web only)
- [ ] Timer countdown + warning emails
- [ ] Auto-publish to 72Hours public feed on trigger
- [ ] Public feed (read-only, paginated)
- [ ] Landing page

### Phase 2 — Core Platform (Months 3–4)
- [ ] SMS check-in via Twilio
- [ ] Trusted contacts system
- [ ] AI transcription on video/audio upload
- [ ] AI case summary generation for feed
- [ ] Case tagging and search
- [ ] Mobile-responsive PWA

### Phase 3 — Network & Distribution (Months 5–6)
- [ ] Webhook publish targets (Telegram, Discord, Slack)
- [ ] Email list publish on trigger
- [ ] Journalist network integration
- [ ] Multi-language AI translation on publish
- [ ] Case verification / community corroboration
- [ ] Tor hidden service (.onion) for high-risk users

### Phase 4 — Scale & Resilience (Months 7–9)
- [ ] Decentralized file storage (IPFS/Arweave as backup layer)
- [ ] Mobile apps (iOS + Android)
- [ ] API for NGOs and media outlets to pull published cases
- [ ] Organizational accounts (for newsrooms, NGOs)
- [ ] Multi-party secret (Shamir's Secret Sharing for group vaults)
- [ ] Offline check-in (dead-drop mechanism)

---

## Contributing

72Hours is built for human rights. Contributions are welcome — especially from:
- Security researchers (audit the crypto model)
- Journalists and activists (shape the features)
- Developers in high-risk countries (build the Tor integration)
- Translators (make the UI accessible globally)

---

## Legal

72Hours does not moderate content before it publishes. We are a platform, not a publisher. Published content is the sole responsibility of the user who uploaded it. We comply with lawful legal process but our architecture is designed so that by the time a court order arrives, suppression is technically impossible.

Users are responsible for ensuring their uploads do not violate laws in their jurisdiction.

---

## License

MIT License — free to use, fork, self-host, and build on.

---

## Why This Exists

> *"The most dangerous moment is right before you speak. After you speak, you're already free."*

72Hours gives people that moment of leverage — the ability to say to anyone threatening them: *"It's already uploaded. The only thing you can do now is let me live long enough to reset the clock."*

---

**Built with urgency. For the ones who need it most.**

⏳ [72hours.io](https://72hours.io) · [Twitter](#) · [Discord](#) · [Donate](#)
