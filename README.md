# 🪙 Crypto Lakehouse Pipeline

An end-to-end data engineering pipeline that ingests live cryptocurrency data from the CoinGecko API and processes it through a Medallion Architecture (Bronze → Silver → Gold) built on Databricks.

---

## 🏗️ Architecture

![Data_architecture_crypto_1775384101257.png](./Data_architecture_crypto_1775384101257.png "Data_architecture_crypto_1775384101257.png")
---
## 🔄 Pipeline
>  ![pipeline_pic_1775381536784.png](./pipeline_pic_1775381536784.png "pipeline_pic_1775381536784.png")

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Databricks | Cloud data platform |
| PySpark | Data processing & transformations |
| Delta Lake | Storage format |
| SQL | Gold layer queries |
| CoinGecko API | Data source |

---

## 📁 Project Structure
```

crypto-lakehouse-pipeline/
├── README.md
├── LICENSE
├── data_sources/          ← API schema / sample responses
└── scripts/
├── bronze/
│   └── bronze_layer.py
├── silver/
│   └── silver_layer.py
└── gold/
├── gold_fact_crypto_market.py
├── gold_dim_coin.py
└── gold_dim_date.py
├── docs/
│   ├── data_architecture_crypto.png
│   ├── data_model_crypto.png
│   └── pipeline.png


```

---

## 🥉 Bronze Layer
- Ingests raw data from CoinGecko API
- Stores data as-is with no transformations
- No schema changes or cleaning

## 🥈 Silver Layer
- Drops unnecessary columns
- Casts and standardizes data types
- Handles nulls and removes duplicates
- Standardizes strings (uppercase, trim)
- Runs logical data validations
- Adds calculated columns (`price_vs_ath`, `volume_to_market_cap`, `circulating_supply_ratio`)
- Adds metadata columns (`ingestion_time`,`ingestion_date`, `batch_id`,`pipeline_run_id`,etc..)

## 🥇 Gold Layer
Three tables following a Star Schema:

| Table | Description |
|---|---|
| `fact_crypto_market` | Core metrics — price, market cap, volume, ratios |
| `dim_coin` | Coin descriptors — id, name, symbol, rank |
| `dim_date` | Date dimension — day, month, quarter, year,etc |

---

## 📊 Data Model

>  ![data_model_crypto_1775386890612.png](./data_model_crypto_1775386890612.png "data_model_crypto_1775386890612.png")

---

## 🚀 How to Run

1. Clone the repo
2. Set up a Databricks workspace
3. Import scripts into Databricks notebooks
4. Run in order:
   - `bronze_layer.py`
   - `silver_layer.py`
   - `gold_dim_coin.py`
   - `gold_dim_date.py`
   - `gold_fact_crypto_market.py`

---

## 📌 Notes
- CoinGecko free tier API is used (no key required)
- Pipeline is designed as a full snapshot refresh per run
- All tables stored as Delta format in Databricks Unity Catalog

---

## 👤 Author
**[Abd El-Rahman Elsebaey]**  

[https://www.linkedin.com/in/abd-el-rahman-elsebaey-5a7852297/] • [https://github.com/AbdelrahmanElsebaey]