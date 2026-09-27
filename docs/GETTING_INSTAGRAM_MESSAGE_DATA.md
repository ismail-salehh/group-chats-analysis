# How to Export Instagram Direct Message Data

A step-by-step guide for exporting Instagram Direct group conversations in JSON format.

---

## Step-by-Step Export Instructions

### Step 1 — Open Instagram Accounts Center
1. Open [Instagram](https://www.instagram.com) in your web browser.
2. Click **More** (bottom left menu) &rarr; **Settings**.
3. In the sidebar, click **Accounts Center** &rarr; **Your information and permissions**.
4. Click **Download your information** (or navigate to `accountscenter.instagram.com`).

### Step 2 — Request a Download
1. Click **Request a download**.
2. Select your **Instagram profile**.

### Step 3 — Select Specific Information
1. When asked what information to include, select **Select types of information**.
2. Check **Messages** (Direct Messages) only.

### Step 4 — Choose Device Download
Select **Download to device**.

### Step 5 — Configure JSON Format & Date Range
- **Format**: Select **JSON** (Required).
- **Media quality**: Select **Low** (speeds up export and reduces file size).
- **Date range**: Select **All time** for complete history, or select a custom range.

### Step 6 — Submit & Download
1. Click **Submit request**.
2. Meta will prepare your export. Check back or wait for the confirmation email.
3. Once available, download the `.zip` archive to your computer.

### Step 7 — Import into Group Chat Analyzer
Drag and drop your Instagram `.zip` archive into Group Chat Analyzer. The app will detect your Instagram Direct threads, merge split fragments (`message_1.json`, `message_2.json`, etc.), and surface your group conversations for analysis.

---

## Notes on Instagram Direct Exports

- **Group Thread Detection**: Instagram group chats are detected automatically when a thread has 3 or more participants or carries group thread identifiers.
- **Fragments**: Long-running Instagram DMs are often split across multiple `message_N.json` files within the `messages/inbox/<thread>/` directory. Group Chat Analyzer merges all files chronologically and deduplicates any overlaps.
- **Privacy**: The analyzer never sends any Instagram messages to any server or external service. All calculations occur inside your browser.
