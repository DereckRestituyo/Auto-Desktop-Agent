# Auto - Autonomous AI Desktop Agent

Auto is a locally hosted, multi-model AI desktop agent built in Python. Designed to operate as a self-correcting ReAct (Reason + Act) loop, Auto goes beyond standard chat interfaces by executing physical OS-level commands, orchestrating multiple LLMs dynamically, and retaining long-term contextual memory.

## 🚀 Core Architecture

*   **Multi-Model Router:** A dynamic routing engine that classifies prompts by complexity. It routes lightweight conversational tasks to fast, cost-effective models (Llama 3 70B) and heavy logical/coding tasks to enterprise-grade reasoners (DeepSeek-R1), optimizing API latency and token cost.
*   **The Hippocampus (Persistent Memory):** A self-repairing JSON database that acts as the agent's long-term memory. Using custom XML tag interception (`<REMEMBER>`), Auto autonomously extracts user preferences, schedules, and facts, injecting them into its master prompt upon boot.
*   **Autonomous ReAct Loop:** Auto operates inside a continuous `while True:` loop. If it lacks data, it triggers a `<SEARCH>` tag, executes a background web scrape using `BeautifulSoup`, reads the raw HTML data, and updates its own context before replying to the user.
*   **OS-Level Execution (The Hands):** Integrated with `subprocess` and `os` libraries, Auto intercepts `<ACTION>` tags to physically control the Windows environment. It can launch local IDEs, open specific web workflows, or trigger local applications autonomously.
*   **Dynamic Privacy Firewall:** Includes a Zero Data Retention (ZDR) toggle that activates automatically when routing to specific uncensored endpoints, guaranteeing strict data privacy for sensitive logic tasks.
*   **Live Telemetry & Cost Tracking:** Intercepts hidden OpenRouter API payload data to calculate and print a live financial ledger (Input/Output token cost) directly to the terminal on every query.

## 🛠️ Tech Stack
*   **Language:** Python 3.10
*   **APIs:** OpenRouter, Google Generative AI
*   **Key Libraries:** `requests`, `BeautifulSoup`, `subprocess`, `sqlite3`, `edge-tts`, `pygame`, `re`, `json`

## 🧠 System Directives & Tag Interception
Auto uses strict internal directives to manage its logic loop. The Python backend catches these tags, executes the corresponding functions, and sanitizes the output before text-to-speech processing:
*   `<SEARCH>query</SEARCH>` - Triggers a background web scrape.
*   `<REMEMBER>fact</REMEMBER>` - Writes a new fact to `memory.json`.
*   `<ACTION>command</ACTION>` - Executes physical PC commands.
*   `<TESTCODE>python_code</TESTCODE>` - Writes code to a local sandbox file, runs it, and feeds terminal errors/successes back to the AI.
