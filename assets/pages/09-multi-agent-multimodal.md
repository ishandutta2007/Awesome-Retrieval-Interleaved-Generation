# 🎨 Multi-Agent Multimodal Interleaved Generation (RAG-IG)

> **First introduced:** 2025 | **Paper:** [RAG-IGBench: Innovative Evaluation for RAG-based Interleaved Generation](https://arxiv.org/abs/2512.05119) — *Zhang et al., NeurIPS 2025*

## Overview

Multi-Agent Multimodal Interleaved Generation (RAG-IG) blends text generation with visual asset injection. The model outputs markdown text containing dynamic placeholders, interleaving real-time asset retrieval queries concurrently to output structurally cohesive multimedia documents.

## Architecture Diagram

```mermaid
flowchart TB
    A[User Query<br/>"Describe Renaissance Art"] --> B[Query Router]

    subgraph "🤖 Multi-Agent System"
        B --> C[Text Agent]
        B --> D[Image Retrieval Agent]
        B --> E[Layout Agent]
    end

    subgraph "📝 Generation Pipeline"
        C --> F[Generate Text with<br/>Placeholder Tokens]
        D --> G[Retrieve Relevant<br/>Images from Database]
        E --> H[Generate Layout Structure]

        F --> I[Assembly Module]
        G --> I
        H --> I

        I --> J[Interleaved Output]
    end

    J --> K[Final Document]

    subgraph "📄 Output Example"
        L["The Renaissance began in Florence...<br/><br/>![Mona Lisa](IMG#1)<br/><br/>Key artists included Leonardo da Vinci...<br/><br/>![The Last Supper](IMG#2)"]
    end

    style C fill:#e1f5fe,stroke:#0288d1
    style D fill:#f3e5f5,stroke:#7b1fa2
    style E fill:#fff3e0,stroke:#f57c00
    style I fill:#e8f5e9,stroke:#388e3c
    style L fill:#ffebee,stroke:#d32f2f
```

## How It Works

### 1️⃣ Multi-Agent Orchestration
Multiple specialized agents work in parallel:
- **Text Agent** — generates coherent narrative text
- **Image Retrieval Agent** — searches for relevant visual assets
- **Layout Agent** — determines optimal placement of visual elements

### 2️⃣ Placeholder-Based Generation
The text agent inserts dynamic placeholders (e.g., `![image description](IMG#k)`) at points where visual context would enhance understanding.

### 3️⃣ Concurrent Asset Retrieval
While the text is being generated, the image retrieval agent independently fetches relevant visual assets from external databases.

### 4️⃣ Assembly
An assembly module replaces placeholders with actual retrieved images, creating a cohesive interleaved document.

## RAG-IGBench Evaluation

The RAG-IGBench benchmark evaluates interleaved generation quality across three dimensions:

| Metric | Description |
|:-------|:------------|
| 📝 **Textual Quality** | Evaluated via ROUGE scores against reference texts |
| 🖼️ **Image Quality** | Assessed through sequential arrangement and edit distance |
| 🔗 **Image-Text Coherence** | Measured using CLIP-scores and semantic alignment |

## Applications

| Application | Description |
|:------------|:------------|
| 📰 **Automated Report Generation** | Financial reports with embedded charts and graphs |
| 📚 **Educational Content** | Textbooks with contextually relevant illustrations |
| 🛒 **E-Commerce** | Product descriptions with dynamically selected images |
| 📊 **Data Storytelling** | Narrative analysis with supporting data visualizations |

## Challenges

- **Placeholder placement** — determining the optimal position for visual elements
- **Cross-modal coherence** — ensuring text and images tell a consistent story
- **Retrieval quality** — finding images that genuinely enhance understanding

---

**[⬆ Back to README](../README.md)**
