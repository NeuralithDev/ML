# FinSense — Data Notes

## Dataset Inventory

| Dataset | Size | Granularity | Role |
|---|---:|---|---|
| Financial | 1.3 MB | TBD | Behavioral/financial profile |
| IBM | 2.2 GB transactions | Transaction | TBD |
| PaySim | 471 MB | Transaction | Fraud benchmark |

## Important Engineering Decisions

### Raw data
Raw datasets are treated as immutable source data.

### Large datasets
PaySim and IBM transaction data will not be loaded entirely into memory.

They will be processed using chunked/streaming ingestion.

### Dataset integration
The datasets will not be blindly concatenated because they originate from different schemas/entities/data-generating processes.
