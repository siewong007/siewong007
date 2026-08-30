<div align="center">

# Paul Wong

**Full-stack engineer — backend-leaning.** Rust · Java · Go · TypeScript  
Malaysia (UTC+8) · MSc Artificial Intelligence, [Sunway University](https://sunwayuniversity.edu.my/)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Paul_Wong-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/paul-wong-02864a19a)
[![Open to full-stack roles](https://img.shields.io/badge/Open_to-full--stack_roles-0a7d32?style=flat-square)](https://www.linkedin.com/in/paul-wong-02864a19a)

<p>
  <img src="https://skillicons.dev/icons?i=rust,java,spring,go,ts,react,postgres,redis,docker,githubactions,terraform,aws,python,pytorch&perline=7" alt="Rust, Java, Spring, Go, TypeScript, React, PostgreSQL, Redis, Docker, GitHub Actions, Terraform, AWS, Python, PyTorch" />
</p>

</div>

I build transactional business systems — the kind where a wrong number is a real problem.
Payroll that has to match statutory law, hotel ledgers that have to balance, stock that must
never go negative. Most of my code is Rust and Java on PostgreSQL, with React in front of it.

The through-line in the work below is **correctness under money and compliance**: integer-cent
arithmetic instead of floats, invariants enforced in the database rather than only in handlers,
characterization tests pinned around billing paths, and calculations that fail loudly rather
than silently returning zero.

---

## Flagship work

### [hotel-app](https://github.com/siewong007/hotel-app) — hotel property management

*Nine months of continuous development: 864 commits, Nov 2025 → Aug 2026.*

A full PMS: reservations, folios, rates, housekeeping, guest portal, staff RBAC, plus a Tauri
desktop build. ~104k lines of Rust and ~87k of TypeScript across 185 API routes and 98 tables.

The part I would point a reviewer at is the money handling. Billing, ledger and invoice totals
are locked down by **characterization tests** — `payment_characterization.rs`,
`ledger_characterization.rs`, `invoice_total_characterization.rs` — that pin existing financial
behaviour before it can be refactored, so a change that alters a total fails the build instead
of quietly shipping. An `openapi_drift` test fails CI when the spec and the router disagree.

`Rust` `Axum` `React` `Tauri` `PostgreSQL` · 5 CI workflows

### [payroll-system](https://github.com/siewong007/payroll-system) — Malaysian SME payroll & HR

*238 commits over five months.*

Multi-company payroll: EPF / SOCSO / EIS, attendance with geofenced kiosk check-in, approvals,
payslip and EA exports. 234 endpoints, 57 tables, 63k lines of Rust.

Three decisions worth the click:

- **Statutory calculation fails closed.** A payroll run refuses to execute unless an
  effective-dated, source-linked, verified rule set covers the period. Automatic PCB is
  hard-disabled outside tests pending LHDN conformance — a missing rate raises an error instead
  of becoming a zero deduction.
- **Tenancy is enforced by the schema.** Employee child tables carry a composite
  `(company_id, id)` foreign key, with `NOT NULL` load-bearing because a composite FK is
  `MATCH SIMPLE` and a null tenant would silently skip the check.
- **488 SQL queries are verified at compile time** via SQLx's offline cache, re-checked in CI so
  a stale cache cannot pass. Money moves as integer sen, never `f64`.

`Rust` `Axum` `React` `PostgreSQL` `Terraform` · CI actions pinned to commit SHAs

### [online-shopping-platform](https://github.com/siewong007/online-shopping-platform) — storefront + admin console

*106 commits, actively developed Apr → Aug 2026.*

Catalog, cart, checkout, memberships, reviews, vouchers, support chat, and an operations console.
84 endpoints, 59 tables, 39 migrations.

Operationally the most disciplined thing I have built: **146 Rust tests enumerated by the
compiler** (86 of them against a real Postgres) plus 67 frontend tests, CI gating on
`clippy -D warnings`, a SHA-256 migration ledger that fails closed on schema drift, HMAC-verified
idempotent payment webhooks, and a backup process that proves itself — it encrypts, ships
off-site, downloads the object back, restores it into a throwaway container and asserts
row-count parity before reporting success. 34 `SELECT … FOR UPDATE` row locks guard the order
and inventory paths.

`Rust` `Axum` `SQLx` `React` `PostgreSQL` `Docker` `Caddy`

---

## The same product, twice

[**hotel-app-spring**](https://github.com/siewong007/hotel-app-spring) re-implements the hotel API
in Spring Boot 4 / Java 21 — 94 JPA entities, 292 route mappings, session-bound JWT with
refresh-token rotation proven by Testcontainers integration tests.

The claim is falsifiable on purpose: a parity checker diffs every `@*Mapping` against the Rust
router's 270-endpoint inventory and exits non-zero on any gap. Porting the same domain across two
type systems is the clearest evidence I can give that I understand the domain rather than the
framework.

---

## Also shipped

| Project | What it is | Stack |
|---|---|---|
| [inventory-crm](https://github.com/siewong007/inventory-crm) | Multi-warehouse inventory and orders. Stock cannot go negative — a DB `CHECK`, `SELECT FOR UPDATE`, and advisory locks for document numbering enforce it, with a 63-check end-to-end suite. | `Go` `chi` `React` `PostgreSQL` |
| [ai-trading-platform](https://github.com/siewong007/ai-trading-platform) | Binance spot research lab — EMA/RSI with ATR stops behind a pre-registered backtest gate that stays research-only until a stored PASS. 8.7k lines of Rust, 148 tests. | `Rust` `SQLite` |
| [banking-app](https://github.com/siewong007/banking-app) | Personal finance API with a hand-written WebAuthn passkey ceremony — DB-persisted, single-use, five-minute challenges — over a 42-migration schema. *Work in progress: many routes are still stubs.* | `Rust` `Axum` `WebAuthn` |
| [airtasker](https://github.com/siewong007/airtasker) | Two-sided task marketplace — accepting an offer atomically rejects competitors, STOMP chat, escrow-style payments. *Prototype.* | `Java` `Spring Boot` `React` |
| [invoice-generator](https://github.com/siewong007/invoice-generator) | Client-side RM invoicing with amount-in-words totals. Every field is driven with live XSS payloads, then asserted on three independent DOM invariants. | `TypeScript` `React` `Vitest` |

---

## Research & ML

| Project | Focus |
|---|---|
| [mlops-credit-card-fraud-detection](https://github.com/siewong007/mlops-credit-card-fraud-detection) | End-to-end reproducible fraud pipeline — DVC, MLflow, Pandera schema contracts, SHAP, Evidently drift monitoring. 110 tests, two CI workflows, [published docs site](https://siewong007.github.io/mlops-credit-card-fraud-detection/). |
| [agent-kv-retention](https://github.com/siewong007/agent-kv-retention) | MSc thesis — KV-cache retention policies for LLM agent workloads. CPU simulator calibrated against vLLM + Qwen2.5-3B, falsification-first design, cost reported in ringgit rather than hit rate. |
| [vantage-pipeline](https://github.com/siewong007/vantage-pipeline) | Local AI video generation, measured rather than asserted. Found the export path was destroying more quality than any model-side lever could recover, and that the quality metric itself ranked worse images higher — both fixed, both falsified against known-bad inputs. |
| [trustrag](https://github.com/siewong007/trustrag) | *In progress.* Hallucination detection for RAG on a Databricks lakehouse — supervised cross-encoder detectors compared against LLM-as-a-judge on accuracy, latency and cost together. |

---

## Stack

**Daily** — Rust (Axum, SQLx, Tokio) · TypeScript / React · PostgreSQL · Docker · GitHub Actions  
**Comfortable** — Java (Spring Boot, JPA) · Go (chi, pgx) · Python · Redis · SQLite · Tauri · Terraform  
**ML** — PyTorch · scikit-learn / XGBoost · Hugging Face · MLflow · DVC · vLLM

<div align="center">

Open to full-stack and backend roles, remote or Malaysia-based.

[LinkedIn](https://www.linkedin.com/in/paul-wong-02864a19a) · [GitHub](https://github.com/siewong007)

</div>
