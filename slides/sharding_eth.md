---
layout: image
image: /img/sharding_eth.png
---

# <logos-ethereum-color /> Sharding

---

# <logos-ethereum-color /> Sharding
- related to horizontal data partition
- shared-nothing architecture
	* shards are autonomous
  * memory & storage is not shared between nodes

<v-click>

- adds complexity & potential failure points ⚠️

</v-click>


<br>
<br>
<br>

<v-clicks>

### When to shard ? 🧐

- application data outgrows capacity of single database node
- slowed response times due to volume of read/writes to single node
- network bandwidth required is greater than the bandwidth available to a single node

</v-clicks>


<!--
![illustrations](/img/horizontal_partitioning.png)

- mehr Daten benötigt, als mit einem Node zu Verfügung zu stellen
- Performanzverlust
- Bandbreite
-->

---

commonly used: 

<img src="/img/sharding_implementations.png" class=" rounded" />

[Source](https://en.wikipedia.org/wiki/Shard_(database_architecture)#Implementations)


---

# <logos-ethereum-color /> Sharding through Random Sampling

<div class="container mx-auto flex flex-row justify-center">
  <img src="/img/sharding_committees.png" class="bg-white p-2 rounded" />
</div>
<br>

<v-click>

- randomly split verification work
- shuffle validator list and assign **committees** of size n to verify a block
- each validator publishes a signature upon block validation

</v-click>

---

# <logos-ethereum-color /> Sharding Consensus

### Important Definitions
- beacon chain
- **slot:** 12 second time-frame in which a block is expected to be added to the chain
- **epoch:** comprised of 32 slots
- **attestation** consisting of
  * vote for current beacon chain head
  * vote on which beacon block should be justified/finalized
  * vote on the current state of the shard chain
  * signatures of all validators agreeing with that vote

<!-- 
# beacon chain
- contains logic for keeping shards secure and synced
- assigns stakers to shards they need to work on
- facilitates cross-shard communications
- already went live

![Collations](/img/sharding_collation.png)
-->

---
layout: center
---

# How can we use the properties of attestations within a committee in a clever way?🤔

<style>

  h1 {
    text-align: center;
  }

</style>

<!-- 
Denkt an die vorher angedeutete Eigenschaft, dass nur die Signaturen verifizert werden müssen.

- if every attestation needed to be verified by all other nodes we would've not gained much
- **Übereinstimmung der Signaturen**
-->

---

# <logos-ethereum-color /> Sharding Consensus

- shard & beacon chain votes should be identical across validators within the same committee
- if we just had a way to combine all signatures... 🤷‍♂️
  - short-midterm: [BLS signatures](https://crypto.stanford.edu/~dabo/pubs/papers/BLSmultisig.html) enable us to store & check signatures `A, B` by only storing `C = A + B`
  - long-term: [zkSNARKs](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)

<br>

<v-click>

### Only 1 signature is stored for a **whole committee**

</v-click>

<!-- 
- one epoch's worth of signatures: `33.6 megabytes` ⇢ `7.6 gigabytes/day`
- using BLS signatures: `2 megabytes/day`
 -->

---

# <logos-ethereum-color /> What about bad actors? 🦹🏻‍♂️

<v-clicks>

- general assumption: committees represent the overall validator set (more or less 😅)
- we try to prevent malicious validators from ending up in the same committee by..
  * ensuring random committee assignments
  * requiring a minimum number of validators per committee
- it is quite unlikely for a bad actor to gain control over a committee
  - e.g. using 128 randomly sampled validator per committee leads to the probability of an attacker with $\frac{1}{3}$ of all validators getting a $>\frac{2}{3}$ committee of less than $2^{-40}$ [src](https://web.archive.org/web/20190504131341/https://vitalik.ca/files/Ithaca201807_Sharding.pdf)

</v-clicks>

<!-- 
- grundsätzliche Annahme: Stichprobe der validator repräsentiert Grundgesamtheit
- bad actors werden durch random assignment und minimum number davon abgehalten ins selbe committee zu kommen
- bei 128 validator/committee ist die Wahrscheinlichkeit, dass ein Angreifer mit 1/3 der validator ein committee mit mehr als 2/3 validator bekommt kleiner als $2^{-40}$
-->

---

# <logos-ethereum-color /> Sharding Roadmap
Ethereum 2.0
- **Phase 0:** POS [beacon chain](https://ethereum.org/en/upgrades/beacon-chain/) without shards (shipped in 2020 🚀)
  * beacon chain contains logic to secure and sync shards
  * also coordinates stakers in the network; assignment of shards 
- **Phase 1:** Basic sharding without EVM (planned for 2023 🗓)

<v-click>

- *Phase 2: EVM state transition function*
- *Phase 3: Light client state protocol*
- *Phase 4: Cross-shard transactions*
- *Phase 5: Tight coupling with main chain security*
- *Phase 6: Super-quadratic or exponential sharding* **Recursively, shards within shards within shards…**
- **Ethereum 3.0**

[learn more](https://eth.wiki/sharding/sharding-roadmap)

</v-click>

<!--
# Phase 1
- Blobs are collated in shards (w/o transactions)
- transactions need EVM

# Do shards need code execution?
3 options presented by vitalik
- state execution not needed
- have some execution shards
- wait for zkSNARKs and revisit the problem
-->


---

# <logos-ethereum-color /> Quick Recap

_i.g.: splitting a database horizontally_
- part of multi-phase upgrade to improve scalability and capacity
- for now shard chains provide _just_  storage layers - _you will learn how to use that in a clever way in a second_ 😏
- committees of random validators approve blocks
- validation results of several committees are combined in a way that only requires checking the signatures of all validators
  - attestation aggregation
  - BLS signatures / zkSNARKs
- **not only** a matter of **scaling** ⇢ improves security & decentralization of the network

<!-- 
- Teil eines mehrstufigen Upgrade-Plans
  - scalability & capacity
- momentan "nur" Speicher
- Validationsergebnisse mehrerer committees werden kombiniert
- nicht "NUR" scaling
-->

<br/>
<v-click>

### Any questions or comments?

</v-click>