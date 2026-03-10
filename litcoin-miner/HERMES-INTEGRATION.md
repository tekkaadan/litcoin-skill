# LITCOIN + Hermes Agent Integration

Three ways Hermes Agent and LITCOIN work together.

---

## 1. Use LITCOIN Relays as Your LLM Provider

LITCOIN's relay network is an OpenAI-compatible inference endpoint. Relay miners serve AI using their own API keys. You pay with LITCREDIT, they earn LITCOIN.

```bash
# In ~/.hermes/.env
OPENAI_BASE_URL=https://api.litcoiin.xyz/v1
OPENAI_API_KEY=lk_YOUR_KEY
```

Or use the free tier (5 requests/hour, no key needed):
```bash
OPENAI_BASE_URL=https://api.litcoiin.xyz/v1
OPENAI_API_KEY=free
```

Available models depend on what relay miners are online. Check:
```bash
curl https://api.litcoiin.xyz/v1/models
```

---

## 2. Install the LITCOIN Skill

The LITCOIN skill teaches Hermes how to mine, stake, claim, research, and manage the full DeFi stack.

**From ClawHub:**
```bash
hermes skills search litcoin
hermes skills install tekkaadan/litcoin
```

**From GitHub:**
```bash
# Or manually copy the litcoin-miner/ folder into ~/.hermes/skills/
```

Once installed, just ask Hermes:
- "Mine some LITCOIN for me"
- "Check my LITCOIN balance"  
- "Run 50 research iterations on sorting"
- "Stake into Circuit tier"
- "Claim my rewards"

The skill includes the full SDK reference — `pip install litcoin` is all Hermes needs to execute.

---

## 3. Autonomous Mining via Cron

Set up Hermes to mine LITCOIN on autopilot:

```
/cron add "0 */2 * * *" "Run 10 rounds of LITCOIN mining, then 5 research iterations. Claim if claimable > 100K."
```

Or a daily research session:
```
/cron add "0 8 * * *" "Check LITCOIN research tasks. Pick the one with the most room for improvement. Run 20 research iterations. Post results to Telegram."
```

Hermes runs these unattended via the gateway daemon. Results are delivered to your configured messaging platform.

---

## Architecture Overview

```
Hermes Agent
  ├── Uses LITCOIN relay as LLM provider (OpenAI-compatible)
  ├── Loads LITCOIN skill for protocol knowledge
  ├── Runs pip install litcoin in terminal
  ├── Calls agent.mine(), agent.research_loop(), agent.claim()
  └── Schedules autonomous mining via cron
  
LITCOIN Coordinator (api.litcoiin.xyz)
  ├── /v1/chat/completions  ← Hermes uses this for inference
  ├── /v1/challenge          ← Mining challenges
  ├── /v1/research/submit    ← Research submissions  
  ├── /v1/claims/status      ← Reward tracking
  └── /v1/models             ← Available relay models

Relay Miners
  └── Serve inference requests from Hermes (and any OpenAI-compatible client)
  └── Earn LITCOIN for each fulfilled request
```

---

## Links

- Site: https://litcoiin.xyz
- Research Lab: https://litcoiin.xyz/research
- SDK: `pip install litcoin` (PyPI v4.0.1)
- MCP: `npx litcoin-mcp` (npm v2.0.0, 25 tools)
- ClawHub Skill: tekkaadan/litcoin
- Twitter: @litcoin_AI
