# AI Secretary — Main Router

A personal AI secretary built on Telegram that manages your calendar, tasks, reminders, and daily schedule through natural language conversation. Powered by OpenAI with PostgreSQL memory so it remembers context across sessions.

## What It Does

Chat with your AI secretary on Telegram and it will:

- **Manage your calendar** — create, update, and query Google Calendar events via natural language
- **Handle tasks and reminders** — log tasks to a database and remind you automatically
- **Remember context** — uses PostgreSQL chat memory so conversations are persistent across sessions
- **Route intelligently** — detects intent and routes to the right sub-agent (calendar, tasks, queries)
- **Send scheduled reminders** — schedule trigger checks for upcoming events and notifies you proactively
- **Query your data** — ask questions about your schedule and get structured answers

## Architecture

```
Telegram Trigger → AI Agent (OpenAI + Postgres Memory)
    → Intent Detection → Switch Router
        ├── Calendar Intent → Create/Update Google Calendar Event
        ├── Task Intent → Insert to Database → Confirm
        ├── Query Intent → SQL Query → Format → Reply
        └── Reminder Check (Scheduled) → Query DB → Send Telegram Alerts
```

## Tech Stack

- **n8n** — workflow orchestration
- **OpenAI GPT** — natural language understanding and response generation
- **PostgreSQL** — persistent chat memory and task/event storage
- **Telegram Bot** — conversational interface
- **Google Calendar** — calendar event management

## Key Features

- **Persistent memory** — PostgreSQL-backed chat history so the AI remembers previous conversations
- **Multi-agent routing** — separate specialised agents for calendar, tasks, and queries
- **Structured output parsing** — AI responses are parsed into structured data before database writes
- **Proactive reminders** — scheduled trigger checks for upcoming events and sends alerts automatically
- **Natural language interface** — no commands needed, just talk normally

## Example Conversations

```
You: Schedule a meeting with Mantas tomorrow at 3pm about the Hostinger interview
Bot: ✅ Created — "Meeting with Mantas" tomorrow at 15:00. I'll remind you an hour before.

You: What's on my schedule this week?
Bot: Here's your week: Monday — dentist 10am, Tuesday — Hostinger interview 2pm...

You: Remind me to send the invoice on Friday at 9am
Bot: ✅ Reminder set for Friday 09:00 — "Send the invoice"
```

## Setup

1. Import the workflow JSON into your n8n instance
2. Connect credentials:
   - Telegram Bot token
   - OpenAI API key
   - PostgreSQL database connection
   - Google Calendar OAuth2
3. Create the required PostgreSQL tables for chat memory, tasks, and events
4. Activate the workflow
5. Start chatting with your bot on Telegram

---

Built by [Shehroz Khan](https://www.linkedin.com/in/shehroz-khan-b91716197/) · Fullstack Automation Engineer
