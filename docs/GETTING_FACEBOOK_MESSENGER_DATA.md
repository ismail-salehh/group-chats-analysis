# How to Export Facebook Messenger Data

A complete guide for exporting your Facebook Messenger conversation history in JSON format.

---

## Step-by-Step Export Instructions

### Step 1 — Open Facebook
Open [Facebook](https://www.facebook.com) in your web browser and sign into the account containing the group chat you want to analyze.

### Step 2 — Open Accounts Center
- Click your profile photo in the top right corner.
- Go to **Settings & privacy** &rarr; **Settings**.
- In the left sidebar, click **Accounts Center** (or navigate directly to [facebook.com/dyi](https://www.facebook.com/dyi)).
- Under *Account settings*, select **Your information and permissions**.
- Click **Download your information** (or **Export your information**).

### Step 3 — Select Your Facebook Profile
If multiple accounts appear in your Accounts Center, check only the Facebook profile that participates in the group conversation.

### Step 4 — Choose Device Download
Select **Download to device** (rather than transferring directly to another cloud service).

### Step 5 — Select Specific Information
Choose **Select types of information** (rather than downloading your entire Facebook history).
Check **Messages** and uncheck everything else.

### Step 6 — Choose the Date Range
- For a complete historical overview of the chat, choose **All time**.
- If you only want to analyze a specific semester, year, or trip, select a custom date window.

### Step 7 — Set Format to JSON (Critical)
Set **Format** &rarr; **JSON**.
Do not choose HTML. HTML is styled for manual viewing, whereas JSON provides the structured timestamp and participant records needed for mathematical analysis.

### Step 8 — Set Media Quality to Low
Set **Media quality** &rarr; **Low**.
Because Group Chat Analyzer focuses on text statistics, timestamps, and interaction graphs, you do not need full-resolution images or videos. Low quality makes Meta generate the archive much faster.

### Step 9 — Submit the Request
Click **Create files** / **Submit request**. Meta may prompt you to re-enter your Facebook password for security.

### Step 10 — Wait for Meta Notification
Meta prepares the archive on their servers. This may take anywhere from a few minutes to several hours depending on the size of your message history. You will receive an email and Facebook notification once the file is ready.

### Step 11 — Download the ZIP Archive
Return to the *Download your information* page under the **Available downloads** tab and download the `.zip` archive to your computer.

### Step 12 — Import into Group Chat Analyzer
Open Group Chat Analyzer in your browser, drag and drop the `.zip` file into the import box (or click *Choose file*). The application will automatically discover conversation threads, parse fragments, and display your chats.

---

## Troubleshooting: "My Recent Messenger Messages Are Missing"

If you notice recent messages from the past few months are missing from your export:

> [!WARNING]
> Meta rolled out default **End-to-End Encryption (E2EE)** across Messenger chats. Encrypted messages are stored locally on your devices and backed up using **Messenger Secure Storage**, which can cause recent encrypted history to be separated from standard account downloads.

To retrieve encrypted history via Secure Storage:
1. Open [Messenger.com](https://www.messenger.com) on your computer.
2. Click your profile avatar in the bottom left corner.
3. Select **Privacy & safety**.
4. Go to **End-to-end encrypted chats** &rarr; **Message storage** (or **Secure storage**).
5. Select **Download secure storage data** if available for your account.
6. Enter your password to authorize the download and save the resulting ZIP.

*Note: Group Chat Analyzer will analyze whatever records exist in the files you supply. Missing messages should not be interpreted as messages that never existed.*
