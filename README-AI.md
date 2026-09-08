# WeatherGPT — AI Chatbot Setup

The chatbot is powered by a server-side Groq LLM and can call a live Open-Meteo weather tool. The browser never receives the Groq API key.

## 1. Install

Use the existing package manager setup from `package.json` (Bun is recommended because the project includes `bun.lock`).

```bash
bun install
```

## 2. Add your AI key

Copy `.env.example` to `.env` and set:

```env
GROQ_API_KEY="your-groq-api-key"
```

Do NOT put this key in a `VITE_` variable and do not commit `.env` to GitHub.

The project already contains the Supabase variables needed by the existing authentication flow. Keep those values in your local `.env`.

## 3. Run

```bash
bun dev
```

Open the local URL shown by Vite and sign in to use `/chat`.

## Where to edit the AI

Main AI logic:

`src/lib/chat.functions.ts`

Edit:
- `SYSTEM_PROMPT` → personality, behavior, response rules
- `WEATHER_TOOL` → what weather data the AI is allowed to request
- `getWeather()` → geocoding + Open-Meteo data
- `callGroq()` → AI model, temperature, token limit
- `sendChatMessage()` → conversation memory, tool loop, validation

Chat UI:

`src/routes/_authenticated/chat.tsx`

Edit:
- `SUGGESTIONS` → starter questions
- `ask()` → sending messages and receiving AI responses
- message rendering → appearance of user/AI messages

## Model

The current implementation uses Groq's OpenAI-compatible chat completions endpoint with `openai/gpt-oss-20b`. You can change the model in `callGroq()` if your Groq account supports another model.
