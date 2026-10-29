# Cost_Base-Pro-
Cost Base Pro Beta V 1.0.0 :is a smart engineering tool that converts BOQs (PDF/images/Excel) into a 10-bucket budget, revealing project funding gaps before signing, in 2 hours instead of 10 days. We offer a customizable pricing and cost control system, linking site to office, protecting your liquidity and profit margins from day one to closure.

CostBase Pro (Beta v1.0.0) — by Lucid Cost Solutions

Smart Solutions for Construction Cost & Project Management

# Overview

CostBase Pro (Beta v1.0.0) is a smart engineering and financial intelligence platform that converts Bills of Quantities (PDF, scanned images, and Excel) into a standardized 10-bucket execution budget—revealing project funding gaps before contract signing in 2 hours instead of 10 days. We deliver a customizable pricing and cost control system that seamlessly links the construction site to the technical office, protecting your liquidity and profit margins from day one through project closeout.

Unlike traditional spreadsheets that suffer from silent formula drift and disconnected file versions across estimating, procurement, and accounting teams, CostBase Pro acts as an automated Financial & Engineering Guardrail across the entire project lifecycle.

#🎯 Why CostBase Pro Instead of Spreadsheets?

Write-Once Site-to-IPC Guardrail:
Site progress quantities are recorded once (e.g., $420\text{ m}^3$ of reinforced concrete on BOQ item 03.02.01). The engine automatically updates the Owner Interim Payment Certificate (IPC), generates the draft tax invoice, and hard-caps the Subcontractor IPC at $420\text{ m}^3$—blocking unapproved Variation Orders (VOs) and preventing overpayment drift.

Peak Financing Gap Detection (Accrual vs. Cash Flow):
Separates paper accounting profit from actual working capital reality. By modeling IPC certification lag ($1\text{ month}$), collection lag ($2\text{ months}$), retention holds ($10\%$), and advance payment amortization, the system pinpoints your exact Peak Financing Gap by month before tender submission.

Self-Learning Institutional Memory & Full Price Traceability ("Why This Price?"):
Every priced BOQ item carries an immutable execution trace (IExecutionTraceRecorder) documenting rate provenance, wastage factors, bulletin dates, and confidence scores, powered by a 4-signal semantic matcher that learns from engineer corrections.

Remaining Exposed Quantity ($Q_{\text{Exposed}}$) Escalation Engine:
When market prices surge, CostBase Pro does not blindly apply inflation to the entire baseline. It deducts already executed quantities and fixed-price purchase/subcontract orders (53xxxxxxxx), calculating net financial exposure strictly on the remaining unhedged quantity:


$$Q_{\text{Exposed}} = \max\left(0, Q_{\text{BAC}} - (Q_{\text{Actual}} + Q_{\text{FixedPO}})\right)$$

Automated 10-Bucket Budget & P6 / SAP WBS Mapping:
Automatically generates hierarchical resource cost codes (CostId) and maps priced BOQs directly into the 10 standard cost control buckets and Primavera P6 / SAP WBS structures in hours rather than weeks.

# You can find & download the Full Version on this MediaFire Link : 
https://www.mediafire.com/file/u6q2de0h4g4qilp/CostBasePro-Setup-1.0.0-x64.exe/file
# You Can Sign Yourself in our Form to get the Activation Key : 
https://docs.google.com/forms/d/e/1FAIpQLSdrNvnr9KWAs4KhZuII66dn81QC4Xc2L--pXX1ayzb5X6Kqtw/viewform?usp=dialog

#⚙️ Core Engineering Architecture

1. Pre-Tender Estimation & AI/OCR Intelligence

Multi-Format BOQ Ingestion (PDF / OCR / Excel): Extracts and normalizes complex Arabic and English construction BOQs using Tesseract OCR, domain-specific morphological normalization, and unit standardization.

Resource Breakdown Auto-Coder: Automatically assigns hierarchical cost identifiers ({CompactParentBoqCode}-{LocalResourceId}) and routes each resource into its corresponding budget bucket and procurement pool:

Resource Type

Local ID Prefix

Budget Bucket

Downstream Target

Material

M-001

.02 (Materials)

Master Material Pool (11xx) / MOS / PO (53xx)

Equipment

E-001

.08 (Equipment)

Heavy Rental PR (18xx) / Idle Equipment Tracker

Labor

L-001

.01 (Wages)

Work Center (M08) / Direct Crew Productivity

Sub_Contractor

S-001

.04 (Subcontractors)

Subcontract Order (53xx) / Sub-IPC Hard Cap

Ministry Bulletin Sync (MHUC): Fetches and parses official construction material price bulletins as ReferenceOnly snapshots with confidence scoring and a mandatory engineer review gate before updating catalog rates and recalculating EAC.

Horus Hybrid AI Assistant: Combines a deterministic, zero-latency offline intent engine with local LLM inference (Ollama) and cloud fallback (ResilientAiGateway with $\le 5$-item batch chunking).

2. Post-Tender Cost Control & Reactive Execution

Standard 10-Bucket Budget Architecture:

Bucket Code

Category Name

Control Scope

.01 Wages & Direct Labor

Site crews, workmanship, and labor productivity

.02 Materials & Raw Supplies

Permanent construction materials and consumables

.03 Services

Testing, surveying, utilities, and site services

.04 Subcontractors

Measured specialist and labor-only subcontracts

.05 Transfer & Logistics

Mobilization, freight, and transport expenses

.06 Depreciation

Owned plant and formwork depreciation allocations

.07 Internal Departments

Central workshops and internal support chargebacks

.08 Equipment & Plant

External equipment rentals, fuel, and maintenance

.09 Planning Contingency

Locked management reserve (requires formal release)

.10 Branch & HQ Overhead

Site indirects, branch allocation, and head-office G&A

47-Node Post-Tender Process Graph: Interactive 7-pillar workflow engine (00 Change Management, 01 Budget, 02 Commitments, 03 Actual Cost & GRNI Accruals, 04 Payments & Back-Charges, 05 Forecast PFR/EAC, and 06 KPIs & Closed-Loop Historical Library) spanning 238 operational steps and 158 cross-module links.

5 Reactive Field-to-Office Pipelines:

RFQ-to-Contract Pipeline: SHA-256 RFQ deduplication, 3-library auto-pricing, and instant tender-to-contract (T $\rightarrow$ C) conversion.

Write-Once Site-to-IPC Propagation: Single-entry site measurement propagation across Owner IPC, Tax Invoice, and Subcontractor IPC caps.

Foreman Voice/Message Parser: Extracts daily output, crew variance, stockout warnings, and cumulative idle rental equipment cost from site messages.

10-Second Project P&L: Real-time matching of certified IPC revenue against posted Actual Cost (AC), cleanly separated from GRNI accruals.

07:00 AM Executive Decision Brief: Automated morning digest highlighting the top 3 actionable cost, schedule, and equipment risks.

#🛠️ Technical Stack

Layer

Technology

Framework & UI

.NET 8.0 Windows (net8.0-windows) — WPF with CommunityToolkit.Mvvm

Data Storage

Atomic JSON Document Store (IEstimateDocumentStore) + EF Core SQLite

Spreadsheets & PDF

ClosedXML (Standardized BOQ & Cost Sheets) + QuestPDF

OCR & NLP

Tesseract OCR + Construction Domain Normalizer & Multi-Signal Matcher

AI Gateway

ResilientAiGateway (Offline Deterministic Engine + Local Ollama + Cloud API)

Licensing

Cryptographic Machine-Bound Hardware Licensing (license.lic / Activation Keys)

#🚀 Build, Verify & Publish

The project supports deterministic Offline Sandbox Builds using the local NuGet cache:

# 1. Fast Offline Build (0 Errors / 0 Warnings)
dotnet build CostBase_Pro.csproj --no-restore -p:OfflineBuild=true -v:q --nologo

# 2. Run Automated Verification & Regression Suite
dotnet run --project CostBase_Pro.csproj --no-build -- --verify-all

# 3. Publish Self-Contained Production Release (win-x64)
dotnet publish CostBase_Pro.csproj -c Release -r win-x64 --no-restore -p:OfflineBuild=true

#🔒 Proprietary License & Patent Pending Notice

Copyright © 2026 Lucid Cost Solutions (Mohammed Mahrous & Mahmoud Mahrous). All Rights Reserved.

This repository and its contents (CostBase Pro) are the exclusive proprietary and confidential property of Lucid Cost Solutions:

No part of this software, source code, database schema, matching weights, or documentation may be copied, modified, distributed, reverse-engineered, or disclosed publicly without a prior written license agreement from Lucid Cost Solutions.

Patent Pending: Core technical mechanisms implemented in this repository—including closed-loop adaptive BOQ-to-catalog matching, parametric item-family pricing with cryptographic execution traces, bottom-up productivity-driven ETC forecasting, and write-once multi-ledger quantity propagation—are the subject of confidential invention disclosures and pending patent applications.
