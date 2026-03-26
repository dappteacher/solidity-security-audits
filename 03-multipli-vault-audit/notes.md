# Audit Notes — MultipliVault

## Initial Observations

- ERC4626-based vault with heavy customization
- Async redemption model → non-standard
- Oracle-based accounting → major red flag
- Strong admin control via AuthUpgradeable

---

## High-Risk Areas Identified Early

### 1. totalAssets Override

```solidity
return balanceOf(this) + aggregatedUnderlyingBalances;
````

Problem:

* Half real, half reported
* Trust assumption on external update

→ Likely critical vulnerability

---

### 2. onUnderlyingBalanceUpdate()

* No validation
* No bounds check
* Only requiresAuth

→ Oracle manipulation vector

---

### 3. adminMint / adminBurn

Immediate red flags:

```solidity
_mint(receiver, shares);
_burn(owner, shares);
```

→ breaks ERC4626 invariant

---

### 4. manage()

```solidity
target.functionCallWithValue(...)
```

→ arbitrary execution layer

Risk depends entirely on Authority

---

## Redemption Flow Analysis

### requestRedeem()

* Transfers shares to vault
* Stores pending state

### fulfillRedeem()

* Operator-controlled
* No user fallback

Funds can be locked indefinitely

---

## FlashRedeem Analysis

Flow:

1. Send assets first
2. External callback
3. Expect shares back
4. Burn shares

Good:

* ReentrancyGuard used
* Balance checks present

Still trust-heavy

---

## Key Invariant Violations

### ERC4626 Broken Assumptions

* Shares can be minted without assets
* Assets can be misreported
* Redemption is asynchronous

---

## Attack Ideas Considered

* Oracle inflation → deposit exploit
* Admin mint → drain vault
* Accounting mismatch → insolvency
* Redemption griefing

---

## Final Impression

This is a **highly flexible but highly trust-dependent system**.

Security depends more on:

* off-chain actors
* governance
* correct configuration

than on pure smart contract safety.

## What Makes This Interesting

* Real-world DeFi pattern (cross-chain / async vaults)
* Hybrid accounting model
* Operator-driven execution

→ Good example of **"design risk vs code risk"**

````
