## 🏗️ System Architecture

FinSense is designed as an AI-powered Personal Finance Intelligence
system that transforms heterogeneous financial data into personalized
financial insights, forecasts, recommendations, and AI-assisted
decision making.

```text
                              ┌──────────────────────────┐
                              │         FinSense         │
                              │   AI Personal Finance    │
                              │      Intelligence        │
                              └────────────┬─────────────┘
                                           │
                    ┌──────────────────────┼──────────────────────┐
                    │                      │                      │
                    ▼                      ▼                      ▼
          ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
          │    Financial    │    │   Behavioral    │    │   Transaction   │
          │     Profile     │    │  Intelligence  │    │  Intelligence   │
          ├─────────────────┤    ├─────────────────┤    ├─────────────────┤
          │ • Income        │    │ • Spending      │    │ • Transactions  │
          │ • Expenses      │    │   patterns      │    │ • Amounts       │
          │ • Savings       │    │ • Frequency     │    │ • Types         │
          │ • Debt          │    │ • Categories    │    │ • Balance flow  │
          │ • EMI           │    │ • Merchants     │    │ • Time patterns │
          │ • Credit Score  │    │ • Trends        │    │ • Activity      │
          └────────┬────────┘    └────────┬────────┘    └────────┬────────┘
                   │                      │                      │
                   └──────────────────────┼──────────────────────┘
                                          ▼
                              ┌──────────────────────────┐
                              │     Financial State      │
                              │                          │
                              │ Unified representation  │
                              │ of the user's financial  │
                              │ condition and behavior   │
                              └────────────┬─────────────┘
                                           │
                         ┌─────────────────┴─────────────────┐
                         │                                   │
                         ▼                                   ▼
              ┌──────────────────────┐             ┌──────────────────────┐
              │     Forecasting      │             │   Recommendations    │
              ├──────────────────────┤             ├──────────────────────┤
              │ • Spending forecast │             │ • Savings actions    │
              │ • Cash-flow forecast│             │ • Budget suggestions │
              │ • Financial trends  │             │ • Debt strategies    │
              │ • Future scenarios  │             │ • Personalized goals │
              └──────────┬───────────┘             └──────────┬───────────┘
                         │                                    │
                         └────────────────┬───────────────────┘
                                          ▼
                              ┌──────────────────────────┐
                              │      AI Assistant        │
                              ├──────────────────────────┤
                              │ • Financial Q&A          │
                              │ • Explain insights       │
                              │ • Explain predictions    │
                              │ • Scenario reasoning     │
                              │ • Personalized guidance  │
                              └────────────┬─────────────┘
                                           │
                                           ▼
                              ┌──────────────────────────┐
                              │     FinSense User        │
                              │                          │
                              │ Understand → Predict →   │
                              │ Decide → Act             │
                              └──────────────────────────┘


Raw Financial Data
        ↓
Data Validation & Cleaning
        ↓
Feature Engineering
        ↓
┌───────────────────────────────────────────┐
│                                           │
│  Financial Profile                        │
│  Behavioral Intelligence                  │
│  Transaction Intelligence                 │
│                                           │
└───────────────────┬───────────────────────┘
                    ↓
             Financial State
                    ↓
       ┌────────────┴────────────┐
       ↓                         ↓
  Forecasting              Recommendations
       │                         │
       └────────────┬────────────┘
                    ↓
              AI Assistant
                    ↓
           Personalized Action
# FinSense — Data Notes

## Dataset Inventory

| Dataset | Size | Granularity | Current Role |
|---|---:|---|---|
| Financial | 1.3 MB | Synthetic merged financial records | Financial/user behavior |
| IBM | 2.2 GB transactions | Transaction | Transactional behavior + fraud |
| PaySim | 471 MB | Transaction | Fraud detection |

## Data Quality

### Financial
- Missing values: 0
- Synthetic merged dataset

### PaySim
- Transaction-level data
- Target: `isFraud`
- Existing rule-based indicator: `isFlaggedFraud`

### IBM
- Transaction-level data
- Contains user/card information
- Contains fraud-related information

## Ingestion Strategy

Small datasets can be loaded directly.

Large transaction datasets will be processed incrementally rather than loaded entirely into memory.

Raw datasets are treated as immutable source data.

### Large datasets
PaySim and IBM transaction data will not be loaded entirely into memory.

They will be processed using chunked/streaming ingestion.

### Dataset integration
The datasets will not be blindly concatenated because they originate from different schemas/entities/data-generating processes.

The Financial dataset is a synthetically merged dataset.

Therefore:
- It can be used for experimentation and feature engineering.
- Relationships between variables should not automatically be interpreted as real-world relationships.
- We need to inspect its construction and schema before deciding which features are suitable for modeling.
- We should avoid making unsupported claims about real-world financial behavior based solely on this dataset.
