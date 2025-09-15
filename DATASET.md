# Ethereum Fraud Detection – Multiclass Dataset Extension

## Overview
The original Kaggle Ethereum Fraud Detection dataset contained binary labels (`FLAG` = 0 or 1).  
We extended this into **multiclass fraud categories** using a combination of **heuristic rules, clustering, and selective on-chain inspection (Alchemy API)**.  

This dataset (`labels_final_patched_autolabeled.csv`) contains **2,179 fraud addresses** labeled into one of five categories:

- **Phishing** – Collector scams that drain many victims.  
- **Ponzi / Pyramid** – Steady inflows and outflows resembling high-yield schemes.  
- **Rug Pull / Exit Scam** – Deployed contracts with sudden value drain.  
- **Wash Trading** – Repetitive trading within a small circle of addresses/tokens.  
- **Mixers** – High-volume relays for obfuscation of funds.  

---

## Fraud Taxonomy & Heuristic Rules

### 1. Phishing
- **Pattern:** Many unique senders, very few outgoing txns.  
- **Heuristic:** `Unique Received From Addresses >= 30` and `Sent tnx small`.  
- **Cluster Hint:** Often in cluster 1.  

### 2. Ponzi / Pyramid
- **Pattern:** Steady inflows + payouts over long lifetime.  
- **Heuristic:** `Received Tnx high`, `Sent tnx present`, `Time Diff long`.  
- **Cluster Hint:** Often in cluster 2.  

### 3. Rug Pull / Exit Scam
- **Pattern:** Deploy contract → pump → massive outflow.  
- **Heuristic:** `Number of Created Contracts >= 1` and `ERC20 max val sent contract > 1e5`.  
- **Cluster Hint:** Often in cluster 0.  

### 4. Wash Trading
- **Pattern:** Very high tx count but very few counterparties.  
- **Heuristic:** `ERC20 uniq sent token name <= 3` and `tx_count >= 100`.  
- **Cluster Hint:** Small outliers in cluster 1 or -1.  

### 5. Mixers
- **Pattern:** Many senders + many receivers, very short gaps.  
- **Heuristic:** `(Sent + Received) > 100` and `Avg min between sent tnx < 60`.  
- **Cluster Hint:** Often in cluster -1.  

---

## Methodology

1. **Heuristic Rules** – Applied rules above to seed high-confidence labels.  
2. **Clustering** – Used HDBSCAN on scaled features to find groups consistent with rug pulls, ponzis, etc.  
3. **Alchemy Enrichment (Optional)** – For ambiguous cases, we inspected a subset of transaction traces (contract creation followed by drains, sudden inflows, etc.).  
4. **Auto-Labeling** – Propagated rules to unlabeled fraud rows for coverage.  

---

## Dataset Files

- `labels_final_patched_autolabeled.csv` → All 2,179 fraud addresses with final multiclass label.  
- `labels_final.csv` → Skeleton dataset (before propagation).  
- `to_review_for_alchemy_auto.csv` → Subset of 30 manually/auto-reviewed addresses with notes & confidence.  

---

## Novelty
- Extended binary fraud → multiclass fraud taxonomy.  
- Rule + cluster + optional Alchemy enrichment pipeline.  
- Provides **fraud-type labels**, which are rarely available in Ethereum datasets.  

---

## Notes
- This dataset is not perfect — some labels are auto-assigned with heuristics.  
- For research, this is sufficient to train and evaluate multiclass GNNs.  
