# 💰 Autonomous Financial Portfolio & Equity Audit Workflows

> **First introduced:** 2026 | **Paper:** [Point-in-Time Financial RAG with Frozen LLMs and Market-Feedback Adaptive Retrieval](https://arxiv.org/abs/2605.31201) — *Zhao & Welsch, MIT 2026*

## Overview

Autonomous Financial Portfolio workflows track volatile market updates. As a financial analyst model calculates quarterly asset risk summaries, the RIG engine dynamically looks up changing stock ticker prices and SEC filing forms, interleaving exact, real-time fiscal metrics into the sentence text.

## Architecture Diagram

```mermaid
flowchart TB
    subgraph "📊 Data Sources"
        A1[SEC EDGAR Filings]
        A2[Yahoo Finance API]
        A3[Bloomberg Terminal]
        A4[Market News Feeds]
    end

    subgraph "🔄 RIG Pipeline"
        B1[User Query:<br/>"Calculate Q3 Risk"] --> B2[Generate Risk Summary]
        B2 --> B3{Stock Data<br/>Needed?}
        B3 -->|Yes| B4[SEARCH: Ticker Prices]
        B4 --> B5[Retrieve Real-Time Prices]
        B5 --> B6[Interleave into Text]
        B6 --> B3
        B3 -->|No| B7[Final Audit Report]
    end

    subgraph "🛡️ Point-in-Time Verification"
        C1[Timestamp All Retrieved Data]
        C2[Prevent Data Leakage]
        C3[Market-Feedback Adaptation]
    end

    A1 --> B5
    A2 --> B5
    A3 --> B5
    A4 --> B5

    style B4 fill:#e1f5fe,stroke:#0288d1
    style B5 fill:#fff3e0,stroke:#f57c00
    style B6 fill:#f3e5f5,stroke:#7b1fa2
    style B7 fill:#e8f5e9,stroke:#388e3c
    style C1 fill:#ffebee,stroke:#d32f2f
    style C2 fill:#ffebee,stroke:#d32f2f
    style C3 fill:#ffebee,stroke:#d32f2f
```

## How It Works

### 1️⃣ Multi-Source Data Integration
The system connects to multiple financial data sources:
- **SEC EDGAR** — for official filings (10-K, 10-Q, 8-K)
- **Real-Time Market APIs** — for current prices and trading volumes
- **News Feeds** — for breaking market-moving events

### 2️⃣ Dynamic Risk Assessment
As the model generates a portfolio risk summary, it identifies points where current data is needed (e.g., "Current P/E ratio", "YTD return") and triggers targeted retrievals.

### 3️⃣ Point-in-Time Verification
A critical feature that ensures all retrieved data is timestamped to prevent lookahead bias in historical analysis. The system only accesses information available at the time being analyzed.

### 4️⃣ Market-Feedback Adaptation
Bayesian source memory tracks which data sources are most predictive, learning from realized market returns to optimize future retrieval strategies.

## Key Features

| Feature | Description |
|:--------|:------------|
| 🔄 **Real-Time Data** | Stock prices, currency rates, and market indices |
| 📋 **SEC Filing Analysis** | Automated extraction from 10-K, 10-Q, proxy statements |
| 🛡️ **Anti-Data Leakage** | Point-in-time verification prevents lookahead bias |
| 🧠 **Adaptive Retrieval** | Learns which sources provide the most useful information |
| 📊 **Structured Output** | Generates formatted tables and comparison matrices |

## Example Workflow

```
Query: "Compare the Q3 performance of AAPL and MSFT"

1. Generate opening paragraph
2. → SEARCH: AAPL Q3 2024 revenue
3. → Retrieve: $89.5B (+6% YoY)
4. → Interleave: "Apple reported Q3 revenue of $89.5 billion..."
5. → SEARCH: MSFT Q3 2024 revenue
6. → Retrieve: $56.2B (+13% YoY)
7. → Interleave: "...while Microsoft achieved $56.2 billion..."
8. → SEARCH: Current P/E ratios for both
9. → Interleave ratios into valuation comparison
10. Final: Comprehensive audit report with all metrics
```

---

**[⬆ Back to README](../README.md)**
