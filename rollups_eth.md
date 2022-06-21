---
layout: image
image: ./img/sharding_eth.png
---

# 🏃🏻 Rollups


---
layout: two-cols
---
# 🏃🏻 Rollups

perform transactions on layer 2 and post data to layer 1 once settled.

<br/>
<br/>
<br/>
<br/>

<v-click>

## There are two distinctly different types of rollups:

- optimistic ✨
- zero-knowledge ⛓

</v-click>

::right::

<div class="container mx-auto flex flex-row justify-center bg-white">
    <img src="/img/rollup_schematic.png" class="m-3 h-40 rounded"/>
</div>

### How does it work?
- on-chain smart contract maintains **state root**: *merkle root* of the rollup state
- anyone can publish a transaction **batch**
    * transactions highly compressed
    * _**previous**_ state root
    * _**next**_ state root

<!-- 
# optimistic
- verlässt sich auf game theory
- Annahme: Transaktionen sind Korrekt
- Nachrechnen **nur**, wenn sich jemand beschwert

# zero-knowledge
- kryptografische Beweise über die Korrektheit der Transaktionen werden erstellt
- zero-knowledge succinct non-interactive argument
- Nachweis über Informationen ohne die Informationen zu kennen
 -->

---

# ✨ Optimistic Rollups

- sequencer certifies that computing `C` with input `X` leads to output `Y` ⇢ _"the transactions I validated are correct"_
    * provides a bond
- **any** other party (**challenger**) can submit a **fraud proof** during a *dispute period* 🚨
    * a bond also needs to be provided
    * gas is paid for with bond of the other party when correct
- suspicious transaction is executed by all nodes on the Ethereum chain 👮🏻‍♂️
- the loosing party's bond is slashed
- if no one submits a **fraud proof** transactions are considered final after the *dispute period* is over


<!-- 
- basiert auf Unschuldsvermutung
- hier sieht man den game-theory Ansatz
    * spam von fraud proofs ist teuer
    * submitten falscher transaction batches ebenfalls
- slashing bedeutet, der bond wird geteilt
-->

---
layout: statement
---
# 🤔 Why does the bond get slashed?

Instead of paying out the full amount to the challenger?

<!-- 
- Frage zur Verdeutlichung des Spieltheoretischen Ansatzes
- bad actor könnte den Disput seiner eigenen batch frontrunnen
- damit "gratis" Betrugsversuche starten
- nur eine der vielen Variablen die bei optimistic rollups spielttheoretisch berücksichtigt werden müssen
-->

---

# ⛓ zk Rollups


---

# ✨ Optimistic vs. zk ⛓

| **Property** | **Optimistic Rollups** | **zk Rollups** |
|---|---|---|
| Gas cost per batch | **~40,000** | ~500,000  |
| Withdrawal period | ~1 week | next batch ⇢ **very fast** |
| Complexity | **low** | high |
| Generalizability | **easier** | harder |
| Per-transaction gas cost on chain | higher | **lower** |
| Off-chain computation cost | **lower** | higher |

[Source](https://vitalik.ca/general/2021/01/05/rollup.html)

<!-- 
# Gas cost per batch
- optimistic: eigentlich nur aktualisieren von state root on-chain
- zk: komplizierte Berechnungen

# Withdrawal period
- optimistic: die *dispute period* muss berücksichtigt werden
    * abhängig von Spezifikation
    * generell 1 Woche

# Complexity
- zk: mathematisch komplex

# Generalizability
- optimistic: nahe an Ethereum daher einfach
- zk: general purpose EVM execution ist sehr schwierig zu beweisen
    * Cairo ist eine Sprache die production-grade Turing-Vollständige STARKs ermöglich

# Per-transaction gas cost on chain
- zk: Transaction data nur zur Verifikation notwendig, kann daher weggelassen werden
- optimistic: benötigt transaction data, falls ein *fraud proof* überprüft werden muss

# Off-chain computation cost
- zk: Berechnung besonders für general-purpose teuer: bis zu 1000x gegenüber der tatsächlichen Berechnung
-->