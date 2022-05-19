---
theme: academic
background: https://source.unsplash.com/collection/94734566/1920x1080
class: 'text-center'
highlighter: shiki
lineNumbers: false
info: |
  ## Scaling DLT's
  A short introduction for the *Blockchain Technology* Seminar SS22

  Course website at [Uni Tübingen](http://ps.informatik.uni-tuebingen.de/teaching/ss22/blockchain/)
drawings:
  persist: false
title: Welcome to Scaling DLT's
---

# Scaling DLT's

A short introduction for the *Blockchain Technology* Seminar SS22

---

# Outline

- **Motivation**
- **Approaches**
- **Layer-1 vs. Layer-2**
- **Lightning Network**
  - Bitcoin Scaling Problem
  - Hashed Timelock Contract (HLTC)
  - Importance for Bitcoin
- **Scaling Ethereum**
  - Primer - short introduction/recap
  - Sharding - ETH's L1 approach to scaling
  - Rollups - sharding isn't enough
- **Avalanche** - a different scaling approach based on consensus
- **Enter the rabbit hole** 🕳 🐇

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Motivation

<br>

![DLT Trilemma](/blockchain_trilemma.png)

<style>

img {
  filter: invert(97%) sepia(95%) saturate(19%) hue-rotate(257deg) brightness(105%) contrast(100%);
}

</style>

---

# Approaches

<v-click>

Any ideas?

</v-click>

<v-click>
  
- increasing block size
- nesting blockchains
- increase consensus efficiency
- state channels
- sidechains
- bundeling / rollups
- parallelization / sharding
  
</v-click>

<!-- 
# nesting vs. sidechains
# state channels
  - no open participation
  - lock up in multi-sig contract
   application specific
# sidenchains
  - rollups utilize sidechains
 -->

---
layout: two-cols
---
# Layer-1

- main DLT network protocol itself
- scaling solutions are changes to code or network structure itself
- e.g. Bitcoin, Ethereum, Avalanche,...

::right::

# Layer-2

- protocols sitting on top of the L1 to increase scalability or add functionality
- it comes down to **offloading effort off the chain**
- e.g. Optimism, Boba, Loopring..

<!-- 
# L2
  - lower fees
  - maintain security; benefit from mainnet security
  - expand use cases
 -->

---
layout: section
---

# ⚡️ Scaling Bitcoin 

![Illustration](/lightning_illustration.png)

---

## ⚡️ Bitcoin Scaling Problem

- huge impact on the network if every node must know about every single transaction
- Visa's 47,000 peak tps vs. &lt;7 tps <
- 1MB block limit
- increasing block size?
- principal-agent problem

<v-click>

### *Conduct transactions off the Bitcoin blockchain itself!*

</v-click>

<!--
- performance needs to be competitive to TradFi
- higher block size -> less people have the necessary bandwidth & hardware
- centralization; blockchain trilemma
- decentralization advantages NEED to be conserved
- large miners are encourage to act on their own interests even more...
-->

---

## ⚡️ Hashed Timelock Contract (HTLC)

---

## ⚡️ Implications for Bitcoin
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
  * institutions & whales  *exist*
              
# Micropayments
- no 3rd party custodian needed anymore
- e.g. paying per-megabyte for mobile internet

# Smart Contracts
- especially time sensitive
- complex transaction flows would be possible

# Cross-Chain Payments
- if hash function is similar across chains transactions could be routed across chains
 -->

---

## ⚡️ tl;dr
<br>
<img src="/lightning_flowchart.png" class="h-70 rounded" />

- opening and closing of payment channel is written on blockchain
- timelocks (HTLC's) are used to ensure communication in the channels
- enables fast and cheap Bitcoin payments down to the satoshi

---
layout: statement
---

## Is the Lightning Network a L1 or L2 scaling solution?🤔

<v-click>

L2

</v-click>

<!-- 
- L2
- but keep in mind that it enforcement still happens on the blockchain itself
  * deferral of state
  * opening and closing of payment channels
 -->

---
layout: statement
---
# 🏃🏻 Scaling Ethereum

"Ethereum is a technology that lets you send cryptocurrency to anyone for a small fee. It also powers applications that everyone can use and no one can take down."

### It's the world's programmable blockchain.

<!--
- a technology with this much impact and use cases should be fast and cheap
-->

---


## 🏃🏻 Primer

---
layout: image-right
image: ./sharding_eth.png
---

## 🏃🏻 Sharding

---
layout: image-right
image: ./sharding_eth.png
---

## 🏃🏻 Rollups

---

# ❄️ Avalanche - Finding Consensus

---

# Enter the rabbit hole 🕳 🐇
- [DeFi Developer Roadmap](https://github.com/OffcierCia/DeFi-Developer-Road-Map)


---

# Sources
- [Ethereum Illustrations](https://ethereum.org/en/assets/#illustrations)
- [Avalanche Illustrations](https://support.avax.network/en/articles/4132288-ava-labs-and-avalanche-press-kit-and-brand-assets)

---
layout: center
class: text-center
---

## Thank you for your attention!

<!--
[Documentations](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/showcases.html)
-->