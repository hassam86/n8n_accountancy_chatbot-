# 🤖 AI Accounting Chatbot (n8n + Google Sheets)

An intelligent accounting assistant built with **n8n**, designed to automatically record, categorize, and update financial transactions in **Google Sheets** using **AI automation**.

This chatbot understands user prompts (like *“Add a business expense for lunch, 50 AED”*) and automatically updates your accounting sheet with structured data — including **Date**, **Transaction Type**, **Description**, **Currency Conversion to USD**, and **Action Type**.

---

## 🚀 Features

- 💬 **Natural Language Input** — Users can type transactions in plain English.
- 📊 **Automatic Google Sheet Update** — AI processes inputs and records them in real time.
- 💱 **Currency Conversion** — Converts any currency to USD automatically.
- 🧾 **Categorization** — Classifies each entry as *Personal* or *Business*.
- ⏰ **Dynamic Date Handling** — Always logs the correct current date.
- 🔗 **Telegram Integration** — Supports direct interaction through a Telegram bot.
- 🧠 **AI-Powered Accounting** — Uses OpenAI API (via n8n AI Agent) for intelligent parsing and logic.

---

## 🧩 Workflow Structure

The n8n workflow consists of the following nodes:

1. **Telegram Trigger**
   - Captures messages from users sent to your Telegram bot.

2. **AI Agent (OpenAI)**
   - System prompt defines the AI’s accountant behavior.
   - Parses messages and prepares structured transaction data:
     - `Date`
     - `Personal/Business Type`
     - `Description`
     - `Amount`
     - `Currency (converted to $)`
     - `Action`

3. **Google Sheets Node**
   - Automatically updates the relevant sheet with parsed data.

4. *(Optional)* **Manual Trigger**
   - Used for testing or debugging without Telegram activation.

---

## ⚙️ Setup Instructions

### 1. Prerequisites
- [n8n](https://n8n.io) (self-hosted or cloud)
- [Google Cloud Console](https://console.cloud.google.com/) project with Sheets API enabled
- [Telegram Bot Token](https://core.telegram.org/bots#3-how-do-i-create-a-bot)
- OpenAI API key

---

### 2. Setup Steps

#### Step 1: Import Workflow
1. Export or copy the provided JSON file into your n8n instance.
2. Open n8n → “Import Workflow” → Paste JSON → Save.

#### Step 2: Configure Credentials
- **Google Sheets Node** → Connect your Google account.
- **Telegram Trigger** → Paste your Telegram Bot Token.
- **AI Agent** → Connect your OpenAI API key.

#### Step 3: Prepare Google Sheet
Create a sheet with columns:
| Date | Type | Description | Amount | Currency ($) | Action |
|------|------|--------------|---------|----------------|----------|

#### Step 4: Activate Workflow
- Keep the workflow **active** to receive messages from Telegram.
- To **test manually**, deactivate it and click **“Execute Workflow.”**

---

## 🧮 Example Prompt

**User:**  
> Add 230 AED business expense for office lunch today  

**AI Output (Google Sheet Entry):**

| Date       | Type     | Description    | Amount | Currency ($) | Action   |
|-------------|----------|----------------|---------|----------------|-----------|
| 08-11-2025  | Business | Office Lunch   | 62.69  | USD            | Expense  |

---

## 🧠 System Prompt Used

```json
{
  "role": "system",
  "content": "You are a smart accountant AI agent. When user sends a message about a financial transaction, extract all key fields: Date (use {{$json.today_date}}), Personal/Business type, Description, Currency conversion to USD, and Action (Expense/Income). Return structured data for Google Sheets update only, no extra text."
}
