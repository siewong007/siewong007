<div align="center">

# Paul Wong

**Full-stack software engineer** · Malaysia  
MSc Artificial Intelligence @ [Sunway University](https://sunwayuniversity.edu.my/)

[![Open to work](https://img.shields.io/badge/Open_to_work-full--stack-0a7d32?style=for-the-badge)](https://www.linkedin.com/in/paul-wong-02864a19a)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Paul_Wong-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/paul-wong-02864a19a)
[![GitHub](https://img.shields.io/badge/GitHub-siewong007-181717?style=for-the-badge&logo=github)](https://github.com/siewong007)

I ship product systems end-to-end — APIs, data stores, and React UIs — in Rust, Java, Go, and TypeScript.

<p>
  <img src="https://skillicons.dev/icons?i=rust,java,go,ts,react,postgres,python,pytorch,tensorflow,docker,aws" alt="Stack" />
</p>

</div>

---

## Product systems

<table>
<tr>
<td width="50%" valign="top">

### [payroll-system](https://github.com/siewong007/payroll-system)
Malaysian SME payroll & HR — EPF / SOCSO / EIS / PCB, approvals, attendance.

`Rust` `Axum` `React` `PostgreSQL` `WebAuthn`

</td>
<td width="50%" valign="top">

### [hotel-app](https://github.com/siewong007/hotel-app)
Hotel administration — rooms, bookings, staff RBAC, Tauri desktop shell.

`Rust` `Axum` `React` `Tauri` `PostgreSQL`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [hotel-app-spring](https://github.com/siewong007/hotel-app-spring)
Feature-identical Spring Boot port of hotel-app — 270 endpoints, JWT + RBAC.

`Java` `Spring Boot` `React` `PostgreSQL`

</td>
<td width="50%" valign="top">

### [banking-app](https://github.com/siewong007/banking-app)
Personal banking & finance with passkeys and fraud / insights MCP servers.

`Rust` `Axum` `React` `WebAuthn` `PostgreSQL`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [inventory-crm](https://github.com/siewong007/inventory-crm)
Multi-warehouse inventory CRM — purchase / sales orders, auto stock moves.

`Go` `React` `PostgreSQL`

</td>
<td width="50%" valign="top">

### [online-shopping-platform](https://github.com/siewong007/online-shopping-platform)
Ecommerce storefront and API — catalog, orders, PostgreSQL.

`Rust` `Axum` `React` `PostgreSQL`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [airtasker](https://github.com/siewong007/airtasker)
Task marketplace — JWT auth, WebSocket chat, escrow-style payments.

`Java` `Spring Boot` `React` `PostgreSQL`

</td>
<td width="50%" valign="top">

### [invoice-generator](https://github.com/siewong007/invoice-generator)
RM invoices with amount-in-words, autosave, XSS-hardened, 192 tests.

`TypeScript` `React` `Vitest`

</td>
</tr>
</table>

## Research & ML

<table>
<tr>
<td width="50%" valign="top">

### [trustrag](https://github.com/siewong007/trustrag)
Lakehouse-native hallucination detection for RAG — supervised detectors vs LLM-as-a-judge. A PyTorch cross-encoder reaches near-parity F1 (0.958 vs 0.969) at ~25x lower p95 latency (212 ms vs 5,207 ms).

`PyTorch` `TensorFlow` `Transformers` `FAISS` `Databricks` `MLflow`

</td>
<td width="50%" valign="top">

### [agent-kv-retention](https://github.com/siewong007/agent-kv-retention)
MSc thesis — KV-cache retention for LLM agents, costed in ringgit not hit rate.

`Python` `vLLM` `LLM`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [mlops-credit-card-fraud-detection](https://github.com/siewong007/mlops-credit-card-fraud-detection)
Reproducible fraud pipeline — Pandera, MLflow, DVC, SHAP, Evidently.

[`Docs site`](https://siewong007.github.io/mlops-credit-card-fraud-detection/) · `Python` `XGBoost` `MLOps`

</td>
<td width="50%" valign="top">

### [ai-trading-platform](https://github.com/siewong007/ai-trading-platform)
Binance spot research lab — EMA / RSI, ATR stops, pre-registered backtest gate.

`Rust` `SQLite` `research-only`

</td>
</tr>
</table>

## Deep learning toolkit

What I actually build models with, and where each of these is used in the repos above.

| Area | Tools | Used in |
|---|---|---|
| **Training frameworks** | PyTorch · TensorFlow / Keras | `trustrag` — a DeBERTa-v3 cross-encoder in PyTorch and a Keras NLI fact-checker, trained on the same labels so the two stacks compare like for like |
| **Transformers & embeddings** | Hugging Face Transformers · Datasets · sentence-transformers · accelerate | `trustrag` — grounded generation (Qwen2.5-1.5B / SmolLM2), claim decomposition, corpus embedding |
| **Retrieval** | FAISS · BM25 (rank-bm25) · RRF fusion · cross-encoder reranking | `trustrag` — hybrid dense + sparse retrieval feeding the RAG pipeline |
| **LLM serving & inference** | vLLM · KV-cache paging & admission policies | `agent-kv-retention` — retention policies validated against real vLLM serving behaviour |
| **Classical ML** | scikit-learn · XGBoost · SHAP | `mlops-credit-card-fraud-detection` — gradient-boosted fraud model with explanations |
| **Experiment tracking & data** | MLflow · DVC · Pandera · Evidently | `trustrag`, `mlops-credit-card-fraud-detection` — runs, artefacts, schema contracts, drift |
| **Distributed / lakehouse** | Databricks · Delta Lake · Spark | `trustrag` — Delta tables for corpus, chunks, traces and results; Spark batch embedding |
| **Evaluation** | P/R/F1 · AUROC · Cohen's κ · p95 latency · cost per 1k claims | `trustrag` — accuracy is never reported without the cost and latency next to it |

---

<div align="center">

### Stack

**Backend** — Rust (Axum) · Java (Spring Boot) · Go  
**Frontend** — TypeScript · React · Vite · Tauri  
**Data** — PostgreSQL · Redis · SQLite · Delta Lake  
**Deep learning** — PyTorch · TensorFlow / Keras · Hugging Face · FAISS · vLLM  
**ML / ops** — Python · MLflow · DVC · Databricks · Docker · GitHub Actions · Terraform

[LinkedIn](https://www.linkedin.com/in/paul-wong-02864a19a) · [GitHub](https://github.com/siewong007)

</div>
