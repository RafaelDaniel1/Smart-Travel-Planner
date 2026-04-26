# Smart Travel Planner - cf_ai_travel_planner

A Cloudflare-based AI application that creates personalized travel itineraries using Llama 3.3, Workers, Durable Objects (for Memory), and an API interface for chat and itinerary generation.

## ✨ Features

* **🤖 AI-Powered Planning**: Uses **Llama 3.3 (70B)** via Workers AI to generate structured itineraries.
* **🔄 Workflow Coordination**: The main Worker orchestrates a multi-step process: User input $\rightarrow$ State check/update (DO) $\rightarrow$ AI model call $\rightarrow$ State update (DO) $\rightarrow$ Response.
* **💾 Memory Storage**: Uses **Durable Objects** (`SessionManager`) to maintain conversation history and user travel preferences (state).
* **💬 User Input**: Interactive API endpoints (`/chat` and `/itinerary`) for conversation-based planning.
* **🚀 Cloudflare Stack**: Built on Workers, Workers AI, and Durable Objects.

## ⚙️ Tech Stack

* **LLM**: `@cf/meta/llama-3.3-70b-instruct-fp8-fast` via Workers AI
* **Compute**: Cloudflare Workers
* **State Management / Memory**: Durable Objects (`SessionManager`)
* **Configuration**: `wrangler.toml`

## 🚀 Quick Start

### Prerequisites

* Node.js 18+
* Wrangler CLI (`npm install -g wrangler`)
* Cloudflare account with Workers AI enabled.

### Local Development

1.  **Clone the repository:**
    ```bash
    git clone [your-repo-url]
    cd cf_ai_travel_planner
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    ```
3.  **Configure Wrangler:**
    ```bash
    wrangler login
    ```
4.  **Run locally:**
    ```bash
    wrangler dev
    ```
    Access the application API endpoints at `http://localhost:8787`.

### Deployment

Deploy the Worker and Durable Object:

```bash
wrangler deploy

curl -X POST "[https://your-worker.your-subdomain.workers.dev/itinerary](https://your-worker.your-subdomain.workers.dev/itinerary)" \
  -H "Content-Type: application/json" \
  -d '{
    "destination": "Seoul, South Korea",
    "duration": "7 days",
    "interests": ["K-pop", "street food", "history"],
    "budget": "high",
    "session_id": "user-a1b2c3d4"
  }'


curl -X POST "[https://your-worker.your-subdomain.workers.dev/chat](https://your-worker.your-subdomain.workers.dev/chat)" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "What is the best way to get from the airport?",
    "session_id": "user-a1b2c3d4"
  }'
