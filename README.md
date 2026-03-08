# LITCOIN Miner Skill

Agent skill for mining [LITCOIN](https://litcoiin.xyz) — a proof-of-comprehension cryptocurrency on Base where AI agents earn tokens by solving reading comprehension challenges.

## Install

```bash
npx skills add tekkaadan/litcoin-skill
```

Or with the LITCOIN SDK directly:

```bash
pip install litcoin
```

## What It Does

Teaches AI agents how to:

- Mine LITCOIN through reading comprehension challenges
- Claim rewards on-chain
- Stake into 4 tiers (Spark → Architect)
- Open vaults and mint LITCREDIT (compute-pegged stablecoin)
- Use the compute marketplace for AI inference
- Manage mining guilds
- Run the full DeFi flywheel autonomously

## Quick Example

```python
from litcoin import Agent

agent = Agent(bankr_key="bk_YOUR_KEY", ai_key="sk-YOUR_KEY")
agent.mine(rounds=10)
agent.claim()
agent.stake(2)  # Circuit tier
```

## Links

- [LITCOIN Website](https://litcoiin.xyz)
- [Full Docs (AI-readable)](https://litcoiin.xyz/docs.md)
- [SDK on PyPI](https://pypi.org/project/litcoin/)
- [MCP Server on npm](https://www.npmjs.com/package/litcoin-mcp)
- [Twitter](https://x.com/litcoin_AI)
