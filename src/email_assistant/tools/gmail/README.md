# Gmail Integration Tools

Connect your email assistant to Gmail and Google Calendar APIs.

## Graph

The `src/email_assistant/email_assistant_hitl_memory_gmail.py` graph is configured to use Gmail tools.
  
You simply need to run the setup below to obtain the credentials needed to run the graph with your own email.

## Setup Credentials

### 1. Set up Google Cloud Project and Enable Required APIs

#### Enable Gmail and Calendar APIs

1. Go to the [Google APIs Library and enable the Gmail API](https://developers.google.com/workspace/gmail/api/quickstart/python#enable_the_api)
2. Go to the [Google APIs Library and enable the Google Calendar API](https://developers.google.com/workspace/calendar/api/quickstart/python#enable_the_api)

#### Create OAuth Credentials

1. Authorize credentials for a desktop application [here](https://developers.google.com/workspace/gmail/api/quickstart/python#authorize_credentials_for_a_desktop_application)
2. Go to Credentials → Create Credentials → OAuth Client ID
3. Set Application Type to "Desktop app"
4. Click "Create"

> Note: If using a personal email (non-Google Workspace) select "External" under "Audience"

<img width="1496" alt="Screenshot 2025-04-26 at 7 43 57 AM" src="https://github.com/user-attachments/assets/718da39e-9b10-4a2a-905c-eda87c1c1126" />

> Then, add yourself as a test user
 
5. Save the downloaded JSON file (you'll need this in the next step)

### 2. Set Up Authentication Files

1. Move your downloaded client secret JSON file to the `.secrets` directory

```bash
# Create a secrets directory
mkdir -p src/email_assistant/tools/gmail/.secrets

# Move your downloaded client secret to the secrets directory
mv /path/to/downloaded/client_secret.json src/email_assistant/tools/gmail/.secrets/secrets.json
```

2. Run the Gmail setup script

```bash
# Run the Gmail setup script
python src/email_assistant/tools/gmail/setup_gmail.py
```

-  This will open a browser window for you to authenticate with your Google account
-  This will create a `token.json` file in the `.secrets` directory
-  This token will be used for Gmail API access

## Use With A Local Deployment

### 1. Run the Gmail Ingestion Script with Locally Running LangGraph Server

1. Once you have authentication set up, run LangGraph server locally:

```
langgraph dev
```

2. Run the ingestion script in another terminal with desired parameters:

```bash
python src/email_assistant/tools/gmail/run_ingest.py --email vinaykiranreddychinnakondu@gmail.com --minutes-since 60
```

- By default, this will use the local deployment URL (http://127.0.0.1:2024) and fetch emails from the past 60 minutes.
- It will use the LangGraph SDK to pass each email to the locally running email assistant.
- It will use the `email_assistant_hitl_memory_gmail` graph, which is configured to use Gmail tools.

#### Parameters:

- `--graph-name`: Name of the LangGraph to use (default: "email_assistant_hitl_memory_gmail")
- `--email`: The email address to fetch messages from (alternative to setting EMAIL_ADDRESS)
- `--minutes-since`: Only process emails that are newer than this many minutes (default: 60)
- `--url`: URL of the LangGraph deployment (default: http://127.0.0.1:2024)
- `--rerun`: Process emails that have already been processed (default: false)
- `--early`: Stop after processing one email (default: false)
- `--include-read`: Include emails that have already been read (by default only unread emails are processed)
- `--skip-filters`: Process all emails without filtering (by default only latest messages in threads where you're not the sender are processed)

#### Troubleshooting:

- **Missing emails?** The Gmail API applies filters to show only important/primary emails by default. You can:
  - Increase the `--minutes-since` parameter to a larger value (e.g., 1000) to fetch emails from a longer time period
  - Use the `--include-read` flag to process emails marked as "read" (by default only unread emails are processed)
  - Use the `--skip-filters` flag to include all messages (not just the latest in a thread, and including ones you sent)
  - Try running with all options to process everything: `--include-read --skip-filters --minutes-since 1000`
  - Use the `--mock` flag to test the system with simulated emails

### 2. Connect to Agent Inbox

After ingestion, you can access your all interrupted threads in Agent Inbox (https://dev.agentinbox.ai/):
* Deployment URL: http://127.0.0.1:2024
* Assistant/Graph ID: `email_assistant_hitl_memory_gmail`
* Name: `Graph Name`
