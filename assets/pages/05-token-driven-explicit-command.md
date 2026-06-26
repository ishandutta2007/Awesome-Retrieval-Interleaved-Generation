# ⌨️ Token-Driven / Explicit Command RIG

> **First introduced:** 2023 | **Paper:** [Toolformer: Language Models Can Teach Themselves to Use Tools](https://arxiv.org/abs/2302.04761) — *Schick et al., 2023*

## Overview

Token-Driven / Explicit Command RIG represents the paradigm where language models are fine-tuned to use search as a native tool. The model directly emits specialized search primitives into its token stream, treating tool calls as first-class tokens in the generation vocabulary.

## Architecture Diagram

```mermaid
flowchart TB
    subgraph "📋 Training Phase"
        A[Tool-Use Demonstrations] --> B[Supervised Fine-Tuning]
        B --> C[Model Learns<br/>Search Tokens]
    end

    subgraph "⚡ Inference Phase"
        D[Input Prompt] --> E[Generate Tokens]
        E --> F{Search Token<br/>Emitted?}
        F -->|Yes: [SEARCH(query)]| G[Execute Search API]
        G --> H[Get Results]
        H --> I[Inject Results<br/>as Context]
        I --> E
        F -->|No| J[Continue Generation]
        J --> K{Generation<br/>Complete?}
        K -->|Yes| L[Final Output]
        K -->|No| E
    end

    style B fill:#e1f5fe,stroke:#0288d1
    style C fill:#f3e5f5,stroke:#7b1fa2
    style F fill:#fff3e0,stroke:#f57c00
    style G fill:#ffebee,stroke:#d32f2f
    style L fill:#e8f5e9,stroke:#388e3c
```

## How It Works

### 1️⃣ Supervised Fine-Tuning (SFT)
The model is trained on datasets where tool calls (e.g., `[SEARCH(query)]`, `[CALCULATOR(expr)]`) are interleaved naturally in the text. The model learns when and how to emit these tokens.

### 2️⃣ Search Token Generation
During inference, when the model encounters a factual claim or data point it needs to verify, it generates a search primitive like `[SEARCH("current stock price of AAPL")]`.

### 3️⃣ Tool Execution
An external executor intercepts these tokens, runs the actual tool call, and returns the results.

### 4️⃣ Context Injection
The tool results are appended to the context, and the model continues generation with the now-verified information.

## Key Innovations

| Innovation | Description |
|:-----------|:------------|
| 🎯 **Self-Supervised Learning** | Models learn tool use without human annotations (Toolformer). |
| 🔧 **Extensible** | New tools can be added by extending the token vocabulary. |
| 📝 **Natural Integration** | Tool calls feel native to the generation process. |
| 🔄 **Multi-Tool Support** | Models can use search, calculators, calendars, and more. |

## Implementations

| System | Year | Key Feature |
|:-------|:-----|:------------|
| **Toolformer** | 2023 | Self-supervised tool learning via API sampling |
| **Gorilla** | 2023 | API call generation for 1,600+ ML APIs |
| **GPT-4 Function Calling** | 2023 | Native tool-use API in production LLMs |
| **DataGemma RIG** | 2024 | Search-specific tool tokens for factual grounding |

## Limitations

- **Token budget** — tool call tokens consume context window space
- **Error handling** — failed tool calls need graceful fallback
- **Security** — uncontrolled tool access can lead to prompt injection

---

**[⬆ Back to README](../README.md)**
