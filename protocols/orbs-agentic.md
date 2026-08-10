# Orbs Agentic

## What is Orbs Agentic?

Orbs Agentic is the execution layer between AI agents and DeFi protocols. When an agent needs to swap, place a limit order, or run a TWAP strategy, it calls an Orbs Agentic tool. The Orbs Network handles execution, routing, and cosigned-oracle verification, so every trade is independently verified on-chain.

Orbs Agentic is not a wallet, not a custodial layer, and not AI trading. It is the verification and execution layer that lets agents execute DeFi safely.

### The need for an agent execution layer

DeFi usage is shifting from humans clicking through UIs to AI agents executing programmatically. Agent frameworks such as LangChain, CrewAI, Eliza, and MCP-based tooling can reason about markets, but reasoning is not the bottleneck holding back autonomous DeFi. The bottleneck is trust, safety, and execution:

* **Safety** - An agent with signing power can be manipulated, hallucinate parameters, or act outside its mandate. Without independent verification, there is nothing between an agent's decision and an irreversible on-chain transaction.
* **Execution quality** - Naive swaps suffer from poor routing, slippage, and MEV. Agents need the same execution infrastructure that professional trading products use.
* **Reliability** - Real execution requires handling retries, partial fills, token approvals, gas, and RPC failures. This operational burden should not sit inside every agent.

Orbs Agentic addresses all three by giving agents structured tools backed by the same Orbs L3 infrastructure that has powered DEX execution products since 2022.

### The Cosigned Oracle

The core security mechanism of Orbs Agentic is the cosigned oracle, which separates strategy from execution security:

1. The agent decides what to do and submits an intent (for example: swap 1,000 USDC to ETH with max 0.5% slippage)
2. The Orbs oracle independently verifies the intent against its constraints: slippage bounds, price checks, and execution conditions
3. Only when verification passes does the oracle cosign, and the transaction is executed on-chain

The agent owns the strategy. The Orbs Network enforces execution safety. An agent cannot go rogue past the constraints it was given, because every trade requires the oracle's independent cosignature before anything moves.

Agents do not manage gas or transaction broadcast. Orbs handles the full execution flow.

### Execution tools

Orbs Agentic exposes a single execution tool with flexible, composable parameters. The agent defines the order configuration, and Orbs handles the execution flow:

* **autoswap** - Agent-driven token swaps with smart routing and slippage protection. The default for most trades.
* **autolimit** - Limit orders with on-chain execution guarantees. Set a price and walk away.
* **secureswap** - Additional cosigned oracle verification for higher-stakes trades. Extra checks before anything moves.
* **TWAP** - Spread large trades over time to minimize price impact, with configurable duration and slicing.

Example call:

```javascript
orbs.autoswap({
  token_in: "USDC",
  token_out: "ETH",
  amount: 1000,
  max_slippage: 0.5
})
```

Routed, verified, cosigned, executed. One call.

### Supported networks

Orbs Agentic supports Ethereum, BNB Chain, Polygon, Arbitrum, Base, Avalanche, Sonic, and Linea.

### Powered by the Orbs Network

All Agentic execution runs on the decentralized Orbs Network. Guardians operating under Proof-of-Stake consensus power the routing, verification, and cosigned-oracle services, the same infrastructure behind the Orbs Advanced Orders Suite (dTWAP, dLIMIT, dSLTP) and Liquidity Hub.

Learn more at [orbs.com/agentic](https://www.orbs.com/agentic/)
