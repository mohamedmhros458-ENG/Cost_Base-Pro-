# CostBase Pro (Beta v1.0.0) — by Lucid Cost Solutions

**Smart Solutions for Construction Cost & Project Management**

![.NET 8.0](https://img.shields.io/badge/.NET-8.0%20Windows-512BD4?style=flat-square&logo=dotnet)
![Architecture](https://img.shields.io/badge/Architecture-WPF%20MVVM%20%7C%20Clean%20Domain-0078D4?style=flat-square)
![Version](https://img.shields.io/badge/Release-Beta%20v1.0.0-00A86B?style=flat-square)
![License](https://img.shields.io/badge/License-Proprietary%20%7C%20Patent%20Pending-D9381E?style=flat-square)

---

## 📖 Overview

**CostBase Pro (Beta v1.0.0)** is a smart engineering and financial intelligence platform that converts Bills of Quantities (PDF, scanned images, and Excel) into a standardized **10-bucket execution budget**—revealing project funding gaps before contract signing in **2 hours instead of 10 days**. We deliver a customizable pricing and cost control system that seamlessly links the construction site to the technical office, protecting your liquidity and profit margins from day one through project closeout.

Unlike traditional spreadsheets that suffer from silent formula drift and disconnected file versions across estimating, procurement, and accounting teams, **CostBase Pro** acts as an automated **Financial & Engineering Guardrail** across the entire project lifecycle.

---

## 🎯 Why CostBase Pro Instead of Spreadsheets?

1. **Write-Once Site-to-IPC Guardrail:**
   Site progress quantities are recorded once (e.g., $420\text{ m}^3$ of reinforced concrete on BOQ item `03.02.01`). The engine automatically updates the Owner Interim Payment Certificate (IPC), generates the draft tax invoice, and hard-caps the Subcontractor IPC at $420\text{ m}^3$—blocking unapproved Variation Orders (VOs) and preventing overpayment drift.
2. **Peak Financing Gap Detection (Accrual vs. Cash Flow):**
   Separates paper accounting profit from actual working capital reality. By modeling IPC certification lag ($1\text{ month}$), collection lag ($2\text{ months}$), retention holds ($10\%$), and advance payment amortization, the system pinpoints your exact **Peak Financing Gap** by month before tender submission.
3. **Self-Learning Institutional Memory & Full Price Traceability ("Why This Price?"):**
   Every priced BOQ item carries an immutable execution trace (`IExecutionTraceRecorder`) documenting rate provenance, wastage factors, bulletin dates, and confidence scores, powered by a 4-signal semantic matcher that learns from engineer corrections.
4. **Remaining Exposed Quantity ($Q_{\text{Exposed}}$) Escalation Engine:**
   When market prices surge, CostBase Pro does not blindly apply inflation to the entire baseline. It deducts already executed quantities and fixed-price purchase/subcontract orders (`53xxxxxxxx`), calculating net financial exposure strictly on the remaining unhedged quantity:
   $$Q_{\text{Exposed}} = \max\left(0, Q_{\text{BAC}} - (Q_{\text{Actual}} + Q_{\text{FixedPO}})\right)$$
5. **Automated 10-Bucket Budget & P6 / SAP WBS Mapping:**
   Automatically generates hierarchical resource cost codes (`CostId`) and maps priced BOQs directly into the 10 standard cost control buckets and **Primavera P6** / **SAP WBS** structures in hours rather than weeks.

---

## ⚙️ Core Engineering Architecture

### 1. Pre-Tender Estimation & AI/OCR Intelligence
* **Multi-Format BOQ Ingestion (PDF / OCR / Excel):** Extracts and normalizes complex Arabic and English construction BOQs using Tesseract OCR, domain-specific morphological normalization, and unit standardization.
* **Resource Breakdown Auto-Coder:** Automatically assigns hierarchical cost identifiers (`{CompactParentBoqCode}-{LocalResourceId}`) and routes each resource into its corresponding budget bucket and procurement pool:

| Resource Type | Local ID Prefix | Budget Bucket | Downstream Target |
| :--- | :---: | :---: | :--- |
| **`Material`** | `M-001` | `.02` (Materials) | Master Material Pool (`11xx`) / MOS / PO (`53xx`) |
| **`Equipment`** | `E-001` | `.08` (Equipment) | Heavy Rental PR (`18xx`) / Idle Equipment Tracker |
| **`Labor`** | `L-001` | `.01` (Wages) | Work Center (`M08`) / Direct Crew Productivity |
| **`Sub_Contractor`** | `S-001` | `.04` (Subcontractors) | Subcontract Order (`53xx`) / Sub-IPC Hard Cap |

* **Ministry Bulletin Sync (`MHUC`):** Fetches and parses official construction material price bulletins as `ReferenceOnly` snapshots with confidence scoring and a mandatory engineer review gate before updating catalog rates and recalculating `EAC`.
* **Horus Hybrid AI Assistant:** Combines a deterministic, zero-latency offline intent engine with local LLM inference (`Ollama`) and cloud fallback (`ResilientAiGateway` with $\le 5$-item batch chunking).

### 2. Post-Tender Cost Control & Reactive Execution
* **Standard 10-Bucket Budget Architecture:**

| Bucket Code | Category Name | Control Scope |
| :---: | :--- | :--- |
| **`.01`** | Wages & Direct Labor | Site crews, workmanship, and labor productivity |
| **`.02`** | Materials & Raw Supplies | Permanent construction materials and consumables |
| **`.03`** | Services | Testing, surveying, utilities, and site services |
| **`.04`** | Subcontractors | Measured specialist and labor-only subcontracts |
| **`.05`** | Transfer & Logistics | Mobilization, freight, and transport expenses |
| **`.06`** | Depreciation | Owned plant and formwork depreciation allocations |
| **`.07`** | Internal Departments | Central workshops and internal support chargebacks |
| **`.08`** | Equipment & Plant | External equipment rentals, fuel, and maintenance |
| **`.09`** | Planning Contingency | Locked management reserve (requires formal release) |
| **`.10`** | Branch & HQ Overhead | Site indirects, branch allocation, and head-office G&A |

* **47-Node Post-Tender Process Graph:** Interactive 7-pillar workflow engine (`00` Change Management, `01` Budget, `02` Commitments, `03` Actual Cost & `GRNI` Accruals, `04` Payments & Back-Charges, `05` Forecast `PFR/EAC`, and `06` KPIs & Closed-Loop Historical Library) spanning 238 operational steps and 158 cross-module links.
* **5 Reactive Field-to-Office Pipelines:**
  1. **RFQ-to-Contract Pipeline:** `SHA-256` RFQ deduplication, 3-library auto-pricing, and instant tender-to-contract (`T` $\rightarrow$ `C`) conversion.
  2. **Write-Once Site-to-IPC Propagation:** Single-entry site measurement propagation across Owner IPC, Tax Invoice, and Subcontractor IPC caps.
  3. **Foreman Voice/Message Parser:** Extracts daily output, crew variance, stockout warnings, and cumulative idle rental equipment cost from site messages.
  4. **10-Second Project P&L:** Real-time matching of certified IPC revenue against posted Actual Cost (`AC`), cleanly separated from `GRNI` accruals.
  5. **07:00 AM Executive Decision Brief:** Automated morning digest highlighting the top 3 actionable cost, schedule, and equipment risks.

---

## 🛠️ Technical Stack

| Layer | Technology |
| :--- | :--- |
| **Framework & UI** | `.NET 8.0 Windows` (`net8.0-windows`) — `WPF` with `CommunityToolkit.Mvvm` |
| **Data Storage** | Atomic JSON Document Store (`IEstimateDocumentStore`) + `EF Core SQLite` |
| **Spreadsheets & PDF** | `ClosedXML` (Standardized BOQ & Cost Sheets) + `QuestPDF` |
| **OCR & NLP** | `Tesseract OCR` + Construction Domain Normalizer & Multi-Signal Matcher |
| **AI Gateway** | `ResilientAiGateway` (Offline Deterministic Engine + Local `Ollama` + Cloud API) |
| **Licensing** | Cryptographic Machine-Bound Hardware Licensing (`license.lic` / Activation Keys) |

---

## 📂 Repository Structure

```text
CostBase_Pro/
├── Domain/                  # Pure domain models & deterministic calculators (Pricing, EVM, Trace)
├── Models/                  # Data structures (Estimation, CostControl, Procurement, Licensing)
├── Services/                # Application services (Catalogs, CostControl, HorusAi, ReactiveFde, WorkflowGraph)
├── ViewModels/              # MVVM presentation logic and reactive state management
├── Views/                   # WPF XAML windows, dialogs, and custom controls
├── Data/                    # Standard catalogs, production rates, and benchmark datasets
├── docs/                    # Architecture foundations and confidential invention disclosures (IDF)
├── Directory.Build.props    # Unified MSBuild properties and offline sandbox guards
└── CostBase_Pro.csproj      # Main .NET 8.0 Windows application project
```

---

## 🚀 Build, Verify & Publish

The project supports deterministic **Offline Sandbox Builds** using the local NuGet cache:

```powershell
# 1. Fast Offline Build (0 Errors / 0 Warnings)
dotnet build CostBase_Pro.csproj --no-restore -p:OfflineBuild=true -v:q --nologo

# 2. Run Automated Verification & Regression Suite
dotnet run --project CostBase_Pro.csproj --no-build -- --verify-all

# 3. Publish Self-Contained Production Release (win-x64)
dotnet publish CostBase_Pro.csproj -c Release -r win-x64 --no-restore -p:OfflineBuild=true
```

---


# You can find & download the Full Version on this MediaFire Link : 
https://www.mediafire.com/file/u6q2de0h4g4qilp/CostBasePro-Setup-1.0.0-x64.exe/file
# You Can Sign Yourself in our Form to get the Activation Key : 
https://docs.google.com/forms/d/e/1FAIpQLSdrNvnr9KWAs4KhZuII66dn81QC4Xc2L--pXX1ayzb5X6Kqtw/viewform?usp=dialog
---

## 🔒 Proprietary License & Patent Pending Notice

**Copyright © 2026 Lucid Cost Solutions (Mohammed Mahrous & Mahmoud Mahrous). All Rights Reserved.**

This repository and its contents (**CostBase Pro**) are the **exclusive proprietary and confidential property of Lucid Cost Solutions**:
* No part of this software, source code, database schema, matching weights, or documentation may be copied, modified, distributed, reverse-engineered, or disclosed publicly without a prior written license agreement from **Lucid Cost Solutions**.
* **Patent Pending:** Core technical mechanisms implemented in this repository—including closed-loop adaptive BOQ-to-catalog matching, parametric item-family pricing with cryptographic execution traces, bottom-up productivity-driven ETC forecasting, and write-once multi-ledger quantity propagation—are the subject of confidential invention disclosures and pending patent applications.
