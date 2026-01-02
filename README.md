# Project JARVIS: Air-Gapped Compliance Verification System (F1 2026)

> **Status:** OPERATIONAL
> **Architecture:** Local RAG (Retrieval-Augmented Generation)
> **Clearance Level:** UNCLASSIFIED // PORTFOLIO DEMONSTRATION

## 🎯 Mission Profile
To engineer a secure, air-gapped **Automated Verification System** capable of auditing **Formula 1 2026 Technical Regulations** without external data exfiltration. This project demonstrates the "Systems-First" methodology required for high-integrity defense and aerospace applications.

## ⚙️ Technical Architecture
* **Orchestrator:** [n8n](https://n8n.io/) (Self-Hosted Workflow Automation)
* **Inference Engine:** [Ollama](https://ollama.ai/) running `Llama 3` (Local LLM)
* **Vector Database:** [Qdrant](https://qdrant.tech/) (Dockerized)
* **Embedding Model:** `nomic-embed-text` (Optimized for technical density)
* **Ingestion Logic:** Recursive Character Splitting (Chunk: 1000 / Overlap: 200)

## 🛠️ Engineering Challenges & V&V
The primary challenge was **Data Integrity** within the FIA PDF Technical Tables.
* **Anomaly:** The `−` (Mathematical Minus) symbol in the PDF did not match standard ASCII hyphens, causing coordinate hallucinations.
* **Resolution:** Implemented a "Symbol Translation Protocol" in the System Prompt.
* **Verification:** Validated against **[Article 3.2.1] FW-PYLON** geometry.
    * *Predicted Range:* 60mm < Z < 200mm
    * *Actual Retrieval:* **PASSED** (Confirmed Z-Limits: 60mm - 200mm)

## 📉 System Performance
| Metric | Value | Notes |
| :--- | :--- | :--- |
| **Ingestion Speed** | 1m 0.2s | Processed 702 Regulatory Chunks |
| **Retrieval Precision** | High | Optimized Chunk Limit (n=25) |
| **Data Sovereignty** | 100% | Zero external API calls (Air-Gapped) |

## 🚀 Usage (Reproduction Steps)
1.  **Deploy Stack:** `docker-compose up -d` (Qdrant, n8n, Ollama).
2.  **Ingest Data:** Run `Workflow_A_Ingestion.json` with `2026_Formula1_Technical_Regulations.pdf`.
3.  **Execute Query:** Run `Workflow_B_Agent.json`.
    * *Query:* "What are the Z-height limits for the Front Wing Pylon?"
