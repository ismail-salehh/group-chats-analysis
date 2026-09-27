# Privacy Architecture & Data Protection

Group Chat Analyzer was built from the ground up as a **local-first, privacy-first analytical tool**.

---

## Core Privacy Commitments

1. **Zero Server Uploads**:
   - The application does not upload chat files, transcripts, or summaries to any server.
   - All ZIP decompression, JSON parsing, Unicode normalization, and analytics execution happen inside your local web browser.

2. **No Accounts or Authentication**:
   - No login, sign-up, or tracking ID is required.
   - We do not ask for Facebook credentials, passwords, session cookies, PINs, or recovery keys.

3. **No Database of Conversations**:
   - There is no central database storing user chats.
   - When you refresh or close the tab, the parsed conversation in memory is completely discarded.

4. **Zero Telemetry or Trackers**:
   - No analytics SDKs (Google Analytics, Mixpanel, etc.).
   - No advertising beacons or social pixels.
   - No crash reporter transmitting conversation excerpts.

5. **No Default External AI/LLM Calls**:
   - All metrics, token frequencies, and heatmaps are calculated using deterministic TypeScript algorithms.
   - No external AI API (OpenAI, Anthropic, Google, etc.) is invoked.

---

## Untrusted Input Security Defenses

Imported user files are treated as untrusted input. The application defends against common archive risks:

- **Path Traversal Protection**: ZIP file paths containing `../`, `..\\`, or absolute roots are discarded to prevent file injection attacks.
- **Selective Extraction**: High-resolution videos and photo media inside ZIP archives are skipped during decompression to protect memory usage and prevent out-of-memory browser crashes.
- **XSS Prevention**: All text rendered in transcripts and user lists is strictly sanitized and escaped against HTML injection.

---

## Participant Privacy Notice

> [!NOTE]
> When you export a group chat, the archive contains private thoughts, photos, and messages written by your friends, family, and colleagues.
>
> While Group Chat Analyzer guarantees that your data stays strictly on your computer, you should always respect the privacy expectations of other group participants before publishing screenshots, sharing summary cards, or distributing reports.
