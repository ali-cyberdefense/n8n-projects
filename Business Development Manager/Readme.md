# Business Development Manager — Multi-Agent System

![n8n](https://img.shields.io/badge/n8n-Workflow%20Automation-orange)
![OpenAI](https://img.shields.io/badge/OpenAI-API-blue)
![Pipedrive](https://img.shields.io/badge/Pipedrive-CRM-green)
![Gmail](https://img.shields.io/badge/Gmail-Email%20Drafts-red)

## The Problem

Business development teams waste hours on repetitive manual work — researching prospects, entering data into CRMs, and drafting outreach emails. Each step is disconnected, slow, and error-prone, especially for small teams without dedicated RevOps support.

## The Solution

A multi-agent AI system built in n8n that automates the entire business development pipeline — from prospect discovery to CRM entry to personalized email drafting — triggered simply by uploading an Ideal Customer Profile (ICP) document to Google Drive.

## How It Works

Upload an ICP document (PDF) to Google Drive → The **BDM Manager Agent** reads it, delegates tasks to three specialized sub-agents, and orchestrates the full pipeline automatically.

## Architecture Overview

```
Google Drive (ICP Upload)
        │
        ▼
┌─────────────────────────┐
│   BDM Manager Agent     │  ← Orchestrator: reads ICP, delegates & controls sub-agents
│   (Google Drive Trigger) │
└────────┬────────────────┘
         │
    ┌────┼──────────────┐
    ▼    ▼              ▼
┌───────┐ ┌──────────┐ ┌───────┐
│Prospect│ │  RevOps  │ │  SDR  │
│ Agent  │ │  Agent   │ │ Agent │
└───┬───┘ └────┬─────┘ └───┬───┘
    │          │            │
    ▼          ▼            ▼
 Firecrawl  Pipedrive    Gmail
  (MCP)      (CRM)     (Drafts)
```

## Sub-Agents Breakdown

### 1. Prospecting Sub-Agent
**Purpose:** Finds and researches potential client prospects based on the ICP criteria.

- Triggered by the BDM Manager via "Execute Sub-Workflow"
- Uses **Firecrawl MCP** to scrape and research companies matching the ICP
- Processes data through **OpenAI API** for intelligent prospect analysis
- Returns **structured output** (parsed via Structured Output Parser) back to the manager
- Equipped with **Simple Memory** for context retention during multi-step research

### 2. RevOps Sub-Agent
**Purpose:** Loads qualified prospect data into Pipedrive CRM automatically.

- Receives parsed prospect data from the manager agent
- AI Agent analyzes and structures the data for CRM entry
- Executes a three-step CRM pipeline in **Pipedrive**:
  - **Create Organization** → company record
  - **Create Person** → contact record linked to the organization
  - **Create Lead** → sales lead linked to the person and organization

### 3. SDR Sub-Agent (Sales Development Rep)
**Purpose:** Drafts personalized outreach emails for each prospect.

- Pulls contact data from **Pipedrive** (Get Many People)
- AI Agent crafts professional, personalized **HTML emails** for each prospect
- Creates email drafts in **Gmail** — ready for human review before sending

## Technical Highlights

- **Multi-Agent Orchestration:** Manager agent delegates to and coordinates three specialized sub-agents using n8n's "Execute Sub-Workflow" pattern
- **Google Drive Trigger:** Workflow activates automatically when an ICP file is uploaded — no manual execution needed
- **MCP Integration:** Firecrawl MCP server enables real-time web scraping for prospect research
- **Structured Output Parsing:** Ensures AI responses follow a consistent schema for reliable downstream processing
- **CRM Automation:** Full Pipedrive pipeline — organization, person, and lead creation — in a single automated flow
- **Conditional Notifications:** IF node routes success/failure outcomes to Pushover push notifications

## Tools & Integrations

| Tool | Role |
|------|------|
| n8n | Workflow orchestration & agent framework |
| OpenAI API | LLM powering all four agents |
| Google Drive | Trigger — ICP document upload |
| Firecrawl (MCP) | Web scraping for prospect research |
| Pipedrive | CRM — organizations, persons, leads |
| Gmail | Email draft creation |
| Pushover | Mobile push notifications |
| Structured Output Parser | Schema-enforced AI responses |

## Workflow Screenshots

### BDM Manager (Orchestrator)
![BDM Manager](https://i.ibb.co/PvCwKgy7/image.png)

### Prospecting Sub-Agent
![Prospecting Agent](https://i.ibb.co/KjJCXLfY/image.png)

### RevOps Sub-Agent
![RevOps Agent](https://i.ibb.co/C551YPWC/image.png)

### SDR Sub-Agent
![SDR Agent](https://i.ibb.co/C3sL3fcv/image.png)
