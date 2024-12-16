# dLIMIT Protocol

## What is dLIMIT?

### Intro to dLIMIT

Most DeFi users are probably familiar with the regular DEX “swap” order, similar to a market order in CeFi.

A limit order, on the other hand, enables users to buy or sell tokens at a specified price or better. While the price is guaranteed, the order being executed is not - limit orders will be executed only if the price meets the order qualifications.

However, decentralized limit orders are not trivial to implement using smart contracts. Flawed implementation of limit orders in DeFi can hurt users by executing the order at a price much worse than they intended, or the order not being executed at all.

This is where Orbs L3 steps in - the Orbs dLIMIT [smart contract](https://github.com/orbs-network/twap) for DEXs ensures that limit orders are executed at an optimal price and at fair fees, in a decentralized and reliable manner.

In addition, the Orbs team has designed a UI template that can be easily integrated and customized by any DEX, to create an intuitive, user-friendly, and informative way for users to set up limit orders trades.

### Contract Architecture and Design

dLIMIT is based on the [dTWAP protocol](https://www.orbs.com/dtwap/) by Orbs and is in fact a specific instance of dTWAP-limit order, in which the total order size equals the individual trade size.

dTWAP is an [audited](https://github.com/orbs-network/twap/blob/master/Audit-Report-PeckShield.pdf), production-tested product that has been integrated into major DEXs such as Sushiswap, QuickSwap (the largest native DEX on Polygon) and SpookySwap (largest on Fantom), with millions of dollars in trading volume to date.
