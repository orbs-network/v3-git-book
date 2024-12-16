# Liquidity Hub

## What is Liquidity Hub?

Liquidity Hub is a decentralized optimization layer for DEXs enabling DEXs to tap into external liquidity sources in order to provide CeFi-competitive prices on swaps.

### The Need for Aggregated Liquidity

DEX-AMMs are the driving engine behind the DeFi revolution, as its most fundamental cornerstone. One of the most basic roles of any DEX is to provide its users with the best price possible when executing a trade. Better prices are obtained via better liquidity. However, on-chain liquidity is highly fragmented as it is spread across different chains, across different AMMs within the chain, and across different pools within the AMM.

The problem of liquidity fragmentation in DeFi has become acute and directly impacts users via adverse exchange prices and material negative price impact on swaps.

**Liquidity Hub by Orbs brings the power of aggregated liquidity to any DEX-AMM, enabling them to provide better price quotes to their users without jeopardizing their liquidity providers.**

### Architecture & Product Spec

Instead of the typical swap that searches for the best route within the DEX's limited liquidity pools, Liquidity Hub enhances this process by utilizing additional liquidity sources:

1. **On-chain solver auction**: Third-party solvers who compete to fill swaps using on-chain liquidity like AMM pools or their own private inventory.
2. **Decentralized orders via API**: Decentralized orders, accessible using API. Enabling institutional/professional traders, such as market makers, to submit bids and compete to fill swaps.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXe7lXMeM-YKBhKYakRmhmHPyIynd0FpvTUfAWjd48Rge_aX3_Tgr-SeLMycoVenpp2hEE-whTNSu9dcekOAkYFBoK2owBMN3MBd4YFwcBSM95Gvc0fgXaLHS0ljv15X6Im4h605679Zz7U0LNebfTBJ3gD6?key=PQMpZ1E3MCh7GiRyPT59fw" alt=""><figcaption></figcaption></figure>

Liquidity Hub allows DEXs to attempt to execute trades without going through the AMM and experiencing AMM price impact. If the layer is unable to execute the trade at a better price than the AMM, the trade will fallback to the AMM contract and execute as usual.

Therefore, Liquidity Hub can only improve a trader’s experience. If Liquidity Hub isn’t competitive, meaning it would only execute at a worse price for the user or can’t execute at all, the swap will be routed through the AMM contract directly as usual.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdP7EXnaVZ1QSjvJ-TOtYDp5WgSZsPJDOTv-o5jxggqfOXQiD12foJWquKaQGdFYqUOdUSzY2zGUcsUTp-UKJVdP9lCTubMdJ-7Wt4vjqTXGPQWBY5Mj4UEshWPW1h_vrq46hPKy_vh7TIFJBg6dt7yertW?key=PQMpZ1E3MCh7GiRyPT59fw" alt=""><figcaption></figcaption></figure>

### Mitigating Centralization risks using Orbs L3

All on-chain parts are trustless since contracts verify all actions. However, one may be concerned that the off-chain Liquidity Hub backend is able to manipulate trades in some way. This is avoided by using Orbs’ decentralized L3 technology.

As part of Liquidity Hub, Orbs Guardians will run software utilizing [ORBS-VM](https://docs.orbs.network/v3/orbs-vm/what-is-orbs-vm) that acts as a decentralized backend that is required for Liquidity Hub’s off-chain portion to run optimally and in a fully decentralized manner.

Learn more about Liquidity Hub [HERE](https://www.orbs.com/Liquidity-Hub-by-Orbs-The-New-Standard-for-DEXs/)
