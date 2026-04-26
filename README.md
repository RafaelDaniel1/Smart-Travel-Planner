# Smart Travel Planner (cf_ai_travel_planner)

## Overview

Smart Travel Planner is a Cloudflare-based AI application that generates personalized travel itineraries and provides conversational travel assistance. It uses Llama 3.3 via Cloudflare Workers AI and maintains user context using Durable Objects for memory and session state.

The system is designed as a full-stack serverless AI workflow that combines real-time user interaction, stateful memory, and structured itinerary generation.

---

## Features

* AI-powered travel planning
  Uses `@cf/meta/llama-3.3-70b-instruct-fp8-fast` via Cloudflare Workers AI to generate structured travel itineraries.

* Multi-step AI workflow

  ```
  User Input → Session State Check (Durable Objects)
  → AI Model Call → State Update → Response
  ```

* Persistent memory
  Uses Durable Objects (`SessionManager`) to store:

  * Chat history
  * User preferences
  * Session-based travel context

* Chat and itinerary APIs

  * `/chat` → conversational travel assistant
  * `/itinerary` → structured travel plan generator

* Serverless Cloud architecture
  Built on Cloudflare Workers, Workers AI, and Durable Objects

---

## Tech Stack

* AI Model: Llama 3.3 (70B Instruct) via Workers AI
* Backend: Cloudflare Workers
* State Management: Durable Objects (SessionManager)
* Frontend: HTML, JavaScript
* Configuration: wrangler.toml
* Runtime: Node.js + Wrangler CLI

---

## Project Architecture

```bash id="q8m1pa"
Client (HTML/JS)
        ↓
Cloudflare Worker (API Layer)
        ↓
SessionManager (Durable Object - Memory)
        ↓
Workers AI (Llama 3.3 Model)
        ↓
Structured Response (Itinerary / Chat)
```

---

## Setup and Installation

### Prerequisites

* Node.js 18+
* Wrangler CLI
* Cloudflare account with Workers AI enabled

---

### Clone Repository

```bash id="k2x9rv"
git clone https://github.com/RafaelDaniel1/cf_ai_travel_planner.git
cd cf_ai_travel_planner
```

---

### Install Dependencies

```bash id="n7v4qc"
npm install
```

---

### Login to Cloudflare

```bash id="d3p8tz"
wrangler login
```

---

### Run Locally

```bash id="s6j1lm"
wrangler dev
```

Application runs at:

```
http://localhost:8787
```

---

## API Usage

### Generate Itinerary

```bash id="t9c2vw"
curl -X POST "https://your-worker.your-subdomain.workers.dev/itinerary" \
  -H "Content-Type: application/json" \
  -d '{
    "destination": "Seoul, South Korea",
    "duration": "7 days",
    "interests": ["K-pop", "street food", "history"],
    "budget": "high",
    "session_id": "user-123"
  }'
```

---

### Chat Endpoint

```bash id="r4m7nx"
curl -X POST "https://your-worker.your-subdomain.workers.dev/chat" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "What is the best way to get from the airport?",
    "session_id": "user-123"
  }'
```

---

## My Contribution

* Designed full AI workflow architecture using Cloudflare Workers
* Implemented Durable Object-based session memory system
* Integrated Llama 3.3 model via Workers AI API
* Built chat and itinerary API endpoints
* Developed frontend interface for user interaction
* Coordinated request flow between AI model and persistent state

---

## Key Challenges

* Managing persistent state in a serverless environment
* Structuring multi-step AI workflows with latency constraints
* Designing session-based memory across stateless requests
* Handling AI response formatting for structured itineraries

---

## Future Improvements

* Add map visualization for itineraries
* Improve personalization using long-term memory profiles
* Add multi-user collaboration for shared trips
* Integrate real-time pricing for flights and hotels
