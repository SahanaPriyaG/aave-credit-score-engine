# aave-credit-score-engine

This project provides a **credit score (0–1000)** for every wallet address that is interacting with the [Aave V2 protocol](https://aave.com) based on past transaction behavior. It applies DeFi level of transaction data (deposit, borrow, repay, etc.) to measure wallet responsibility and trust.

---

## Objective

To develop a solid and open ML-based scoring pipeline to:

- Identify **reliable** users (high scores)
- Identify **risky or bot-like** users (low scores)
- Ensure interpretability through legible feature logic and scoring measures

---

## Approach

### ✅ Features Engineered per Wallet:
- **Counts** of primary actions: `deposit`, `borrow`, `repay`, `redeemunderlying`, `liquidationcall`
- `total_txns`: Total transactions
- `unique_assets`: Assets interacted with uniquely
- `avg_amount`, `max_amount`: Average and maximum transaction amount
- **Ratios**:
  - `repay_to_borrow`
  - `redeem_to_deposit`
  - `liquidation_rate` = liquidations / total_txns

### Scoring Logic
- All the features are scaled to 0–1000 using `MinMaxScaler`.
- Final credit score = **mean of all scaled features**
- Larger values of `repay_to_borrow` and `redeem_to_deposit` show good behavior.
- Large `liquidation_rate` decreases the score.

---

##  Visuals

- Credit score distribution histogram
- Top 10 most trusty wallets
- Bottom 10 most risky wallets

---

## Features

- Unambiguous function-based scoring rules
- Seaborn-based score visualization
- CSV export for downstream processes

---

## Notes

- There is no usage of personal or KYC information—this is solely on-chain conduct scoring.
- This approach is transparent, extensible, and explainable.

---

