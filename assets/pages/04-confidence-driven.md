# 📊 Confidence-Driven Interleaved Generation

> **First introduced:** 2023 | **Paper:** [Active Retrieval Augmented Generation (FLARE)](https://arxiv.org/abs/2305.06983) — *Jiang et al., EMNLP 2023*

## Overview

Confidence-Driven Interleaved Generation continuously monitors the model's internal token output log-probabilities (perplexities) during sampling. When generation confidence dips below a target boundary, it triggers a localized vector lookup to correct facts in real-time.

## Architecture Diagram

```mermaid
flowchart TB
    A[Start Generation] --> B[Sample Next Token]
    B --> C[Compute Log-Probability]
    C --> D[Store in Sliding Window]
    D --> E{Window Avg. Confidence<br/>> Threshold?}
    E -->|Yes - Confident| B
    E -->|No - Uncertain| F[Pause Generation]
    F --> G[Generate Search Query<br/>from Recent Context]
    G --> H[Retrieve Relevant Documents]
    H --> I[Re-rank & Filter Context]
    I --> J[Resume Generation<br/>with Augmented Context]
    J --> B

    subgraph "📈 Confidence Metrics"
        K[Token-Level Logits]
        L[Sentence-Level Perplexity]
        M[Entropy Score]
    end

    style E fill:#fff3e0,stroke:#f57c00
    style F fill:#ffebee,stroke:#d32f2f
    style G fill:#e1f5fe,stroke:#0288d1
    style H fill:#f3e5f5,stroke:#7b1fa2
    style J fill:#e8f5e9,stroke:#388e3c
```

## How It Works

### 1️⃣ Token Generation Monitoring
The system tracks the log-probability of each generated token. A sliding window (typically 5–10 tokens) maintains a running average of token confidence.

### 2️⃣ Uncertainty Detection
When the average confidence drops below a threshold (e.g., *p* < 0.35), the system infers that the model is operating outside its knowledge boundary.

### 3️⃣ Query Construction
The recently generated low-confidence tokens are used to formulate a targeted search query for the vector database.

### 4️⃣ Localized Retrieval
Only the most relevant document chunks are retrieved, minimizing context pollution.

### 5️⃣ Fact Verification
The sentence is re-generated with the retrieved context, ensuring that the final output is factually grounded.

## Key Advantages

- 🎯 **Selective retrieval** — only triggers when necessary, reducing overhead
- 📉 **Reduced hallucination** — catches factual errors as they occur
- 🔄 **Adaptable** — naturally handles multi-hop reasoning
- 📊 **Quantifiable** — confidence thresholds can be tuned per use case

## Challenges

- 🔧 **Threshold tuning** — optimal thresholds vary by domain and model
- 🐌 **Generation pauses** — each retrieval step adds latency
- 📝 **Query quality** — depends on the model's ability to formulate good search queries

---

**[⬆ Back to README](../README.md)**
