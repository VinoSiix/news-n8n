Here's a copy-paste ready `README.md` for your n8n workflow:

---

# 📰 BBC World News Digest to Telegram

This n8n workflow automatically fetches the latest world news from the BBC RSS feed, aggregates them into a digest, summarizes the content into tweet-ready format using AI, and sends the output to a Telegram chat.

## 🔄 Workflow Overview

1. **Schedule Trigger**  
   Triggers the workflow on a defined schedule.

2. **RSS Feed Reader**  
   Fetches news items from [BBC World News RSS Feed](https://feeds.bbci.co.uk/news/world/rss.xml).

3. **Aggregate News (Function Item)**  
   Processes the RSS feed data by extracting titles, descriptions, and links, then combines them into a single digest string.

4. **Limit**  
   Ensures only the latest items are passed forward (configurable).

5. **AI Agent**  
   Uses a language model to convert the news digest into concise tweets (280 characters or less), preserving key information.

6. **Cohere Chat Model**  
   Provides the AI model used by the agent. Requires valid Cohere API credentials.

7. **Telegram Sender**  
   Sends the summarized tweets to a specified Telegram chat. Requires valid Telegram API credentials and a chat ID.

## ⚙️ Setup Instructions

### 1. **Credentials**
You need to configure the following credentials in n8n:

- **Cohere API**
  - Used by the "Cohere Chat Model" node.
  - [Get your API key from Cohere](https://dashboard.cohere.ai/)

- **Telegram API**
  - Used by the "Send a text message" node.
  - Obtain your Telegram bot token and set up a bot via [BotFather](https://core.telegram.org/bots#botfather).
  - Replace `YOUR-CHAT-ID` in the Telegram node with the actual chat ID where you want to send messages.

### 2. **Dependencies**
Ensure you have the following nodes installed:
- `n8n-nodes-base.scheduleTrigger`
- `n8n-nodes-base.rssFeedRead`
- `n8n-nodes-base.functionItem`
- `n8n-nodes-base.limit`
- `@n8n/n8n-nodes-langchain.agent`
- `@n8n/n8n-nodes-langchain.lmChatCohere`
- `n8n-nodes-base.telegram`

### 3. **Schedule Configuration**
Adjust the schedule in the **Schedule Trigger** node to run at your preferred interval (e.g., daily, hourly).

## 🧠 AI Prompt Used

The AI agent is instructed with the following system message:

> "Summarize input text into concise, ready-to-post tweets. Have 10 different outputs. Output complete tweets (280 chars or less) that can be copied directly. Preserve key information and intent strictly from the input."

## 📤 Output Example

The Telegram node will receive a message like:

```
Tweet 1: Breaking news from BBC World...
[Read more](https://www.bbc.com/news/...)

Tweet 2: Major update on global events...
[Read more](https://www.bbc.com/news/...)
...
```

## 📁 Notes

- The workflow ensures that only a limited number of recent news items are processed.
- The function node gracefully handles cases where no news is available.
- You can customize the RSS URL to fetch news from other sources.

## 🛠️ How to Import

1. Open your n8n instance.
2. Go to **Workflows** > **Import**.
3. Paste the JSON workflow data.
4. Configure credentials and node parameters as needed.
