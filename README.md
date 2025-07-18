# aave-credit-score-engine

This project assigns a **credit score (0–1000)** to each wallet address interacting with the [Aave V2 protocol](https://aave.com), based on historical transaction behavior. It uses DeFi transaction-level data (deposit, borrow, repay, etc.) to evaluate wallet trustworthiness and responsibility.

---

## 🚀 Objective

To build a robust and transparent ML-based scoring pipeline to:

- Detect **reliable** users (high scores)
- Detect **risky or bot-like** users (low scores)
- Provide interpretability using clear feature logic and scoring metrics

---

## 🧠 Approach

### ✅ Features Engineered per Wallet:
- **Counts** of key actions: `deposit`, `borrow`, `repay`, `redeemunderlying`, `liquidationcall`
- `total_txns`: Total number of transactions
- `unique_assets`: Number of unique assets interacted with
- `avg_amount`, `max_amount`: Mean and peak transaction amounts
- **Ratios**:
  - `repay_to_borrow`
  - `redeem_to_deposit`
  - `liquidation_rate` = liquidations / total_txns

### 📏 Scoring Logic
- All features are normalized using `MinMaxScaler` to the range 0–1000.
- Final credit score = **mean of all scaled features**
- Higher values of `repay_to_borrow` and `redeem_to_deposit` indicate responsible behavior.
- High `liquidation_rate` lowers the score.

---

## 🛠️ How to Run

1. **Upload `user-transactions.json`** to your Google Drive.
2. **Open `wallet_credit_score_colab.ipynb`** in Google Colab.
3. Run the notebook to:
   - Load data
   - Clean + preprocess
   - Generate scores using `score_wallet()` function
   - Visualize results
   - Export scores to CSV

---

## 📂 Output

| wallet_address | credit_score |
|----------------|--------------|
| 0xABC...123     | 930          |
| 0xDEF...456     | 120          |
| ...            | ...          |

---

## 📈 Visuals

- Histogram of credit score distribution
- Top 10 high-trust wallets
- Bottom 10 risky wallets

---

## ✨ Bonus Features

- Clear function-based scoring logic
- Score visualization via Seaborn
- Commented, professional-quality code
- CSV export for downstream tasks

---

## 🔒 Notes

- No personal or KYC data is used—this is purely on-chain behavior scoring.
- This solution is designed to be transparent, extensible, and interpretable.

---
