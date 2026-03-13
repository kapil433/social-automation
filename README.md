# Social Automation — Pillar 2

> **Personal OS**: Blog → **Automation** → Projects → Research

Automates distribution of long-form content from the personal blog to social media platforms. You write long — this system summarizes and distributes. You stay out of short-form entirely.

## Architecture

```
[Blog RSS Feed]
      ↓
[n8n Trigger: new post detected]
      ↓
[Fetch full article text]
      ↓
[Claude/GPT API: generate platform copies]
      ↓
[Telegram: human approval gate]  ← YOU APPROVE HERE
      ↓
[Route by platform]
├── LinkedIn: professional tone, bullet structure, 1200 chars
└── Twitter/X: 270 chars, punchy, data hook
      ↓
[Log: Airtable/Notion — date, title, platform, engagement]
```

## Components

### OpenClaw (Agent Brain)
- **SOUL.md** — Agent identity: writes in Kapil's voice (data-first, automotive/complexity lens, no hype)
- **AGENTS.md** — Operational playbook: channels to monitor, heartbeat schedule
- **MEMORY.md** — Long-term memory of tasks and context
- Runs locally or on private server
- Connects to 134+ MCP tools including social publishers

### n8n (Workflow Orchestrator)
- Visual workflow connecting blog RSS → Claude API → social platforms
- Cron-triggered: checks for new posts
- Heartbeat every 30 minutes for pending tasks

## Folder Structure

```
social-automation/
├── openclaw/
│   ├── SOUL.md          ← Agent identity and voice
│   ├── AGENTS.md        ← Operational playbook
│   ├── MEMORY.md        ← Long-term memory template
│   └── HEARTBEAT.md     ← Pending tasks checklist
├── n8n/
│   ├── workflows/
│   │   └── blog-to-social.json   ← n8n workflow export
│   └── README.md
├── prompts/
│   ├── linkedin-prompt.md        ← Platform-specific prompts
│   └── twitter-prompt.md
└── README.md
```

## Setup

### 1. OpenClaw Installation
```bash
npm install -g openclaw
openclaw init
# Choose: Anthropic (Claude)
# Enter API key (stored locally only)
# Connect Telegram bot via @BotFather
```

### 2. Configure SOUL.md
```
You are Kapil's content agent. You summarize his long-form blog posts
into platform-specific social copies. You write in his voice:
data-first, no hype, domain-specific (automotive, complexity science, policy).
Never add emojis unless the post is on Instagram.
Never hallucinate stats — only use what is in the source article.
```

### 3. n8n Workflow
Import `n8n/workflows/blog-to-social.json` into your n8n instance.

Configure nodes:
- RSS Feed URL: `https://kapil433.github.io/personal-blog/feed.xml`
- Claude API key (in n8n credentials)
- LinkedIn + Twitter API credentials
- Telegram Bot token (for approval gate)

## Key Principle

> You write long → OpenClaw/n8n summarizes + distributes → You stay out of short-form entirely.

## Part of the Four-Pillar System

```
Pillar 1: personal-blog
Pillar 2: social-automation (this repo)
Pillar 3: msil-work-tool | commercialize-analytics | complexity-lab
Pillar 4: research-platform
```
