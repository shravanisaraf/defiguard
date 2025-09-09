# DeFiGuard 🛡️

**Final Year Engineering Project**
**Title:** Real-time Fraud Detection in DeFi (Ethereum) using Hybrid GNN + Federated Learning

-----

## 📖 Project Summary

DeFiGuard ingests historical Ethereum transaction data (from Kaggle) for model training and uses Alchemy WebSocket for a live transaction stream. We build features, create graph snapshots, train a hybrid **Graph Neural Network (GNN) + Transformer** classifier, and demonstrate **federated learning** using Flower. A FastAPI model server + Streamlit dashboard provide real-time inference and visualization.

-----

## 📂 Project Structure

```
defiguard/
├─ data/                 # datasets (raw parquet, kaggle, labels)
├─ realtime/             # realtime SQLite DB
├─ src/                  # code modules (ingestion, features, models, federated, serve, demo)
├─ notebooks/            # Jupyter exploration
├─ docs/                 # documentation and setup logs
```

-----

## ⚙️ Setup Instructions

### 1\. Clone repo

```bash
git clone git@github.com:shravanisaraf/defiguard.git
cd defiguard
```

### 2\. Create virtual environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3\. Install dependencies

```bash
pip install -r requirements.txt
```

### 4\. Environment variables

Copy `.env.example` to `.env` and fill in your keys:

```
ETH_ALCHEMY_WS=wss://eth-mainnet.g.alchemy.com/v2/YOUR_KEY
ETHERSCAN_API_KEY=YOUR_KEY
KAGGLE_KTX_PATH=data/raw/kaggle/transactions.csv
SQLITE_DB_PATH=realtime/realtime.db
LABELS_CSV=data/raw/labels.csv
```

### 5\. Test connection

```bash
python test_alchemy_ws.py
```

Expected output:

```
Connected: True
Latest block: 179xxxx
```

-----

## 👩‍💻 Contributors

  * **Shravani Saraf** — Data & Infra Lead
  * **Teammate B** — Models & ML Lead
  * **Teammate C** — Federated & Serving Lead

-----

## ✅ Day 1 Status

  * Repo structure initialized ✅
  * Env + Alchemy WS tested ✅
  * Kaggle dataset path prepared ✅
  * Labels stub committed ✅
  * Next: features & realtime ingestion (Day 2)
