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

# 🥜 [zkSNARKs in a nutshell](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)

- **S**uccinct
    * message sizes are really small in comparison to the actual computation
- **N**on-interactive
    * setup phase and single message from prover to verifier
    * anyone can verify without interacting anew
- **AR**guments
    * protection only against computationally limited provers
    * computational soundness vs. perfect soundness
- **K**nowledge
    * impossible for prover to construct a proof w/o a witness
    * e.g. address, path to Merkle-tree node,...

<!-- 
- ARguments: mit genug Rechenleistung kann jede public-Key Verschlüsselung gebrochen werden
- vgl. Quantum security der Hash-Funktion von STARKs

# Knowledge Stift Beispiel
- du bist farbenblind
- Zwei Stifte: rot - blau
- ich kann beweisen, dass ich einen Unterschied erkennen kann, wenn du sie hinter dem Rücken tauschst
- dafür **MUSS** ich wissen, welcher Stift welcher ist
-->

---

# 🥜 [zkSNARKs in a nutshell](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)

four main ingredients:

- encoding as polynomial problem
- succinctness by random sampling
- homomorphic encryption
- zero knowledge

---

# 🥜 [zkSNARKs in a nutshell](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)

<br/>
<br/>
<br/>

$$t(x) h(x)=w(x) v(x)$$

<br/>
<br/>
<br/>

## encoding as polynomial problem
- program/data is compiled into quadratic equation of polynomials
- equality only holds if the program is computed correctly
- a **prover** wants to convince the **verifier** that said equality holds

<!-- 
program wird in quadratische Gleichung kompiliert $t(x) h(x)=w(x) v(x)$
- Gleichheit gilt nur, wenn das Programm richtig berechnet wird
- *prover* will den *verifier* überzeugen, dass diese Gleichheit gilt
-->

---

# 🥜 [zkSNARKs in a nutshell](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)

<br/>
<br/>
<br/>

$$t(s) h(s)=w(s) v(s)$$

<br/>
<br/>
<br/>

## succinctness by random sampling
- verifier chooses a/multiple evaluation point $s$
- therefore simplifying the problem fromm polynomial multiplication to
    * simple multiplication
    * equality check on numbers

<!-- 
*verifier* wählt einen evaluation point und reduziert damit das Problem zu einfacher Multiplikation und Gleichheits check auf nummern $t(s) h(s)=w(s) v(s)$
- reduziert Beweis Größe und Zeit stark
- 3 Punkte auf elliptic curve
-->

---

# 🥜 [zkSNARKs in a nutshell](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)

<br/>
<br/>
<br/>

$$E$$

<br/>
<br/>
<br/>

## homomorphic encryption
- quasi homomorphic function $E$ is selected
- allows the **prover** to compute $E(t(s)), \ldots$ withouth knowing $s$
- only $E(s)$ and some other encrypted values are known

<!-- 
quasi homomorphische Funktion $E$ wird gewählt
- Homomorphismus bildet Elemente aus einer Menge in andere Menge ab, ohne ihre Bilder hinsichtlich der Struktur ihres Verhaltens (Operationen) zu verändern
- *prover* kann nun $E(t(s))$ berechnen ohne $s$ zu kennen
-->

---

# 🥜 [zkSNARKs in a nutshell](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)

<br/>
<br/>
<br/>

$$t(s) h(s) k=w(s) v(s) k$$

<br/>
<br/>

## zero knowledge
- **prover** permutes the encrypted values by multiplication with a number $k$
- **verifier** can check if their _stucture_ is correct even _**withouth knowing the encoded values**_

<br/>

#### Handwavy Idea 👋🏻
- checking $t(s) h(s)=w(s) v(s)$ is identical to checking $t(s) h(s) k=w(s) v(s) k$
- with one important _**difference**_:
    * checking $t(s) h(s) k=w(s) v(s) k$ only requires $t(s) h(s) k$ and $w(s) v(s) k$
    * it's impossible to derive $t(s) h(s)$ or $w(s) v(s)$

<!-- 
*prover* permutiert die verschlüsselten Werte mit einer Zahl
- damit kann *verifier* deren Struktur überprüfen ohne die verschlüsselten Werte zu kennen
- Grobe Idee: $t(s) h(s)=w(s) v(s)$ überprüfen ist identisch mit Überprüfen von $t(s) h(s) k=w(s) v(s) k$
- jedoch kann aus $t(s) h(s) k$,.. nicht $t(s) h(s)$ abgeleitet werden
-->

---

# [🔏 A simple zk-SNARK example](https://consensys.net/blog/developers/introduction-to-zk-snarks/)

A zk-SNARK consists of three algorithms

- key `G`enerator
    * takes secrect parameter `lambda` and program `C`
    * returns publicly available _proving key_ `pk` and _verification key_ `vk`
- `P`rover
    * takes `pk`, public input `x` and private witness `w`
    * returns a _proof_ `prf=P(pk, x, w)`
- `V`erifier
    * takes `vk`, `x` and `prf`
    * `V(vk, x, prf)` returns `true` if proof is correct; `false` otherwise
    
 `V` returns `true` if prover knows a witness  satisfying `C(x, w) == true`

<!-- 
# `G`
- keys müssen einmalig für gegebens `C` erstellt werden

# `P`
- prover kennt die witness
- witness hat was mit dem Programm zu tun; erinnert euch an die Stifte

# `lambda`
- jeder mit Wissen über lambda kann falsche Beweise erstellen
- Erstellung sehr wichtig
- Design Ritual für lambda von zCash in Quellen
-->

---

# [🔏 A simple zk-SNARK example](https://consensys.net/blog/developers/introduction-to-zk-snarks/)

premise: _Alice and Bob use a zkSNARK, since Alice wants to proof her knowledge about a secret value._

<br/>
<br/>

```js {1-3|5|6|7-9}
function C(x, w) {
    return ( sha256(w) == x );
}

(pk, vk) = G(C, lambda);
prf = P(pk, H, s);
result = V(vk, H, prf) ? 'Alice is a lier 🚫' : 'Alice knows the secret 🔓';

'Alice knows the secret 🔓'
```

<!-- 
- Bob erstellt den _proving key_ und den _verification key_ mit dem Generator
- Alice darf auf keinen Fall lamda erfahren
- Alice erstellt einen Beweis mit dem proof Algorithmus
    * sie will beweisen, dass sie den Wert $s$ kennt, der gehashed $H$ ergibt
- Alice zeigt Bob den Beweis
    * er verifiziert den Beweis mit `V`
- Alice war ehrlich und konnte Bob beweisen, dass sie $s$ kennt, ohne ihm $s$ zu sagen

_vergebt mir für die letzte Zeile: offensichtlich kein gültiges JS_
-->

---

# 👨🏻‍🏫 zkSNARK recap

- based on elliptic curves
- enables **verifiers** to check knowledge of **prover** without the need to reveal the secret
    * $t(x) h(x)=w(x) v(x)$
    * $t(s) h(s)=w(s) v(s)$
    * $E(t(s)), \ldots$
    * checking $t(s) h(s)=w(s) v(s)$ is identical to checking $t(s) h(s) k=w(s) v(s) k$
- currently on the roadmap to be utilized by Ethereum
- there are alternatives and plenty of different implementations (STARKs, PLONK,...)

<!--
- Verschlüsselung als quadratische Gleichung
- evaluation points und damit einfache Multiplikation
- quasi Homomorphismus und damit $E(t(s))$ berechnen ohne $s$ zu kennen
- zufälliges $k$ erlaubt Überprüfung ohne die Möglichkeit "den wahren Wert" zu ermitteln
-->

---

# Rollups: ✨ Optimistic vs. zk ⛓

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