***Human-in-the-Loop (HITL) AI Email Assistant***

**The Problem:** High-volume inboxes lead to delayed responses, but fully autonomous AI replies can be risky for professional communication.

**The Solution:** A "Human-in-the-Loop" agent that monitors incoming Gmail messages, generates context-aware drafts using LLMs, and waits for a user "Approval" via a simple interface before sending.

**Technical Highlights:**

Contextual Prompting: Sends the email thread to an LLM with specific instructions to maintain the brand's tone of voice.

Confirmation Workflow: Utilizes n8n's "Human review" node to pause execution until the user verifies the draft.

Automation Loop: Upon approval, the agent automatically executes the Gmail: Send command and archives the original thread.
