# Perpetual Hub Ultra

## What is Perpetual Hub Ultra?

Perpetual Hub Ultra is a complete, turnkey perpetual futures platform that any trading venue can launch under its own branding, without building a specialized chain, bootstrapping liquidity, or running a complex backend.

With **Ultra 2.0**, the entire perps stack runs in-house on Orbs Layer-3 infrastructure: execution, settlement, hedging, liquidation, pricing, and a professional-grade trading UI, with no third-party dependencies. Liquidity is sourced from day one through the platform's integrated hedging infrastructure, so venues can go live with deep execution immediately.

### The Full Stack, In-House

Every component required to run a high-performance perps venue runs natively within Orbs' Layer-3 infrastructure. A single, unified stack handles the entire trading lifecycle, from the moment an order is placed to the moment it settles on-chain.

For integrating venues, that means fewer dependencies, fewer points of failure, and a faster path to launch. For traders, it means smoother execution and consistent performance under real market conditions.

The protocol sources and hedges across multiple deep liquidity venues. This multi-source approach delivers tighter pricing, deeper books, and the flexibility to support a far wider universe of trading pairs than any single venue could offer alone.

### TEE-Verified Execution

At the core of Ultra 2.0's architecture is a Trusted Execution Environment (TEE) that serves as the authoritative engine for all state transitions. Every trade, position update, and liquidation runs inside this environment, with remote attestation ensuring the execution logic has not been tampered with.

The architecture breaks down into several core components:

#### Hedger

Trusted, whitelisted hedgers with high-SLA guarantees take the operational counterparty role, hedging across multiple deep liquidity venues. This multi-venue approach delivers deep, professional-grade execution from day one without relying on external solver networks.

#### Liquidator

Real-time solvency monitoring with automatic position liquidation when maintenance margin thresholds are breached. Cross-margin risk calculations use the same shared formulas across the entire stack, so there is no discrepancy between what a trader sees and what the system enforces.

#### Price Oracle

A signed mark-price feed inside the TEE drives risk calculations, funding rates, and liquidation decisions. Prices are cryptographically signed with EIP-712 and verified on every operation, creating a verifiable audit trail for every price input that affects the system.

#### On-Chain Rollup Settlement

All state, including user positions, balances, pending orders, and system configuration, lives in a unified Merkle tree. State roots are committed on-chain via a rollup contract, so every transition from order placement to settlement is verifiable. The result is the transparency of on-chain with the performance of off-chain execution.

### A CeFi-Grade Trading Experience

Ultra 2.0 ships with a complete, exchange-grade trading interface, fully customizable to the host venue's brand. It runs on TradingView charts and includes the full suite of order types serious traders expect: market and limit orders, stop-loss and take-profit, and advanced brackets.

Combined with one-click trading, account abstraction, and gasless flows, traders get professional-grade polish with the self-custody and transparency of on-chain.

### Built for Many Venues, Across Many Chains

Perpetual Hub Ultra scales horizontally: the same complete stack can power a network of branded perps venues across multiple chains.

QuickSwap, a long-standing Orbs integration partner, passed a governance vote to adopt Perpetual Hub Ultra as the default perps infrastructure across all QuickSwap chains, with more venue announcements to follow.

Any trading venue can launch a full perpetual futures platform, branded, deeply liquid, and feature-complete, with minimal development effort and a fast time to market.

Learn more about Perpetual Hub Ultra [HERE](https://www.orbs.com/perpetual-hub/)
