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

includes an easily verifiable cryptographic **valididty** proof in every *batch*.

- enable a party to prove knowledge about something while having **z**ero **k**nowledge about "the something"
- rollups only inlcude validity proof
- faster finality
- currently there are two approaches to zk proofs


<!-- 
- nur validity proof: optimistic rollups brauchen die Transaktionsdaten um ggf. einen fraud proof zu überprüfen
- finality: state direkt verifiziert, wenn der Rollup bei der main chain ankommt
- "Bewiesen ist es ja schon"
-->

---

# ⛓ zk Rollups

### **S**calable **T**ransparent **A**rgument of **K**nowledge ⇢ **STARKs**
- rely on hash functions ⇢ quantum resistant
- don't require trusted set-up
- larger proof size requires
    * more time to verify
    * higher gas fees (up to 24\%)

<br/>

### **S**uccinct **N**on-interactive **A**rgument of **K**nowledge ⇢ **SNARKs**

- based on [elliptic curves](https://curves.ulfheim.net/)
- currently the main approach of Ethereum using the [PLONK](https://vitalik.ca/general/2019/09/22/plonk.html) protocol
- better developer support among other benefits

[_read more about the differences & advantages_](https://consensys.net/blog/blockchain-explained/zero-knowledge-proofs-starks-vs-snarks/)


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