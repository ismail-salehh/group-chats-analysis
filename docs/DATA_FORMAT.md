# Data Format & Canonical Model

Group Chat Analyzer uses a platform-neutral **canonical data model** to separate platform-specific export quirks from the core analytical engine.

---

## Architecture Pipeline

```text
Export ZIP or Folder
        ↓
Platform Adapters
├── FacebookMessengerAdapter
└── InstagramAdapter
        ↓
Canonical Conversation Model
├── Conversation
├── Participant[]
└── Message[]
        ↓
Deterministic Analysis Engine
        ↓
Interactive Web UI & Reports
```

---

## Canonical Schema

```typescript
export type Platform = "facebook" | "instagram" | "whatsapp" | "discord" | "unknown";

export interface Participant {
  id?: string;
  name: string;
}

export interface Reaction {
  emoji: string;
  actor?: string;
}

export interface Message {
  id?: string;
  threadId: string;
  platform: Platform;
  sender: string;
  timestampMs: number;
  text: string | null;
  normalizedText?: string;
  messageType: string | null;
  reactions: Reaction[];
  hasMedia: boolean;
  mediaCount: number;
  isSystemEvent: boolean;
  isUnsent: boolean;
  rawType?: string;
}

export interface Conversation {
  id: string;
  platform: Platform;
  title: string | null;
  participants: Participant[];
  messages: Message[];
  sourcePath?: string;
  isGroup: boolean;
  threadType?: string;
}
```

---

## Fragment Merging & Chronology

Meta splits long conversation histories across multiple numbered files:

```text
messages/inbox/thegroup_12345/
├── message_1.json
├── message_2.json
└── message_3.json
```

1. **Fragment Collection**: All files under the same directory are grouped together.
2. **Merging**: Message records across all files are merged into a single array.
3. **Chronological Sorting**: Messages are sorted in ascending order by `timestamp_ms`. (Filename numbering is not chronological).
4. **Conservative Deduplication**: Any overlapping duplicate records (matching timestamp, sender, and content) are deduplicated.
5. **Encoding Repair**: Meta's Latin-1/UTF-8 mojibake bug (where UTF-8 bytes were decoded as ISO-8859-1) is automatically detected and repaired for Arabic, Latin accents, and emojis.
