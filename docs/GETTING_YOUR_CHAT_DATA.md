# Getting Your Group Chat Data

Group Chat Analyzer analyzes **official JSON exports** from Meta (Facebook Messenger and Instagram Direct).

Because all analysis runs **100% locally on your computer**, you never provide your login password, PIN, recovery codes, or cookies to this application. You simply request your data export directly from Meta, download the generated ZIP archive to your device, and drop it into Group Chat Analyzer.

---

## Which Guide Applies to You?

Select the guide matching the conversation platform:

1. [📘 How to Export Facebook Messenger Data](./GETTING_FACEBOOK_MESSENGER_DATA.md)
   - For Facebook Messenger group chats and community threads.
   - Covers Meta Accounts Center export settings, choosing JSON, and troubleshooting end-to-end encryption with Messenger Secure Storage.

2. [📸 How to Export Instagram Direct Data](./GETTING_INSTAGRAM_MESSAGE_DATA.md)
   - For Instagram Direct group chats.
   - Covers Instagram Accounts Center, selecting Messages only, and requesting JSON format.

3. [🔬 Technical Research & Export Specifications](./RESEARCH.md)
   - Deep dive into Meta's export architecture, encryption schemes, JSON schema structures, and character encoding mechanics.

---

## 3 Golden Rules for Exporting Meta Data

Regardless of whether you export from Facebook or Instagram:

1. **Always Choose JSON format** (Never HTML):
   - Meta offers HTML (designed for human viewing in a browser) and JSON (machine-readable structured records). Group Chat Analyzer requires **JSON** to calculate accurate timestamps, reactions, and metrics.
2. **Select Messages only** (to save time and disk space):
   - You do not need photos, posts, comments, or advertising history. Selecting only *Messages* will make Meta prepare your export significantly faster.
3. **Choose "Low" media quality**:
   - Because Group Chat Analyzer analyzes textual messages, word counts, and reaction timestamps, you do not need 4K videos or original high-resolution photos. Selecting *Low* media quality drastically reduces the ZIP file size.

---

## Privacy Notice

> [!IMPORTANT]
> Your exported archive contains messages, timestamps, and reactions from everyone in the group chat, not just you.
>
> Group Chat Analyzer processes everything inside your web browser and **never sends your files or messages to any server or external service**. However, when sharing screenshots, summary cards, or CSV files from the analyzer, please consider the privacy of other participants in your conversation.
