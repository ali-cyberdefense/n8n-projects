**The Problem:** Stock market volatility requires rapid portfolio adjustments, but manual monitoring is inefficient for retail investors.

**The Solution:** A cross-platform agent that integrates real-time market data with personal investment targets to provide instant notifications and record-keeping.

**Technical Highlights:**

API Integration: Connects to the MarketStack API via REST to fetch live ticker prices.

Conditional Logic: Implements complex IF/Switch nodes to compare live prices against user-defined thresholds.

Multi-Channel Alerting: Executes a three-step output: updates Google Sheets, sends a formal Gmail summary, and triggers a mobile push notification (via Pushover/Telegram).
