# MultipliVault Security Audit

This repository contains a professional security analysis of the **MultipliVault** smart contract system.

## Target

- Repo: https://github.com/multipli-libs/Barebones-MultipliVault
- Contract: `src/vault/MultipliVault.sol`
- Version: v2

## Scope

The audit focuses on:
- Core vault logic (ERC4626-based)
- Redemption flow (async + flash redeem)
- Fee mechanisms
- Oracle-based accounting
- Admin privileges and trust assumptions

## Methodology

This audit was conducted using:

- Manual code review
- Threat modeling
- ERC4626 invariant analysis
- Adversarial thinking (attacker mindset)
- Code4rena-style reporting

## Summary of Findings

| Severity | Count |
|--------|--------|
| Critical | 2 |
| High     | 3 |
| Medium   | 3 |
| Low      | 1 |

## Key Risks

- Oracle manipulation affecting share pricing
- Admin minting leading to full fund drain
- Centralized control over funds and execution
- Accounting inconsistencies between reported and actual assets

## Files

- `report.md` → Full audit findings
- `notes.md` → Raw audit notes and thought process
- `scope.txt` → Defined audit scope

## Disclaimer

This audit is for educational and portfolio purposes.  
It does **not** guarantee the absence of vulnerabilities.

---

## Author

**Yaghoub Adelzadeh**  
Smart Contract Security Researcher

- GitHub: https://github.com/dappteacher
```

