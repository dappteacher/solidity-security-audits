# Smart Contract Audit — Simple Staking Contract

## Overview

This folder contains a security analysis and audit report for a real-world smart contract project:

* **Project:** simple-staking-contract
* **Source:** [https://github.com/RealJohnnyTime/simple-staking-contract](https://github.com/RealJohnnyTime/simple-staking-contract)
* **Contract Audited:** `contracts/Staking.sol`

The goal of this audit is to identify vulnerabilities, analyze design decisions, and suggest improvements for production readiness.

---

## Contents

* `report.md` → Full audit report with findings and recommendations
* `notes.md` → Personal analysis process and technical observations
* `scope.txt` → Defines the exact scope of the audit

---

## Audit Scope

This audit focuses on:

* Staking and reward distribution logic
* Token handling and ERC20 interactions
* Security vulnerabilities and edge cases
* Contract design and best practices

---

## Summary of Findings

The contract follows a standard reward accounting model but contains several issues:

* **High Severity**

  * Unsafe ERC20 usage
  * Incorrect handling of fee-on-transfer tokens
  * Insolvency risk when staking and reward tokens are the same

* **Medium Severity**

  * Payable `stake()` function (ETH can be locked)
  * Missing validations and events
  * Misleading signature verification logic

* **Low Severity**

  * No reentrancy guard
  * Minor precision loss in reward calculations

See `report.md` for full details.

---

## Disclaimer

This audit is for **educational and portfolio purposes only**.
It does not guarantee the security of the contract.

---

## Contact

If you are a project owner and would like a deeper audit or collaboration, feel free to reach out.

---
