---
layout: image
image: ./img/sharding_eth.png
---

# <logos-ethereum-color /> Sharding


---

# <logos-ethereum-color /> Sharding
- related to horizontal data partition
- shared-nothing architecture
	* shards are autonomous
  * memory & storage is not shared between nodes 
- adds complexity & potential failure points ⚠️


<br>
<br>
<br>


### When to shard ? 🧐

- application data outgrows capacity of single database node
- slowed response times due to volume of read/writes to single node
- network bandwidth required is greater than the bandwidth available to a single node

<!--
![illustrations](/img/horizontal_partitioning.png)
-->


---

commonly used: 

<img src="/img/sharding_implementations.png" class=" rounded" />

[Source](https://en.wikipedia.org/wiki/Shard_(database_architecture)#Implementations)


---

# <logos-ethereum-color /> Sharding through Random Sampling

<br>
<div class="container mx-auto flex flex-row justify-center">
  <img src="/img/sharding_committees.png" class="bg-white p-2 rounded" />
</div>
<br>

- randomly split verification work
- shuffle validator list and assign **committees** of size n to verify a block
- each validator publishes a signature upon block validation
- the network **only needs to verify the signatures** - less work

---

# <logos-ethereum-color /> Sharding Consensus

### Important concepts
- beacon chain
- **slot:** 12 second time-frame in which a block is expected to be added to the chain
- **epoch:** comprised of 32 slots
- **attestation** consisting of
  * validator index
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
 -->

---
layout: statement
---

# How can we use the properties of attestations within a committee in a clever way?

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

### Only 1 signature is stored for a **whole committee**

<!-- 
- one epoch's worth of signatures: `33.6 megabytes` ⇢ `7.6 gigabytes/day`
- using BLS signatures: `2 megabytes/day`
 -->

---

# <logos-ethereum-color /> What about bad actors? 🦹🏻‍♂️

- general assumption: committees represent the overall validator set (more or less 😅)
- we try to prevent malicious validators from ending up in the same committee by..
  * ensuring random committee assignments
  * requiring a minimum number of validators per committee
- it is quite unlikely for a bad actor to gain control over a committee
  - e.g. using 128 randomly sampled validator per committee leads to the probability of an attacker with $\frac{1}{3}$ of all validators getting a $>\frac{2}{3}$ committee of less than $2^{-40}$ [src](https://web.archive.org/web/20190504131341/https://vitalik.ca/files/Ithaca201807_Sharding.pdf)

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
- part multi-phase upgrade to improve scalability and capacity
- for now shard chains provide _just_  storage layers - _you will learn how to use that in a clever way in a second_ 😏
- committees of random validators approve blocks
- validation results of several committees are combined in a way that only requires checking the signatures of all validators
  - attestation aggregation
  - BLS signatures / zkSNARKs
- **not only** a matter of **scaling** ⇢ improves security & decentralization of the network

<v-click>

### Any questions or comments?

</v-click>