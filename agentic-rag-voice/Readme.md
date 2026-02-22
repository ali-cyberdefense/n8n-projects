# Agentic RAG — Voice-Powered Customer Service Agent

![n8n](https://img.shields.io/badge/n8n-Workflow%20Automation-orange)
![Supabase](https://img.shields.io/badge/Supabase-Vector%20Store-green)
![ElevenLabs](https://img.shields.io/badge/ElevenLabs-Voice%20Agent-purple)
![OpenAI](https://img.shields.io/badge/OpenAI-Embeddings%20%26%20LLM-blue)

## The Problem

Traditional customer service systems rely on rigid FAQ scripts or expensive human agents. Customers get frustrated with chatbots that can't understand context, and businesses struggle to keep knowledge bases accessible and up to date.

## The Solution

A two-part Agentic RAG (Retrieval-Augmented Generation) system that ingests company knowledge into a vector database, then serves it through an AI voice agent (via ElevenLabs) that acts as a natural-sounding customer service representative — answering questions using your actual company data.

## How It Works

**Phase 1 — Data Ingestion:** Company knowledge from Google Sheets is embedded and stored in Supabase vector database.

**Phase 2 — Voice Retrieval:** ElevenLabs voice agent calls the webhook → AI Agent retrieves relevant knowledge from Supabase → responds conversationally via voice.

## Architecture Overview

```
Phase 1: Data Ingestion
========================
Google Sheets → Edit Fields → Supabase Vector Store
                                    ↑
                              OpenAI Embeddings


Phase 2: Voice Retrieval (RAG)
===============================
ElevenLabs Voice Agent
        │
        ▼ (Webhook - POST)
┌─────────────────────┐
│      AI Agent       │
│  ┌───────────────┐  │
│  │ Supabase      │  │  ← Retrieves relevant knowledge chunks
│  │ Vector Store  │  │
│  └───────────────┘  │
│  + Simple Memory    │  ← Maintains conversation context
│  + OpenAI Chat Model│
└─────────┬───────────┘
          ▼
  Respond to Webhook  → Voice response back to caller
```

## Agents Breakdown

### 1. Data Ingestion Workflow
**Purpose:** Converts company knowledge into searchable vector embeddings.

- Manually triggered (run once or when data updates)
- Pulls rows from **Google Sheets** containing company knowledge/FAQ data
- **Edit Fields** node structures the data for embedding
- **OpenAI Embeddings** converts text into vector representations
- **Supabase Vector Store** stores the embeddings with the **Default Data Loader** for retrieval

### 2. RAG Voice Agent
**Purpose:** Answers customer questions using company knowledge, delivered via voice.

- **Webhook** (POST) receives requests from the ElevenLabs voice agent
- **AI Agent** processes the customer's question using OpenAI Chat Model
- **Supabase Vector Store** (as a tool) performs similarity search to find relevant knowledge
- **Simple Memory** maintains conversation history for multi-turn dialogues
- **Respond to Webhook** sends the answer back to ElevenLabs for voice synthesis

## Technical Highlights

- **Agentic RAG Pattern:** AI Agent decides when and how to query the vector store — not hardcoded retrieval, but intelligent, context-aware search
- **Vector Embeddings:** OpenAI embeddings enable semantic search — finds answers based on meaning, not keyword matching
- **Voice Integration:** ElevenLabs voice agent provides a natural phone/voice interface for end users
- **Webhook + Respond to Webhook:** Full request-response cycle — voice agent sends a question, waits on the line, and gets a meaningful answer back
- **Conversational Memory:** Simple Memory node enables multi-turn conversations so the agent remembers previous questions in the same session
- **Scalable Knowledge Base:** Update Google Sheets and re-run ingestion — no code changes needed to expand the agent's knowledge

## Tools & Integrations

| Tool | Role |
|------|------|
| n8n | Workflow orchestration & agent framework |
| OpenAI API | Chat model (LLM) + text embeddings |
| Supabase | PostgreSQL vector database (pgvector) |
| ElevenLabs | Voice agent — speech-to-text & text-to-speech |
| Google Sheets | Source data for knowledge base |
| Webhook / Respond to Webhook | API endpoint for voice agent communication |

## Workflow Screenshots

### Data Ingestion Pipeline
![Data Ingestion](https://i.ibb.co/nsPmRtMW/image.png)

### RAG Voice Agent
![RAG Agent](https://i.ibb.co/7xvV6vxf/image.png)
