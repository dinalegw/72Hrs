# 72Hours ⏳

> **If you go missing, the truth goes public.**

72Hours is an open-source dead man's switch platform for journalists, activists, whistleblowers, and anyone whose safety depends on the world knowing what they know. Upload your evidence — video, audio, documents, photos — set your timer, enter your secret phrase regularly to reset it. If 72 hours pass without your check-in, everything publishes automatically.

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

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js 14 (App Router) + TypeScript |
| Styling | Tailwind CSS + shadcn/ui |
| Backend | Next.js API Routes + Node.js |
| Database | Supabase (Postgres + Auth + Realtime) |
| File Storage | Cloudinary (media) + Supabase Storage (docs) |
| Encryption | AES-256-GCM client-side encryption before upload |
| Scheduling | Supabase Edge Functions + cron jobs (timer logic) |
| Email/SMS | Resend (email) + Twilio (SMS check-ins) |
| AI Features | Anthropic Claude API (summaries, tagging, translation) |
| Deployment | Vercel (frontend) + Supabase (backend) |
| CDN | Cloudflare (DDoS protection + global distribution) |

---

## Project Structure

```
72hours/
├── app/                          # Next.js App Router
│   ├── (public)/                 # Public-facing pages
│   │   ├── page.tsx              # Landing page
│   │   ├── feed/                 # Public news feed
│   │   │   ├── page.tsx          # All cases
│   │   │   └── [caseId]/         # Individual case page
│   │   └── about/                # About + how it works
│   ├── (auth)/                   # Auth pages
│   │   ├── login/
│   │   └── signup/
│   └── (dashboard)/              # Authenticated user area
│       ├── vault/                # Upload and manage files
│       ├── timer/                # Set and manage countdown
│       ├── publish-settings/     # Configure publish targets
│       └── trusted-contacts/     # Backup keyholders
├── components/
│   ├── ui/                       # shadcn/ui base components
│   ├── vault/                    # File upload, encryption UI
│   ├── timer/                    # Countdown display, check-in
│   ├── feed/                     # News feed, case cards
│   └── shared/                   # Navbar, footer, layout
├── lib/
│   ├── crypto.ts                 # Client-side encryption utils
│   ├── supabase.ts               # DB client
│   ├── timer.ts                  # Timer logic
│   ├── publisher.ts              # Auto-publish engine
│   └── ai.ts                     # Claude API integration
├── supabase/
│   ├── migrations/               # DB schema
│   └── functions/                # Edge functions (timer cron)
├── public/
└── README.md
```

---

## Database Schema (Overview)

```sql
-- Users
users (id, email, secret_phrase_hash, created_at, plan)

-- Vaults (one per user, holds their case)
vaults (id, user_id, title, description, status, publish_at, timer_hours, last_checkin, created_at)

-- Files inside a vault
vault_files (id, vault_id, name, type, size, encrypted_url, thumbnail_url, transcript, created_at)

-- Published cases (public)
published_cases (id, vault_id, title, summary, tags, country, published_at, view_count)

-- Check-in log
checkins (id, vault_id, method, timestamp, ip_hash)

-- Trusted contacts
trusted_contacts (id, vault_id, name, email, phone, role)
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

## Getting Started (Development)

### Prerequisites
- Node.js 18+
- A Supabase project
- A Cloudinary account
- Anthropic API key (for AI features)

### Setup

```bash
# Clone the repo
git clone https://github.com/yourusername/72hours.git
cd 72hours

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
# Fill in your Supabase, Cloudinary, Anthropic, Resend, Twilio keys

# Run database migrations
npx supabase db push

# Start dev server
npm run dev
```

### Environment Variables

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

# Cloudinary
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=

# Anthropic (AI features)
ANTHROPIC_API_KEY=

# Resend (email)
RESEND_API_KEY=

# Twilio (SMS check-ins)
TWILIO_ACCOUNT_SID=
TWILIO_AUTH_TOKEN=
TWILIO_PHONE_NUMBER=

# App
NEXTAUTH_SECRET=
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

---

## Contributing

72Hours is built for human rights. Contributions are welcome — especially from:
- Security researchers (audit the crypto model)
- Journalists and activists (shape the features)
- Developers in high-risk countries (build the Tor integration)
- Translators (make the UI accessible globally)

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

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