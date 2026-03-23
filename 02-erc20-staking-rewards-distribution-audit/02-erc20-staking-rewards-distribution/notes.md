# Audit Notes (Raw)

## General Observations

* Uses clone (proxy) pattern via OpenZeppelin Clones
* Multi-reward token mechanism
* Time-based reward distribution

---

## Initial Concerns

### 1. Solidity Version

* Uses fixed pragma:
  pragma solidity 0.8.12;

* Not flexible for newer compiler fixes

* Not a vulnerability but not ideal

---

### 2. Ownable + Clones Issue

* Factory deploys clones using `Clones.clone`
* Constructors are NOT executed in clones

Risk:

* Owner may not be initialized properly
* Must be set inside `initialize()`

---

### 3. Initialization Flow

* Tokens transferred before initialize
* Potential front-running risk

---

### 4. Reentrancy

* Claim / Withdraw functions:

  * Follow Checks-Effects-Interactions pattern

However:

* No `ReentrancyGuard`
* External token calls still risky
* Multiple reward tokens loop increases attack surface

---

### 5. Input Validation

* Factory may not validate:

  * reward tokens length vs amounts
  * zero address
  * duplicate tokens

---

### 6. Token Risk

* Accepts arbitrary ERC20 tokens

Potential issues:

* Fee-on-transfer tokens
* ERC777 reentrancy hooks
* Rebasing tokens

---

### 7. Gas Concerns

* Loops over reward tokens
* Could become expensive

---

## 🧠 Key Insight

Biggest architectural risk:
Initialization + ownership in clone contracts

Not:

* Solidity version
* Not only reentrancy

---

##  To Verify Further

* Exact order of state updates vs transfers
* Initialization modifier usage
* Ownership assignment
* Reward calculation precision
