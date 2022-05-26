---
layout: image
image: ./img/sharding_eth.png
---

# 🏃🏻 Sharding


---

# 🏃🏻 Sharding
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
- network bandwith required is greater than the bandwith available to a single node

<!--
![illustrations](/img/horizontal_partitioning.png)
-->


---

commonly used: 

<img src="/img/sharding_implementations.png" class=" rounded" />

[Source](https://en.wikipedia.org/wiki/Shard_(database_architecture)#Implementations)


---

# 🏃🏻 Sharding through Random Sampling

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
# 🏃🏻 Quadratic Sharding
include?..


---

# 🏃🏻 Sharding Roadmap
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
# beacon chain
- contains logic for keeping shards secure and synced
- assigns stakers to shards they need to work on
- facilitates cross-shard communications

# Phase 1
- Blobs are collated in shards (w/o transactions)
- transactions need EVM
-->


---
# 🏃🏻 Quick Recap

content...