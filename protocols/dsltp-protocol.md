# dSLTP Protocol

### Introduction to dSLTP

dSLTP, powered by Orbs, is the first DeFi implementation of a decentralized stop order solution for DEXs. Built on Orbs’ Layer-3 technology, dSLTP delivers reliable, robust, and efficient execution of stop-loss and take-profit orders — all in a fully decentralized manner.

Stop orders are essential tools for strategic trading, as they help protect investments by limiting potential losses through **stop-loss** orders and enable traders to capitalize on market breakouts with **take-profit** triggers.

_dSLTP is part of Orbs Advanced Orders Suite, which also includes_ [_dLIMIT_](https://www.orbs.com/dlimit/) _and_ [_dTWAP_](https://www.orbs.com/dtwap/)_, bringing advanced order types to DeFi that were once available only on centralized exchanges._

### Stop-loss and Take-profit orders

A **stop-loss order** is an advanced trading tool that enables users to limit potential losses by selling a token if its price moves against their position. For example, suppose a token’s price drops by a predetermined percentage. A stop-loss order helps ensure it is sold at the best available price, protecting the user’s portfolio from further losses.

Stop-loss orders are a critical risk management tool, especially in **volatile markets**, as they provide a safeguard when prices move unfavorably.

A **take-profit** order is an advanced trading tool that enables traders to set a predefined price level at which to secure profits from an open position. When combined with stop-loss orders, it enables better trade management, helping optimize potential gains while controlling risk.

<figure><img src="../.gitbook/assets/unknown.png" alt=""><figcaption></figcaption></figure>



### How to set up a stop-loss order

In this section, we’ll show an example of how to set up a stop-loss order using dSLTP

1. Select the STOP LOSS order in the DEX UI

<figure><img src="../.gitbook/assets/unknown (2).png" alt="" width="563"><figcaption></figcaption></figure>

2. Choose the “**From**” and “**To**” tokens and enter the amount you wish to trade.

* **Example**: You hold **1 BNB** at the current market price of **\~$839** and want to place a stop-loss order to sell 1 BNB for USDT if the price falls below a certain threshold.

<figure><img src="../.gitbook/assets/unknown (3).png" alt="" width="563"><figcaption></figcaption></figure>

\
3\. Specify the Trigger Price. The trigger price is the price at which the stop-loss order will be activated.

* **Example**: You set the trigger price 5% **below the current market price** of BNB.

<figure><img src="../.gitbook/assets/unknown (4).png" alt="" width="563"><figcaption></figcaption></figure>



4. Choose Order Type: Market or Limit.&#x20;

Both order types have their advantages and risks, and choosing between them depends on the user’s priorities.

* **Stop-loss market orders** guarantee that your order will be executed once the stop price is triggered. However, in fast or volatile markets, slippage can occur, and the executed price may be significantly worse than the trigger price. This means the amount of output tokens received could be lower than expected.
* **Stop-loss limit orders** protect against receiving a worse price than your specified limit. Once the stop price is triggered, the order will execute only at the limit price or better. The downside is that if the market price falls below your limit, the order may not execute at all.
* **Example**: Use a stop-loss **limit** order with a limit price **8% below the market price**.

<figure><img src="../.gitbook/assets/unknown (6).png" alt="" width="563"><figcaption></figcaption></figure>

\
5\. Set Order Expiry - Define how long the stop-loss order will remain active.

* Example: Set expiry to 1 week.

<figure><img src="../.gitbook/assets/unknown (7).png" alt="" width="563"><figcaption></figcaption></figure>



6. Review and Submit Order

All of the parameters have now been defined and we are ready to do a final review and submit our order.



<figure><img src="../.gitbook/assets/unknown (9).png" alt="" width="563"><figcaption></figcaption></figure>



**Example summary:**

* You hold 1 BNB, expecting the price to rise, but you want protection if it drops.
* Trigger price: **$799** (5% below market price).
* Limit price: **$774** (8% below market price).

\
This means that if BNB’s price falls below $799, the trigger price will be activated and the order will sell 1 BNB to USDT at the closest price possible to our trigger price. The order will execute as long as the price is equal or above our limit price of $774.

If the price drops rapidly below our limit before the order manages to execute, our stop-loss order will not execute (unless the price rebounds back above the limit).

As mentioned above, a limit price provides us with downside protection but does not guarantee execution.\


<figure><img src="../.gitbook/assets/unknown (12).png" alt="" width="563"><figcaption></figcaption></figure>



7. View and Manage Orders

Open orders and order history can be accessed at any time in the DEX UI. Open orders can be canceled by clicking the **Cancel** button.

<figure><img src="../.gitbook/assets/unknown (14).png" alt="" width="563"><figcaption></figcaption></figure>



### Powered by Orbs

The dSLTP protocol is developed by [Orbs](https://www.orbs.com/) and powered by Orbs’ [L3 technology](https://www.orbs.com/overview/).

Orbs Network has dozens of independent validators running Proof-of-Stake consensus. The network has been running in mainnet since 2019. All Orbs Network validators are takers and participate as honest bidders in the protocol, guaranteeing that orders are executed 24/7 with high redundancy and best price.

### Troubleshooting and FAQ

Still unsure of something? Having trouble with your order? Be sure to check the [FAQ](https://www.orbs.com/dtwap-and-dlimit-faq/) section.

### Additional resources

You can find more information about dSLTP in the following links:

* [FAQ](https://www.orbs.com/dtwap-and-dlimit-faq/)&#x20;
* dTWAP/dSLTP telegram [support group](https://t.me/dTWAPSupportGroup)
* dSLTP webpage
* [Github](https://github.com/orbs-network/liquidity-hub/blob/v2/README.md)
* security audit
