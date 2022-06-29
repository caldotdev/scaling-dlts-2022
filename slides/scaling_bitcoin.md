---
layout: section
---
# <logos-bitcoin /> Scaling Bitcoin 

![Illustration](/img/lightning_illustration.png)

---

# <logos-bitcoin /> Scaling Problem
- huge impact on the network if every node must know about every single transaction
- Visa's 47,000 peak tps vs. &lt; 7 tps
- 1MB block limit
- increasing block size?
- principal-agent problem

<br>
<br>

<v-click>

### *Deal with transactions off the Bitcoin blockchain itself!*

</v-click>

<!--
- performance needs to be competitive to TradFi
- higher block size -> less people have the necessary bandwidth & hardware
- centralization; blockchain trilemma
- decentralization advantages NEED to be conserved
- large miners are encourage to act on their own interests
- PAP: Konflikt zwischen Verhalten der Representanten einer Gruppe und den Interessen der Gruppe selbst
- even more...

-->

---

# ⚡️ tl;dr
<br>
<img src="/img/lightning_flowchart.png" class="h-70 rounded" />

<v-clicks>

- opening and closing of payment channel is written on blockchain
- timelocks (HTLC's) are used to ensure communication in the channels
- enables fast and cheap Bitcoin payments down to the satoshi

</v-clicks>

<!-- 
# Satoshi
- kleinste Einheit von Bitcoin
- 1 satoshi = 0.00000001
-->

---
layout: center
---

## Is the Lightning Network a L1 or L2 scaling solution?🤔

<br/>
<br/>

<v-click>

# L2

</v-click>

<style>

  h1 {
    text-align: center;
  }

</style>

<!-- 
- L2
- but keep in mind that it enforcement still happens on the blockchain itself
  * deferral of state
  * opening and closing of payment channels
 -->

---

# <logos-bitcoin /> Implications for Bitcoin
The Lightning Network enables the following functionality for Bitcoin

- Instant Transactions
- Exchange Arbitrage
- Micropayments
- Financial Smart Contracts
- Cross-Chain Payments

<br>
<br>

<v-click>

### *Scaling does not "just" improve the speed of a network!*

</v-click>

<!-- 
# Exchange Arbitrage
- current incentive to hold funds on exchanges
- massive cold storages for exchanges might not longer be necessary (I disagree)
  * Lightning isn't for large payments
  * institutions & whales *exist*
              
# Micropayments
- no 3rd party custodian needed anymore
- e.g. paying per-megabyte for mobile internet

# Smart Contracts
- especially time sensitive
- complex transaction flows would be possible

# Cross-Chain Payments
- if hash function is similar across chains transactions could be routed across chains
 -->