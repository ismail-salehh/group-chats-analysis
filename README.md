# Group Chat Analyzer

Turn your exported Facebook Messenger and Instagram Direct group-chat archives into rich, interactive historical reports entirely inside your web browser. Built on a local-first, zero-knowledge architecture, Group Chat Analyzer decompresses, normalizes, and analyzes long-running personal conversations locally without transmitting a single byte of chat data to any external server or AI service.

```text
┌────────────────────────────────────────────────────────────────────────┐
│  WEEKEND CREW                                                          │
│  18,421 messages · 7 participants · 2021 → 2026                        │
├──────────────┬──────────────┬─────────────┬─────────────┬──────────────┤
│  Top Voice   │  Peak Hour   │  Peak Day   │ Top Emoji   │ Biggest Mnth │
│  Ahmed (31%) │  22:00–23:00 │  Friday     │ 😂 (1,420x) │ May 2024     │
├──────────────┴──────────────┴─────────────┴─────────────┴──────────────┤
│                                                                        │
│                       MESSAGE TIMELINE OVER TIME                       │
│     ██                                              ████               │
│     ██   ██                                    ██   ████   ██          │
│     ██   ██   ██                          ██   ██   ████   ██   ██     │
│   ─────────────────────────────────────────────────────────────────    │
│   2021       2022          2023          2024          2025    2026    │
│                                                                        │
├─────────────────────────────────────┬──────────────────────────────────┤
│         ACTIVITY HEATMAP (7×24)     │      INTERACTION NETWORK         │
│   Mon [  ][  ][░░][▒▒][██][░░]      │            Ahmed                 │
│   Tue [  ][  ][░░][██][██][▒▒]      │           /  |  \                │
│   Wed [  ][  ][▒▒][██][▓▓][░░]      │       Sara - Bob - Elena         │
│   Thu [  ][░░][▒▒][██][██][▒▒]      │           \  |  /                │
│   Fri [  ][░░][██][██][██][██]      │            Tariq                 │
│   Sat [  ][  ][░░][██][▓▓][▒▒]      │                                  │
│   Sun [  ][  ][  ][▒▒][██][░░]      │  (Transition flows < 15 mins)    │
├─────────────────────────────────────┴──────────────────────────────────┤
│  RECURRING PHRASES ("Inside Joke" Candidates)                          │
│  • "coffee emergency" (83x · 5 members)  • "classic move" (62x · 4 mem)│
└────────────────────────────────────────────────────────────────────────┘
```

---

## What It Does

Your group chats hold the history of your friendships, family milestones, study groups, and inside jokes. Group Chat Analyzer surfaces the hidden patterns in those raw archives:

- **Group DNA Cards**: Instant high-level summary cards (top speaker share, peak activity hours, busiest day of the week, longest conversation burst, top emoji, and longest group silence).
- **Activity Timeline & 7×24 Heatmap**: Hour-of-day by day-of-week heatmaps rendered in your local timezone, alongside monthly and daily message timelines.
- **Participant Breakdown & Script Classification**: Message share, word share, median message length, active days cadence, attachment ratios, and Unicode script classification (Arabic script vs. Latin alphabet vs. Digits vs. Emojis).
- **Conversation Bursts & Starters**: Automatic segmentation of conversation sessions based on configurable inactivity gaps (default: 60 minutes), measuring who tends to initiate chat bursts.
- **Interaction Network**: Interactive circular SVG transition graphs and matrix tables displaying speaker-to-speaker turn flows within 15 minutes.
- **Multilingual Lexicon & Recurring Phrases**: Content word frequencies (filtering curated English and Arabic stopwords), bigrams, trigrams, and candidate recurring phrases ("inside joke" candidate detector).
- **Searchable Transcript Explorer**: Fast in-memory keyword search with participant filtering, attachment filtering, and HTML-escaped rendering to prevent XSS.
- **Exportable Reports & Share Cards**: Downloadable Group Summary cards, CSV participant statistics, and complete JSON analytical payloads.

---

## Why It Exists

Most modern communication tools either lock your history behind proprietary interfaces or offer crude search utilities. Worse, many modern analytics tools require uploading your private archives to third-party cloud servers or proprietary LLM APIs.

Group chats contain private, intimate thoughts belonging to **other people**—friends, family, and colleagues who never agreed to have their data ingested into a cloud database.

Group Chat Analyzer exists to provide **rigorous, deterministic personal archaeology** with absolute privacy:
- We distinguish **observed facts** (*"Ahmed sent 31.4% of messages"*) from speculative inferences.
- We avoid unsupported psychological profiling, mental-health claims, or relationship scoring ("who is toxic", "who is the best friend").
- We run 100% inside your web browser.

---

## Privacy Architecture

| Guarantee | Implementation Details |
| :--- | :--- |
| **Zero Server Ingestion** | All ZIP extraction, JSON parsing, and analysis occur locally inside client-side TypeScript. |
| **No Account or Database** | No login, signup, user database, or persistent cloud storage. |
| **No Telemetry / Beacons** | Zero Google Analytics, Facebook Pixel, tracking beacons, or telemetry scripts. |
| **No External LLM Calls** | Analytics are deterministic algorithms. No private text is dispatched to external AI providers. |
| **Untrusted Input Hardening**| ZIP path traversal attacks (`../`) are neutralized; transcript rendering escapes all HTML entities. |
| **Memory Isolation** | High-resolution binary video/image payloads in ZIPs are skipped during decompression to avoid memory leaks. |

Read the full [Privacy Documentation](./docs/PRIVACY.md).

---

## Quick Start

### 1. Prerequisites
- [Node.js](https://nodejs.org/) v18.0.0 or higher
- npm, pnpm, or yarn

### 2. Local Setup

```bash
# Clone the repository
git clone https://github.com/your-username/group-chat-analyzer.git
cd group-chat-analyzer

# Install dependencies
npm install

# Run automated test suite
npm test

# Start local development server
npm run dev
```

Open your browser to `http://localhost:3000`.

### 3. Immediate Demo Dataset
If you don't have an export archive ready, click the **"Try Demo"** button on the landing screen to instantly explore a pre-bundled synthetic conversation spanning 3 years, 6 members, and over 1,500 messages with Arabic and English dialogue, reactions, and inside jokes.

---

## How to Export Your Messenger Data

Meta provides official data exports through the centralized **Accounts Center**:

1. Open Facebook in a desktop browser and navigate to **Settings & privacy** &rarr; **Settings** &rarr; **Accounts Center** &rarr; **Your information and permissions** &rarr; **Download your information** (or navigate directly to [facebook.com/dyi](https://www.facebook.com/dyi)).
2. Select **Download to device**.
3. Choose **Select types of information**, check **Messages**, and uncheck all other categories.
4. Set **Format** to **JSON** (Required. Do not select HTML).
5. Set **Date range** to **All time** (for full history) and **Media quality** to **Low** (to minimize download size).
6. Submit your request. Once Meta prepares your archive, download the `.zip` file and drop it into Group Chat Analyzer.

> [!WARNING]
> **End-to-End Encryption (E2EE) Notice:** Meta now encrypts personal Messenger chats by default. Encrypted chat history is managed via **Messenger Secure Storage**. If recent messages appear missing from your standard Facebook export, follow our [Messenger Secure Storage Guide](./docs/GETTING_FACEBOOK_MESSENGER_DATA.md#troubleshooting-my-recent-messenger-messages-are-missing).

---

## Supported Data

Group Chat Analyzer provides first-class support for both Meta conversational ecosystems:

| Platform | Ingestion Target | Multi-File Fragment Merging | Group Detection |
| :--- | :--- | :---: | :---: |
| **Facebook Messenger** | JSON ZIP or extracted folder | Automatic (`message_1.json`, `message_2.json`, ...) | Automatic (signals > 2 members or group metadata) |
| **Instagram Direct** | JSON ZIP or extracted folder | Automatic (`message_1.json`, `message_2.json`, ...) | Automatic (signals > 2 members or group metadata) |
| **WhatsApp / Discord** | Planned canonical adapters | Roadmap | Roadmap |

Read our detailed export manuals:
- [📘 Facebook Messenger Export Guide](./docs/GETTING_FACEBOOK_MESSENGER_DATA.md)
- [📸 Instagram Direct Export Guide](./docs/GETTING_INSTAGRAM_MESSAGE_DATA.md)
- [🧭 Export Landing Guide](./docs/GETTING_YOUR_CHAT_DATA.md)

---

## Analysis Features

```text
analysis/
├── OverviewStats         # Volume, calendar span, active days, cadence, median lengths
├── ParticipantStats      # Individual metrics, word counts, script breakdown, peak hours
├── TemporalStats         # 7x24 heatmap, 24-hour distribution, weekday distribution
├── SessionsStats         # Activity bursts (60m gap), longest session, longest silence
├── StartersStats         # % and count of bursts initiated per member
├── ResponseTimeStats     # Approximate response delays, median/mean, distribution buckets
├── InteractionStats      # Circular network graph, consecutive transition matrix
├── ReactionsStats        # Reactions leaderboard, given vs received, top-reacted messages
├── EmojisStats           # Unicode pictographic extraction, emoji-heavy member rankings
├── VocabularyStats       # Stopword filtering, single words, bigrams, trigrams, inside jokes
├── EvolutionPeriod[]     # Monthly evolution cards, active participants, recurring terms
└── NotablePeriod[]       # Factual highlights, single-day records, peak expressive days
```

Every metric is mathematically defined and accompanied by known limitations in our [Analysis Methods Reference](./docs/ANALYSIS_METHODS.md).

---

## Screenshots & Interface Overview

The interface is structured into 8 cohesive analytical workspaces:

- **Overview Tab**: Group DNA cards, message composition progress bars (text vs. media vs. system events), temporal cadence, and milestone records.
- **Activity Tab**: Monthly and daily message volume timeline, 7×24 activity heatmap with interactive cell inspection, 24-hour distribution, and day-of-week bar charts.
- **People Tab**: Detailed participant summary cards and full comparative sortable table with script ratios and attachment metrics.
- **Interactions Tab**: Interactive circular SVG transition graph highlighting turn-taking networks, top interacting pairs, and response delay distribution buckets.
- **Text & Lexicon Tab**: Candidate recurring phrases ("inside joke" candidate detector), word clouds, bigram/trigram selectors, and emoji leaderboards.
- **Evolution Tab**: Monthly interactive drill-down cards displaying top active participants and keywords across the years.
- **Transcript Explorer Tab**: In-memory keyword search, participant dropdown filter, attachment filter, and paginated message context.
- **Export & Share Tab**: Visual summary share card, CSV participant statistics export, and privacy-safe JSON summary download.

---

## Architecture

```text
User's Computer
       │
   Export ZIP / Directory
       │
       ▼
Browser File API (Client-side FileReader / ArrayBuffer)
       │
       ▼
Streaming ZIP Decompressor (fflate)
  • Path traversal sanitization
  • Selective JSON decompression (skips video/image blobs)
       │
       ▼
Platform Discovery & Adapters
  ├── FacebookMessengerAdapter
  └── InstagramAdapter
       │
       ▼
Normalization & Encoding Repair
  • Meta Latin-1/UTF-8 mojibake repair
  • Unicode Normalization Form C (NFC)
  • Extended Pictographic emoji extraction
       │
       ▼
Canonical Normalized Model (Conversation / Message[])
       │
       ▼
Deterministic Analytics Engine
  (Overview · Temporal · People · Bursts · Responses · Interactions · Lexicon)
       │
       ▼
React UI (Tailwind CSS · Interactive SVG Visualizers · Share Cards)
```

Read the technical specifications in [Data Format](./docs/DATA_FORMAT.md) and [Research Paper](./docs/RESEARCH.md).

---

## Limitations

- **Encrypted Messenger Archives**: Standard Meta account downloads may omit recent end-to-end encrypted Messenger messages unless retrieved via desktop Secure Storage export.
- **Approximate Interaction Metrics**: Response times and interaction edges are operational heuristics based on consecutive messages within configured time windows; they do not represent cryptographic reply confirmations.
- **Browser Memory Limits**: Extremely massive exports (>500,000 messages) may require modern browsers with sufficient available RAM.

---

## Roadmap

- [x] **v0.1**: Meta Group Chat Analyzer (Facebook Messenger & Instagram Direct JSON, client-only architecture, deterministic analytics, share cards).
- [ ] **v0.2**: Dialect-aware Arabic tokenization, language detection, and topic cluster modeling.
- [ ] **v0.3**: Local IndexedDB saved sessions and historical comparative diffs.
- [ ] **v0.4**: Optional local WebGPU / Ollama LLM narrative summaries.
- [ ] **v0.5**: WhatsApp and Discord canonical export adapters.

---

## Contributing

We welcome contributions, bug reports, and synthetic test fixtures!

1. Fork the repository and create your branch from `main`.
2. Do **not** commit real private chat exports or personal names to Git. Use synthetic test fixtures.
3. Ensure all tests pass: `npm test`.
4. Ensure the production build compiles cleanly: `npm run build`.
5. Submit a pull request with a descriptive summary of your changes.

---

## License

This project is open-source under the [MIT License](./LICENSE).
