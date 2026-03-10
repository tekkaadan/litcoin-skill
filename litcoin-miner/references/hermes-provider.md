# Using LITCOIN as a Hermes Agent LLM Provider

LITCOIN's compute marketplace serves AI inference through a decentralized relay network. It's fully OpenAI-compatible and works as a Hermes Agent provider with zero code changes.

## How It Works

1. Relay miners connect to the LITCOIN coordinator via WebSocket
2. They register their AI provider (Venice, OpenAI, Groq, Together, etc.) and available models
3. When you send a request to `/v1/chat/completions`, the coordinator routes it to the best available relay
4. The relay processes the request using their own API key (your data never touches their key)
5. Response streams back to you

## Setup

### Option A: API Key Auth (recommended)

Get an API key at https://litcoiin.xyz/compute (Connect tab):

```bash
# ~/.hermes/.env
OPENAI_BASE_URL=https://api.litcoiin.xyz/v1
OPENAI_API_KEY=lk_YOUR_KEY
```

### Option B: Wallet Auth

If you have LITCREDIT balance:

```bash
# ~/.hermes/.env  
OPENAI_BASE_URL=https://api.litcoiin.xyz/v1
# No API key needed — use X-Wallet header (handled by SDK)
```

### Option C: Free Tier

5 requests per hour, no key needed:

```bash
# ~/.hermes/.env
OPENAI_BASE_URL=https://api.litcoiin.xyz/v1
OPENAI_API_KEY=free
```

## Available Models

Models depend on which relays are online. Check with:

```bash
curl https://api.litcoiin.xyz/v1/models
```

Common models available: llama-3.3-70b, gpt-4o, claude-3.5-sonnet (depends on relay miners).

## Features Supported

- Streaming (SSE)
- Tool/function calling
- Multi-turn conversations
- System prompts
- Temperature, top_p, max_tokens
- Provider targeting (specific relay selection)

## Targeting a Specific Relay

If you want to use a specific miner's relay:

```json
{
  "model": "llama-3.3-70b",
  "messages": [{"role": "user", "content": "Hello"}],
  "provider": "0xabc..."
}
```

## Network Status

Check relay health: https://litcoiin.xyz/compute
API endpoint: `GET https://api.litcoiin.xyz/v1/compute/providers`

## Costs

- Free tier: 5 requests/hour
- LITCREDIT: 1 LITCREDIT = 1,000 output tokens of frontier inference (~$0.01)
- Relay miners earn LITCOIN for serving your requests

## Hermes-Specific Notes

- Works with `hermes model` — select "Custom Endpoint" and enter the base URL
- Hermes's vision tools, MoA, and web summarization may need a separate OpenRouter key (they call OpenRouter independently)
- The LITCOIN endpoint does not support image inputs — use OpenRouter for vision tasks alongside LITCOIN for text
