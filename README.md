# SIR V.4.2 × Semantica — Proof of Concept

**Document ID:** SEM-TFE-POC-2026-V1.0
**Date:** June 27, 2026
**Classification:** RESTRICTED — CO-DEVELOPMENT BRIEF
**Prepared By:** Semantica Engineering / Joint Systems Architecture
**Jurisdiction:** Democratic Socialist Republic of Sri Lanka

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Problem Statement](#2-problem-statement)
3. [Solution Overview](#3-solution-overview)
   - [3.4 Semantica's Core Responsibilities](#34-semanticas-core-responsibilities)
4. [POC Scope & Boundaries](#4-poc-scope--boundaries)
5. [System Architecture](#5-system-architecture)
6. [4-Week Delivery Plan](#6-4-week-delivery-plan)
7. [Deliverables Matrix](#7-deliverables-matrix)
8. [Financial Calibration Baseline](#8-financial-calibration-baseline)
9. [Success Criteria & Acceptance Gates](#9-success-criteria--acceptance-gates)
10. [Risk Register](#10-risk-register)
11. [Team & Responsibilities](#11-team--responsibilities)
12. [Appendix A — Repository Structure](#appendix-a--repository-structure)
13. [Appendix B — Key Code Contracts](#appendix-b--key-code-contracts)

---

## 1. Executive Summary

This document defines the Proof of Concept scope, architecture, and 4-week execution plan for integrating **Semantica** as the core intelligence, validation, and accountability middleware within **The Full Equation (TFE) Sovereign Integrity Rail (SIR) V.4.2**.

Sri Lanka is the sovereign case study. The PoC demonstrates that raw biophysical and industrial telemetry from four Critical Resource Nodes can be converted into auditable, legally defensible **Sovereign Integrity Units (SIUs)** — assets structured to qualify as Tier-1 High-Quality Liquid Assets (HQLA) on the Central Bank of Sri Lanka's balance sheet.

**The PoC must be fully functional and demo-ready in 28 working days.** It produces a running system with 14 named deliverables — not a slide deck.

---

## 2. Problem Statement

### 2.1 The Accountability Gap in Sovereign Asset Minting

When a central bank ingests national natural assets onto its balance sheet to satisfy Tier-1 HQLA reserve criteria, every financial figure and every programmatic decision must be **legally underwritable and mathematically defensible**. The current landscape fails on three axes:

- **Traceability gap** — Standard RAG pipelines synthesize documents probabilistically. The synthesis path is invisible. Auditors cannot reconstruct the chain from a token valuation back to the raw sensor reading that caused it.

- **Compliance enforcement gap** — Probabilistic LLM reasoning is used to evaluate regulatory rules. Results are inconsistent between runs, non-repeatable under audit, and legally indefensible in court.

- **Temporal integrity gap** — Legacy systems use flat changelogs with no bi-temporal tracking. There is no mechanism to prove a historical baseline was untampered, and no way to replay the state of the world as it was on a specific past date.

### 2.2 The Specific Problem for Sri Lanka

Sri Lanka holds four high-value natural asset classes that are currently **unmonetized on the Central Bank balance sheet**:

- **Highland hydrology** — the Knuckles and Central Massif recharge zones
- **Coastal blue-carbon reserves** — Kokkilai and Puttalam lagoon mangrove shields
- **Phosphate mining corridors** — Eppawala extraction complexes
- **Containerized trade gateway** — Port of Colombo JCT/CICT terminals

No existing system can convert the raw biophysical and industrial reality of these nodes into a financially auditable, legally compliant reserve instrument. Without a verifiable middleware layer:

- No international rating agency will underwrite the SIU reserve
- No clearinghouse will accept the 4:1 collateral squeeze hook as legally mandated
- No regulator will accept the compliance audit without a deterministic, machine-readable lineage trail

### 2.3 Why This PoC Is Necessary Now

This PoC proves — in running code against real Sri Lankan data — three things:

1. Semantica's deterministic reasoning layer can sit between TFE edge hardware and STOKR's Liquid Network ledger and produce a legally defensible minting signal
2. The resulting SIU minting decision is unbribable, fully auditable, and W3C PROV-O compliant
3. The 4:1 Yield Compression Event fires with zero probabilistic dependency — no LLM in the loop

---

## 3. Solution Overview

### 3.1 Three-Layer Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    TFE EDGE HARDWARE LAYER                      │
│  Sentinel Hub V.4 (biophysical) + Socket-7 Gateways (SCADA)    │
│  SRAM PUF silicon fingerprinting + ML-KEM-768 encryption        │
└────────────────────────────┬────────────────────────────────────┘
                             │  Post-Quantum Encrypted Stream
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│               SEMANTICA VERACITY LAYER  ← this PoC              │
│                                                                 │
│  ├─ SHACL Ingestion Gates                                       │
│  ├─ LayoutLMv3 Forensic Clean Room                              │
│  ├─ Bi-Temporal Knowledge Graph                                 │
│  ├─ Betweenness Centrality Engine                               │
│  ├─ Rete Network Compliance Rules                               │
│  ├─ record_decision() + trace_decision_chain()                  │
│  └─ W3C PROV-O Export                                           │
└────────────────────────────┬────────────────────────────────────┘
                             │  Verified Oracle Handshake
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                  STOKR INFRASTRUCTURE LAYER                     │
│  ORO Fund SPV (Sicos Securities) + Blockstream AMP              │
│  SIU (reserve) + SIU-T (transactional) on Liquid Network       │
│  24/7 secondary trading via SideSwap                            │
└─────────────────────────────────────────────────────────────────┘
```

### 3.2 The SIU Valuation Formula

Every minted SIU is valued by:

```
SIU_adjusted = f(C_B × ΣE_D) × (1 − Ω_Threshold)
```

- **C_B** — Betweenness Centrality of the node within the sovereign hypergraph
- **ΣE_D** — Downstream Asset Exposure (port throughput velocity, data-centre uptime, infrastructure lifespan)
- **Ω_Threshold** — Real-time risk probability derived from live edge sensor readings

### 3.3 The Collateral Squeeze Rule

```
γ = { 2:1  if Ω_Threshold < Ω_Crit      ← normal baseline conditions
    { 4:1  if Ω_Threshold ≥ Ω_Crit      ← Yield Compression Event
```

When a sensor breach fires, the **Rete network — not an LLM** — triggers the Yield Compression Event and pushes the 4:1 lock signal to STOKR's TaaS endpoint along with a complete, immutable causal path object.

---

### 3.4 Semantica's Core Responsibilities

Semantica is the **sole middleware layer** between TFE's edge hardware and STOKR's settlement ledger. Everything that makes a minting or squeeze decision legally defensible is Semantica's responsibility. The table below defines hard ownership boundaries.

> **What Semantica does NOT own:** Physical edge hardware collection (TFE), token issuance and settlement (STOKR), SPV legal structuring (STOKR/Sicos), and the LayoutLMv3 document model itself (Hugging Face, containerised by Kaif).

---

#### Responsibility 1 — SHACL Ingestion Validation Gate

- **What:** Defines the OWL ontology for all TFE entity types (biophysical node, industrial node, telemetry reading, threshold event, mint decision). Auto-derives SHACL shape constraints from the ontology using pySHACL.
- **How:** Every raw telemetry packet arriving from TFE-ib or TFE-gdp simulators must pass the SHACL gate before any data touches the knowledge graph. Packets that fail structural validation are rejected with a plain-English report; they never reach the graph layer.
- **Success bar:** 100% of intentionally corrupted test packets rejected. Zero false passes.
- **SDK component:** `ingestion/shacl_gates.py` + `ingestion/ontology.ttl`

---

#### Responsibility 2 — Bi-Temporal Knowledge Graph

- **What:** Stores every asserted fact with two independent timestamps — `valid_time` (when the fact was true in the real world) and `recorded_at` (when Semantica ingested it). These are never conflated.
- **How:** `TemporalKnowledgeGraph` wraps every graph edge with this dual timestamp. `graph.state_at("YYYY-MM-DD")` reconstructs the full 4-node Sri Lanka hypergraph as it existed on any past date, enabling forensic replay without modifying the live graph.
- **Why this matters:** Satisfies bi-temporal audit requirements for international rating agencies. Any claim that "the highlands recharge rate was X in 2003" can be replayed and proven.
- **SDK component:** `graph/temporal_graph.py`

---

#### Responsibility 3 — Allen Interval Algebra Anomaly Detection

- **What:** Applies the 13 Allen temporal relations (`meets`, `overlaps`, `during`, `starts`, `finishes`, `before`, `equal`, and their inverses) to detect timing anomalies in the ingested SCADA and biophysical logs.
- **How:** Flags event sequences where a downstream effect precedes its upstream cause — a strong signal of data tampering or instrument miscalibration — without any LLM interpretation.
- **SDK component:** Enabled via `TemporalKnowledgeGraph(enable_allen_algebra=True)`

---

#### Responsibility 4 — Betweenness Centrality Engine

- **What:** Computes C_B (Betweenness Centrality) for each of the 4 Sri Lanka nodes, quantifying how many shortest paths in the sovereign hypergraph pass through each node. A node with high C_B is a critical bottleneck; its loss cascades systemically.
- **How:** `CentralityCalculator` runs over the live graph state. C_B for all 4 nodes must compute in < 50ms. The result feeds directly into the SIU valuation formula as the primary floor-price variable.
- **Interpretation:** Node 4 (Port of Colombo) typically holds the highest C_B due to trade interdependency. Node 1 (highlands hydrology) holds the highest ecological weight because it constrains Nodes 2 and 3 downstream.
- **SDK component:** `graph/centrality.py`

---

#### Responsibility 5 — SIU Valuation Formula (Live Computation)

- **What:** Computes `SIU_adjusted = f(C_B × ΣE_D) × (1 − Ω_Threshold)` in real time as graph state changes. No off-chain oracle. No LLM interpolation.
- **Variables owned by Semantica:**
  - `C_B` — computed from the live graph (Responsibility 4 above)
  - `ΣE_D` — summed Downstream Asset Exposure across all 4 nodes; hardcoded coefficients sourced from the Genesis Matrix
  - `Ω_Threshold` — derived from live SHACL-validated sensor readings; updated on every successful packet ingestion
- **SDK component:** `graph/centrality.py` + `graph/context_graph.py`

---

#### Responsibility 6 — Rete Compliance Engine (Deterministic, Zero-LLM)

- **What:** Evaluates all regulatory and ecological rules against every telemetry packet and every mint decision. Uses a pre-compiled Rete network — not an LLM, not a vector index, not a probabilistic classifier.
- **Rules owned by Semantica (all 6):**
  - Rule 1 — Aquifer drawdown velocity ≤ recharge rate (Node 1)
  - Rule 2 — Invasive species density below threshold in mangrove perimeter (Node 2)
  - Rule 3 — Thermodynamic harmonics within ±2σ of genesis baseline (Node 3)
  - Rule 4 — PLC load weight vs. bill of lading divergence < 3% (Node 4)
  - Rule 5 — Wildfire fuel continuity index below critical threshold (biophysical nodes)
  - Covenant Rule — SIU-T circulating supply ≤ 50% of SIU parent reserve at all times
- **Guarantee:** 1,000 evaluations on identical inputs produce identical outputs. Non-compliance blocks the mint call with a structured error naming the exact failing rule.
- **SDK component:** `reasoning/rete_engine.py` + `reasoning/rules/`

---

#### Responsibility 7 — S-1 Mint Decision Tracker

- **What:** Creates an immutable, cryptographically-bound causal object for every minting and squeeze decision. The object records the decision category, outcome, confidence score, rationale, and the list of entity nodes involved.
- **Three API methods Semantica must expose:**
  - `graph.record_decision()` — writes the decision object to the graph
  - `graph.check_decision_rules()` — runs the Rete evaluation and binds the result to the decision
  - `graph.trace_decision_chain()` — walks the causal graph backward from the decision to the originating sensor values, timestamps, and breach values
- **Constraint:** If `check_decision_rules()` returns `approved=False`, the mint call raises a structured error before any signal reaches STOKR. No blocked decision is silently discarded.
- **SDK component:** `reasoning/decision_tracker.py`

---

#### Responsibility 8 — 4:1 Yield Compression Event Engine

- **What:** When `Ω_Threshold ≥ Ω_Crit`, Semantica's Rete network fires the Yield Compression Event within 100ms — no human in the loop, no LLM, no probabilistic delay.
- **Sequence Semantica owns:**
  1. Sensor breach detected in SHACL-validated packet
  2. `Ω_Threshold` value updated in the knowledge graph
  3. Rete evaluates the compression rule — fires immediately
  4. `record_decision(category="yield_compression", outcome="squeeze_4_1")` creates the causal object
  5. Causal object posted to STOKR TaaS `/collateral-squeeze` endpoint
  6. Collateral ratio transitions from 2:1 → 4:1 on the circulating SIU-T supply
- **SLA:** p99 latency from breach detection to 4:1 lock confirmation < 100ms
- **SDK component:** `reasoning/rete_engine.py` + `reasoning/decision_tracker.py`

---

#### Responsibility 9 — Provenance Manager (Per-Claim Source Attribution)

- **What:** Tracks every asserted fact in the knowledge graph to its originating source: document filename, DOI, author, page number, ingestion timestamp, and confidence score. Every single data point that influences an SIU valuation must have a provenance record.
- **How:** `ProvenanceManager.track_entity()` binds claims at ingestion time. `get_lineage()` walks the full multi-hop ancestor chain — a claim derived from a derived metric will chain back through all intermediate steps to the original source document.
- **Minimum standard:** Every entity in the graph must have a ≥ 3-hop provenance chain traceable to a DOI or official government source.
- **SDK component:** `provenance/manager.py`

---

#### Responsibility 10 — W3C PROV-O Turtle Export

- **What:** Converts the provenance graph into a compliance-grade W3C PROV-O Turtle (`.ttl`) file. This is the artifact that international auditors, rating agencies, and regulators receive.
- **Required triples in every export:**
  - `prov:Entity` — every tracked data entity
  - `prov:wasDerivedFrom` — lineage chain
  - `prov:wasAttributedTo` — source authority (government body, DOI holder)
  - `prov:generatedAtTime` — ingestion timestamp
  - `prov:wasAssociatedWith` — the sensor or parsing agent that generated the claim
- **Validation gate:** The generated `.ttl` must parse with zero errors in rdflib before being considered a valid export artifact.
- **SDK component:** `provenance/exporter.py`

---

#### Semantica Responsibility Summary

| # | Responsibility | SDK Component | Key Guarantee |
| --- | --- | --- | --- |
| R1 | SHACL Ingestion Gate | `ingestion/shacl_gates.py` | 100% corrupted packets rejected |
| R2 | Bi-Temporal Knowledge Graph | `graph/temporal_graph.py` | Point-in-time replay at any date |
| R3 | Allen Interval Algebra | `graph/temporal_graph.py` | Timing anomalies flagged without LLM |
| R4 | Betweenness Centrality | `graph/centrality.py` | C_B for 4 nodes in < 50ms |
| R5 | SIU Valuation Formula | `graph/centrality.py` | Live, no off-chain oracle |
| R6 | Rete Compliance Engine | `reasoning/rete_engine.py` | Deterministic, zero-LLM, 6 rules |
| R7 | S-1 Mint Decision Tracker | `reasoning/decision_tracker.py` | Full causal chain to sensor |
| R8 | 4:1 Compression Event | `reasoning/rete_engine.py` | < 100ms p99 breach-to-lock |
| R9 | Provenance Manager | `provenance/manager.py` | ≥ 3-hop lineage to DOI |
| R10 | W3C PROV-O Export | `provenance/exporter.py` | Zero-error rdflib parse |

---

## 4. POC Scope & Boundaries

### 4.1 What Is In Scope

- **Forensic Ingestion Clean Room** — Containerized LayoutLMv3 pipeline that parses historical Sri Lankan datasets, purges invalid entries, and outputs the Genesis Matrix
- **Dual-Telemetry Simulators** — TFE-ib (biophysical) and TFE-gdp (SCADA/industrial) stream generators for all 4 nodes
- **SHACL Validation Gates** — Auto-derived OWL ontology shapes that reject structurally invalid telemetry packets before any ledger contact
- **Bi-Temporal Knowledge Graph** — `valid_time` + `recorded_at` on every graph edge; `graph.state_at()` for point-in-time replay
- **Betweenness Centrality Engine** — C_B calculation over the 4-node Sri Lanka hypergraph
- **Rete Compliance Engine** — Deterministic, non-probabilistic Bad-Neighbor ecological rules and sovereign covenant evaluation
- **S-1 Mint Decision Tracker** — `record_decision()`, `check_decision_rules()`, and `trace_decision_chain()` for every minting and throttle event
- **Next.js Sovereign Dashboard** — Premium web UI with Sigma.js hypergraph, live WebSocket telemetry, Tremor KPI cards, Recharts timelines, and PROV-O lineage explorer
- **W3C PROV-O Audit Export** — Automated Turtle file generation from any minting or compression event
- **4:1 Squeeze Hook Demo** — Live triggered Yield Compression Event from a simulated sensor threshold breach

### 4.2 What Is Out of Scope

The following are post-PoC deliverables and will **not** be built during these 4 weeks:

- Physical Sentinel Hub V.4 and Socket-7 hardware deployment
- Live STOKR Liquid Network mainnet token issuance
- CSSF / SAMA / BCL regulatory submission and legal filing
- Production SRAM PUF silicon fabrication and ML-KEM-768 hardware integration (simulated in PoC)
- ORO Fund SPV legal structuring and CSSF registration

### 4.3 The Four Sri Lanka Critical Resource Nodes

All telemetry is **simulated** using public datasets and synthetic generators calibrated to real Sri Lankan specifications.

---

#### Node 1 — Central Highlands Hydrological Water Tower

- **Location:** Knuckles Range & Central Massif
- **Track:** TFE-ib (biophysical)
- **Live stream:** Upper-catchment baseflow kinetics, topsoil suspension curves, acoustic soil moisture saturation indexes (simulated via Sentinel Hub V.4 enclave model)
- **Forensic ingestion target:** 40 years of daily rainfall registries, mountain run-off logs, and reservoir depth sonar

**Data Sources:**

- [Department of Meteorology — Sri Lanka](http://www.meteo.gov.lk/) — official daily rainfall registries and station observation logs (primary historical baseline)
- [Water Resources Board Sri Lanka](http://www.wrb.gov.lk/) — reservoir depth sonar archives, river run-off gauging station records
- [NOAA Global Historical Climatology Network Daily (GHCNd)](https://www.ncei.noaa.gov/products/land-based-station/global-historical-climatology-network-daily) — 40yr precipitation gap-fill for missing station data
- [NASA POWER API](https://power.larc.nasa.gov/) — daily solar irradiance, temperature, and precipitation reanalysis for Sri Lanka grid cells
- [Global Runoff Data Centre (GRDC)](https://www.bafg.de/GRDC/EN/01_GRDC/grdc_node.html) — mountain discharge historical records for Mahaweli basin tributaries
- [ESA CCI Soil Moisture](https://www.esa-soilmoisture-cci.org/) — topsoil saturation index time series used to calibrate aquifer drawdown velocity (Rule 1 baseline)
- [FAO AQUASTAT](https://www.fao.org/aquastat/en/) — national freshwater resources statistics for ΣE_D coefficient calibration
- [Copernicus Land Service — Soil Water Index](https://land.copernicus.eu/global/products/swi) — near-real-time and historical surface soil moisture for Ω_Threshold calibration

---

#### Node 2 — Kokkilai & Puttalam Lagoon Coastal Blue Carbon Shields

- **Location:** Northern (Kokkilai) and Western (Puttalam) coastal lagoons
- **Track:** TFE-ib (biophysical)
- **Live stream:** Wave kinetic energy dissipation, intertidal tidal surge, vegetative canopy density via neuromorphic SNN ASIC simulation
- **Forensic ingestion target:** 30 years of deltaic bathymetric charts, mangrove baseline maps, and historic storm-surge manifests

**Data Sources:**

- [Global Mangrove Watch — JAXA/EORC](https://www.eorc.jaxa.jp/ALOS/en/dataset/gmw_e.htm) — 30yr mangrove canopy area time series; primary source for C_B calculation at this node
- [OBIS — Ocean Biodiversity Information System](https://obis.org/) — mangrove-dependent species occurrence records for invasive species density baseline (Rule 2)
- [GBIF — Global Biodiversity Information Facility](https://www.gbif.org/) — coastal ecosystem species distribution data for the Northern Province
- [Copernicus Marine Service (CMEMS)](https://marine.copernicus.eu/) — wave kinetic energy profiles, sea level anomalies, and tidal surge historical records for Sri Lankan coastal waters
- [NOAA CoastWatch](https://coastwatch.noaa.gov/) — satellite-derived sea surface temperature and coastal chlorophyll concentration time series
- [Coast Conservation & Coastal Resource Management Dept. Sri Lanka](http://www.coastal.gov.lk/) — storm-surge manifests, coastal erosion surveys, and lagoon boundary legal delineations
- [Blue Carbon Initiative](https://www.thebluecarboninitiative.org/) — mangrove carbon sequestration coefficients used to compute the blue-carbon component of ΣE_D
- [Copernicus Climate Change Service (C3S)](https://climate.copernicus.eu/) — sea level rise projections and storm frequency trends feeding Ω_Threshold calibration

---

#### Node 3 — Eppawala Phosphate & Strata Mining Complexes

- **Location:** North-Central Province, Eppawala
- **Track:** TFE-gdp (SCADA/industrial)
- **Live stream:** RSID vibration and thermodynamic harmonics from extraction mills, weigh-bridge load signatures (simulated via Modbus/TCP SCADA model)
- **Forensic ingestion target:** 20 years of SCADA log streams, automated weigh-bridge manifests, and refinery mass-balance registers

**Data Sources:**

- [Geological Survey & Mines Bureau Sri Lanka (GSMB)](http://www.gsmb.gov.lk/) — 20yr mining licence registers, SCADA log archives, and extraction production records (primary source)
- [USGS National Minerals Information Center — Phosphate Rock](https://www.usgs.gov/centers/national-minerals-information-center/phosphate-rock) — global phosphate reserve statistics used to calibrate the ΣE_D infrastructure lifespan coefficient
- [IFA — International Fertilizer Association](https://www.fertilizer.org/) — global phosphate price indices and production benchmarks for transfer-pricing anomaly detection (Rule 4 analogue)
- [UN Environment Programme — Global Material Flows Database](https://www.unep.org/explore-topics/resource-efficiency/what-we-do/natural-resource-governance) — extraction ecosystem impact baselines for wildfire fuel index and thermodynamic harmonic ±2σ genesis baseline (Rule 3)
- [World Bank Commodity Markets (Pink Sheet)](https://www.worldbank.org/en/research/commodity-markets) — monthly phosphate spot price time series for ΣE_D commodity value floor calibration
- [FAO — Global Soil Partnership](https://www.fao.org/global-soil-partnership/en/) — soil degradation indices used to bound the aquifer drawdown interdependency with Node 1

---

#### Node 4 — Port of Colombo (JCT / CICT Automated Container Terminals)

- **Location:** Colombo, Western Province
- **Track:** TFE-gdp (SCADA/industrial)
- **Live stream:** Crane gantry PLC load weights, container tracking manifests, freight logistics velocity, gate-clearance manifests (shielded within Mu-Metal Faraday cage simulation)
- **Forensic ingestion target:** Shipping bills of lading, port flow meter histories, and international trade customs documentation
- **Key interdependency:** The S-1 Mint algorithm binds Node 4 trade clearance velocity directly to the biophysical risk scores of Nodes 1 and 2 — a drought event in the highlands depresses port throughput within 90 days

**Data Sources:**

- [Sri Lanka Ports Authority (SLPA)](https://www.slpa.lk/) — container throughput statistics, berth occupancy records, gate-clearance manifests (primary source)
- [UNCTAD Maritime Statistics](https://unctadstat.unctad.org/wds/ReportFolders/reportFolders.aspx) — Port of Colombo annual container TEU throughput for ΣE_D trade velocity calibration
- [World Bank — Container Port Traffic Data](https://datacatalog.worldbank.org/search/dataset/0038027) — historical Colombo TEU benchmark series (1990–present)
- [IMO — Global Integrated Shipping Information System (GISIS)](https://gisis.imo.org/) — vessel registration, cargo manifests, and port state control inspection records
- [MarineTraffic AIS Historical Data](https://www.marinetraffic.com/) — vessel movement data for freight velocity simulation and gate-clearance anomaly detection
- [John Keells Holdings (JCT Operator)](https://www.johnkeells.com/) — JCT terminal operational benchmarks and throughput reports (public annual reports)
- [China Merchants Port Holdings (CICT Operator)](https://www.cmport.com.hk/) — CICT terminal capacity, crane utilisation rates, and container dwell time statistics
- [Sri Lanka Customs — Trade Statistics](https://www.customs.gov.lk/) — import/export declaration data and bill of lading cross-reference for PLC load weight anomaly detection (Rule 4)

---

## 5. System Architecture

### 5.1 Data Flow

```
[Public + Synthetic Sri Lanka Data]
          │
          ▼
┌─────────────────────────────┐
│  LayoutLMv3 Clean Room      │  ← containerised, Docker Compose
│  40yr forensic ingest       │
│  → Genesis Matrix (Parquet) │
└────────────┬────────────────┘
             │
      ┌──────┴───────┐
      ▼              ▼
┌──────────────┐  ┌──────────────┐
│  TFE-ib Sim  │  │ TFE-gdp Sim  │
│  Nodes 1 & 2 │  │ Nodes 3 & 4  │
└──────┬───────┘  └──────┬───────┘
       └──────┬──────────┘
              ▼
   ┌───────────────────────┐
   │  SHACL Ingestion Gate │  ← drops bad packets here
   └──────────┬────────────┘
              ▼
   ┌───────────────────────────┐
   │  Semantica Knowledge Graph│
   │  ├─ Bi-Temporal Engine    │
   │  ├─ Centrality Engine     │
   │  ├─ Rete Rule Engine      │
   │  └─ ProvenanceManager     │
   └──────┬──────────┬─────────┘
          │          │
   record_decision  PROV-O export
          ▼          ▼
   ┌────────────┐  ┌──────────────────────┐
   │  Dashboard │  │ sir_audit_trail.ttl  │
   │  FastAPI + │  │ W3C PROV-O Turtle    │
   │  Streamlit │  └──────────────────────┘
   └─────┬──────┘
         │ /mint-trigger
         ▼
   ┌────────────────┐
   │ STOKR TaaS Stub│  ← mock endpoint in PoC
   └────────────────┘
```

### 5.2 Technology Stack

#### Backend

- **Document parsing** — LayoutLMv3 (Hugging Face), Docker
- **Knowledge graph** — Semantica ContextGraph + TemporalKnowledgeGraph
- **Validation** — SHACL shapes (pySHACL), OWL ontology (rdflib)
- **Reasoning** — Semantica ReteEngine (deterministic, zero-LLM)
- **Provenance** — Semantica ProvenanceManager + RDFExporter
- **Graph algorithms** — Semantica CentralityCalculator (C_B)
- **API layer** — FastAPI (Python) with WebSocket support (`/ws/telemetry`, `/ws/events`)
- **Data simulation** — NumPy, Pandas, synthetic generators
- **Containerisation** — Docker Compose
- **Testing** — pytest (unit + integration), locust (load)

#### Frontend — Sovereign Intelligence Dashboard

- **Framework** — [Next.js 14](https://nextjs.org/) (App Router, TypeScript, SSR + client components)
- **Styling** — [Tailwind CSS](https://tailwindcss.com/) + [shadcn/ui](https://ui.shadcn.com/) component primitives
- **Dashboard components** — [Tremor](https://www.tremor.so/) for KPI cards, sparklines, area charts, and progress bars
- **Sovereign hypergraph** — [Sigma.js](https://www.sigmajs.org/) + [Graphology](https://graphology.github.io/) for the force-directed 4-node knowledge graph and the PROV-O lineage DAG explorer
- **Time-series charts** — [Recharts](https://recharts.org/) for node telemetry timelines, C_B trend lines, and Ω_Threshold history
- **Live data** — Native WebSocket client (`/ws/telemetry`, `/ws/events`) for real-time telemetry push from FastAPI — no polling
- **Animations** — [Framer Motion](https://www.framer.com/motion/) for collateral ratio transitions, breach alerts, and panel state changes

---

## 6. 4-Week Delivery Plan

> **Timeline:** July 1 – July 28, 2026 · **20 working days** · Hard milestone at end of each week

---

### Week 1 — Foundation, Data & Ingestion

**July 1–4 · 4 days**

**Goal:** The skeleton runs. All four nodes have synthetic data flowing through the ingestion pipeline and SHACL is catching bad packets.

#### Day 1–2 · Environment & Data Setup

- [ ] Initialise monorepo folder structure: `/ingestion`, `/graph`, `/reasoning`, `/api`, `/dashboard`, `/tests`
- [ ] Docker Compose stack up: LayoutLMv3 service · Semantica service · FastAPI service · Streamlit service
- [ ] Generate synthetic telemetry datasets for all 4 nodes:
  - Node 1: 40yr daily rainfall time-series (CSV), reservoir depth sonar logs
  - Node 2: 30yr bathymetric depth charts, mangrove canopy density index
  - Node 3: 20yr SCADA vibration logs in Modbus/TCP format simulation
  - Node 4: Port manifest records, PLC crane load weights, gate-clearance records
- [ ] Seed with public data where available — NOAA, Copernicus Level-2, UN FAO open datasets

#### Day 3–4 · Ingestion Clean Room + SHACL Gates

- [ ] Containerise LayoutLMv3 document parsing pipeline
- [ ] Build `ingestion/cleanroom.py` — ingests CSVs and PDFs, purges anomalous entries, outputs Genesis Matrix as Parquet
- [ ] Define OWL ontology for TFE entity types: biophysical node, industrial node, telemetry reading, threshold event
- [ ] Auto-derive SHACL shapes from the ontology (`ingestion/shacl_gates.py`)
- [ ] SHACL gate behaviour: any out-of-range packet generates a plain-English validation report and is dropped before graph contact
- [ ] Unit tests: inject 10 deliberately corrupted packets → assert all 10 rejected

**Week 1 Exit Gate:**

- [ ] All 4 node datasets loaded and versioned in `/data`
- [ ] LayoutLMv3 cleanroom producing a valid Genesis Matrix with no tampered entries
- [ ] SHACL gate demonstrably rejecting malformed telemetry on every run
- [ ] `docker compose up` starts all services clean with no errors

---

### Week 2 — Knowledge Graph, Temporal Engine & Centrality

**July 7–11 · 5 days**

**Goal:** The 4-node Sri Lanka hypergraph is live. Bi-temporal state replay works at any historical date. Betweenness Centrality fires in sub-millisecond time.

#### Day 5–6 · Bi-Temporal Knowledge Graph

- [ ] Initialise `ContextGraph(advanced_analytics=True)` with 4 nodes and inter-node edges
- [ ] Tag every graph edge with `valid_time` (when the fact was true in the world) and `recorded_at` (when it was ingested)
- [ ] Implement `graph.state_at("YYYY-MM-DD")` — reconstruct the full 4-node hypergraph as of any past date
- [ ] Load Genesis Matrix into graph (40yr baseline for Node 1, 30yr for Node 2, 20yr for Nodes 3 & 4)
- [ ] Implement Allen Interval Algebra anomaly detection: flag `overlaps`, `during`, and `meets` timing anomalies in historical SCADA logs
- [ ] Test: `graph.state_at("1990-01-01")` returns a valid non-empty graph; delta between 1990 and 2024 is non-empty and structurally correct

#### Day 7–8 · Betweenness Centrality Engine

- [ ] Implement `CentralityCalculator` over the 4-node hypergraph
- [ ] Compute C_B for each node — quantifying each node's geostrategic routing density within the sovereign hypergraph
- [ ] Implement Downstream Asset Exposure (ΣE_D): hardcode port throughput velocity (Node 4) and catchment recharge contribution (Node 1) as E_D values
- [ ] Implement the live SIU valuation formula:

```python
siu_adjusted = f(C_B * sum_E_D) * (1 - omega_threshold)
```

- [ ] Implement incremental delta updates: new telemetry patches the graph without a full rebuild
- [ ] Benchmark: C_B calculation over the 4-node graph must complete in < 50ms

#### Day 9 · Provenance Binding

- [ ] Implement `ProvenanceManager` — every ingested fact is bound to its source document, DOI, author, page number, and confidence score
- [ ] Implement `trace_lineage()` — walks the full multi-hop ancestor chain from any SIU metric back to the originating data source
- [ ] Bind Node 2 coastal data to a synthetic OBIS biodiversity record with DOI metadata
- [ ] Bind Node 3 SCADA data to a synthetic mass-balance register with extraction authority metadata
- [ ] Unit test: `prov.get_lineage("node1_highland_recharge")` returns a complete 3-hop chain to the source file

**Week 2 Exit Gate:**

- [ ] `graph.state_at("2010-01-01")` and `graph.state_at("2024-01-01")` return distinct, structurally correct graph states
- [ ] C_B computed for all 4 nodes, confirmed sub-50ms
- [ ] `SIU_adjusted` formula computing live against real graph state
- [ ] Full provenance chain traced for at least one fact per node (4 nodes total)

---

### Week 3 — Rete Compliance Engine, Mint Logic & Squeeze Hook

**July 14–18 · 5 days**

**Goal:** The policy brain is live. Minting is gated by deterministic rules. The 4:1 squeeze fires within 100ms of any threshold breach.

#### Day 10–11 · Rete Network Rule Compilation

Compile the full Bad-Neighbor rule library into `ReteEngine` with no LLM calls anywhere in the path:

- [ ] **Rule 1** — Reject any node where aquifer drawdown velocity exceeds the recharge rate (Node 1)
- [ ] **Rule 2** — Reject any node where invasive species density is flagged in the mangrove perimeter (Node 2)
- [ ] **Rule 3** — Reject any SCADA stream where thermodynamic harmonics fall outside ±2σ of the genesis baseline (Node 3)
- [ ] **Rule 4** — Flag any port manifest where PLC load weight vs. bill of lading weight diverges by > 3% (Node 4)
- [ ] **Rule 5** — Reject any biophysical node where the wildfire fuel continuity index breaches the critical threshold
- [ ] **Covenant Rule** — No SIU-T minting above 50% of the SIU parent reserve (2:1 over-collateralisation lock enforced at every mint call)
- [ ] Implement `ReteEngine.evaluate(telemetry_packet)` → `{approved: bool, failing_rule: str | None}`
- [ ] Test: 5 compliant packets → all pass; 5 non-compliant packets → all fail with the correct named rule

#### Day 12–13 · S-1 Mint Decision Engine

- [ ] Implement `graph.record_decision()`:

```python
decision_id = graph.record_decision(
    category="s1_sovereign_mint",
    outcome="mint_siu_t",
    confidence=0.98,
    rationale="Baseline biophysical conditions satisfied. All 4 nodes stable.",
    entities=["node1_highland", "node2_coastal", "node3_mining", "node4_port"],
)
```

- [ ] Implement `graph.check_decision_rules(decision_id, ruleset="sir_v4_2_compliance")` — runs Rete evaluation and binds the result to the decision object
- [ ] Implement `graph.trace_decision_chain(decision_id)` — reconstructs the complete causal path backward through the graph to the originating sensor values
- [ ] Enforce the 2:1 over-collateralisation lock at mint time: `SIU-T_supply ≤ 0.5 × SIU_parent_reserve`
- [ ] Blocked minting: if Rete returns `approved=False`, raise a structured error containing `failing_rule` and the full causal path object

#### Day 14 · 4:1 Yield Compression Event

- [ ] Implement `Ω_Threshold` sensor monitor: simulates threshold breach (e.g. Node 1 aquifer drawdown velocity spike)
- [ ] Implement the Rete-triggered Yield Compression Event:
  - Ω_Threshold crosses Ω_Crit → Rete fires immediately with no delay
  - `record_decision(category="yield_compression", outcome="squeeze_4_1")` creates an immutable causal object
  - Compression state pushed to STOKR TaaS stub endpoint `/collateral-squeeze`
  - Collateral lock scales from 2:1 to 4:1 on the circulating SIU-T supply
- [ ] Implement `trace_decision_chain()` on the squeeze event — returns the exact sensor coordinates and threshold values that triggered the breach
- [ ] End-to-end test: inject Node 1 breach → Rete fires in < 100ms → 4:1 lock confirmed → causal chain fully reconstructable

**Week 3 Exit Gate:**

- [ ] All 5 Bad-Neighbor rules plus the covenant rule enforce deterministically — zero LLM calls in the compliance path
- [ ] Minting is blocked correctly whenever any rule fails
- [ ] Yield Compression Event fires and locks 4:1 within 100ms of the breach signal
- [ ] `trace_decision_chain()` returns a complete causal path for both mint and squeeze events

---

### Week 4 — Dashboard, PROV-O Export, Integration Testing & Demo Polish

**July 21–25 · 5 days**

**Goal:** Everything is wired end-to-end. The 9-step demo loop runs cleanly from cold start. PROV-O Turtle export is valid. The system is presentation-ready.

#### Day 15–16 · Next.js Sovereign Intelligence Dashboard

Build `dashboard/` as a Next.js 14 App Router project. All 8 panels consume live data via WebSocket or REST — zero mocked state in the UI.

**Panel 1 — Sovereign Hypergraph (`HypergraphView.tsx`)**

- [ ] Sigma.js + Graphology force-directed graph of all 4 Sri Lanka nodes
- [ ] Node size = C_B weight; node color = health status (green / amber / red); edge thickness = interdependency strength
- [ ] Click any node → right-side flyout drawer showing live telemetry stream, C_B value, ΣE_D contribution, and Ω_Threshold reading for that node
- [ ] Animate node color transition on threshold breach (smooth Framer Motion pulse)

**Panel 2 — SIU Valuation (`SIUValuationCard.tsx`)**

- [ ] Tremor KPI card with animated counter showing live `SIU_adjusted`
- [ ] 24hr sparkline beneath the main figure
- [ ] Donut chart (Recharts) breaking down each node's C_B contribution to the final value
- [ ] Ω_Threshold radial gauge — sweeps red as the value approaches Ω_Crit

**Panel 3 — Collateral Ratio (`CollateralGauge.tsx`)**

- [ ] Large animated ratio badge: `2:1` (white on dark green) or `4:1` (white on red) with Framer Motion spring transition on squeeze
- [ ] SIU-T circulating supply progress bar vs SIU parent reserve floor (Tremor)
- [ ] Countdown timer showing seconds since last compression event

**Panel 4 — PROV-O Lineage Explorer (`ProvenanceGraph.tsx`)**

- [ ] Second Sigma.js instance rendering the provenance DAG for the currently selected minting decision
- [ ] Click any DAG node → tooltip showing entity IRI, source DOI, author, page number, and confidence score
- [ ] One-click `.ttl` export button wired to `GET /audit/{entity_id}`

**Panel 5 — Node Telemetry Timeline (`NodeTelemetry.tsx`)**

- [ ] Recharts multi-line chart per node showing key sensor metric vs historical baseline
- [ ] Threshold breach markers rendered as vertical red lines on the timeline
- [ ] Date range selector: 7d / 30d / 1yr / genesis

**Panel 6 — Compression Event Feed (`CompressionFeed.tsx`)**

- [ ] Real-time WebSocket push from `/ws/events` — no manual refresh
- [ ] Color-coded rows: red for active squeeze, amber for restoring, green for baseline
- [ ] Expandable causal chain view per event showing the full `trace_decision_chain()` output

**Panel 7 — Mint Decision Feed (`MintFeed.tsx`)**

- [ ] Live WebSocket feed of all mint and block decisions
- [ ] Green `APPROVED` badge or red `BLOCKED — {failing_rule}` badge per row
- [ ] Click decision ID → opens PROV-O Lineage Explorer (Panel 4) for that decision

**Panel 8 — Trigger Control Panel (`TriggerPanel.tsx`)**

- [ ] Node breach buttons: one per node (Node 1–4) wired to `POST /simulate/breach`
- [ ] Restore Baseline button wired to `POST /simulate/restore`
- [ ] WebSocket connection status indicator (green dot / red dot) in the header

#### Day 17 · W3C PROV-O Audit Export

- [ ] Implement `RDFExporter.export(lineage, output_path, format="turtle")`
- [ ] Each exported file must include: entity IRI, source DOI, author, page number, PUF fingerprint flag, ML-KEM encapsulation flag, and confidence score
- [ ] One-click export from the dashboard → generates `sir_sovereign_audit_trail.ttl`
- [ ] Validate: the Turtle file parses with zero errors in rdflib and contains `prov:Entity`, `prov:wasDerivedFrom`, `prov:wasAttributedTo`, and `prov:generatedAtTime` triples
- [ ] Generate and validate exports for all 4 nodes' lineage and the most recent minting decision

#### Day 18 · FastAPI Integration + STOKR TaaS Stub

Finalise all endpoints in `api/main.py`:

- [ ] `POST /ingest` — accepts a telemetry packet, runs SHACL, loads to graph
- [ ] `GET /siu-value` — returns live `SIU_adjusted` with full C_B, ΣE_D, and Ω breakdown
- [ ] `GET /compliance/{decision_id}` — returns Rete result and causal chain for a given decision
- [ ] `POST /mint` — records a mint decision, checks all rules, returns approved or blocked with failing rule
- [ ] `GET /audit/{entity_id}` — returns the full provenance lineage for a given entity
- [ ] `GET /graph/state?date=YYYY-MM-DD` — returns the bi-temporal graph snapshot at a given date
- [ ] `POST /simulate/breach` — injects a threshold breach on a specified node

Build `api/stokr_stub.py`:

- [ ] Logs all incoming mint triggers and collateral squeeze signals with timestamps
- [ ] Document all endpoints with OpenAPI schema auto-generated by FastAPI

#### Day 19 · End-to-End Integration Testing

Run the full 9-step demo loop and fix all failures before Day 20:

1. **Cold start** — Genesis Matrix loads, all 4 nodes appear in the graph
2. **Live stream** — 10 packets per node injected; 2 corrupted per node → SHACL rejects all 8 bad packets
3. **Centrality** — C_B computed; `SIU_adjusted` value updates live in the dashboard
4. **Mint** — `POST /mint` for Node 4 (Port of Colombo) → approved → STOKR stub receives the signal
5. **Breach** — `POST /simulate/breach?node=1` triggers a Node 1 aquifer drawdown event
6. **Squeeze** — Dashboard shows 4:1 lock within 100ms; collateral ratio updates in real time
7. **Causal chain** — `trace_decision_chain()` returns exact sensor coordinates and breach values
8. **Audit export** — PROV-O Turtle file generated, validated, and downloadable from the dashboard
9. **Time replay** — `GET /graph/state?date=1990-01-01` returns the correct 1990 hypergraph

- [ ] Fix all integration failures surfaced during the run
- [ ] Performance test: 100 concurrent telemetry packets through SHACL + graph in < 5 seconds

#### Day 20 · Demo Hardening & Documentation

- [ ] Freeze the demo scenario script — exact click sequence for the presentation
- [ ] Pre-seed the graph with the full 40yr Genesis Matrix so the demo starts instantly with no load lag
- [ ] Capture backup screenshots of every panel in case of live demo network issues
- [ ] Write `DEMO_SCRIPT.md` — exact steps, expected outputs, and talking points for every screen
- [ ] Final build test: `docker compose up --build` from a clean environment → all services green within 3 minutes

---

## 7. Deliverables Matrix

| # | Deliverable | Owner | Due | Acceptance Criteria |
|---|---|---|---|---|
| D1 | Genesis Matrix — 4 nodes, synthetic + public data | Kaif | Jul 4 | LayoutLMv3 cleanroom produces valid Parquet; no tampered entries pass |
| D2 | SHACL Ingestion Gate | Kaif | Jul 4 | 100% of injected corrupted packets rejected before graph contact |
| D3 | Bi-Temporal Knowledge Graph — 4 Sri Lanka nodes | Kaif | Jul 11 | `graph.state_at()` returns distinct valid snapshots for 1990, 2010, 2024 |
| D4 | Betweenness Centrality Engine | Kaif | Jul 11 | C_B computed for all 4 nodes in < 50ms; `SIU_adjusted` formula live |
| D5 | Provenance Manager — per-claim source attribution | Kaif | Jul 11 | `trace_lineage()` returns ≥ 3-hop chain to DOI for each node |
| D6 | Rete Compliance Engine — 5 rules + covenant | Kaif | Jul 18 | All rules fire deterministically; zero LLM calls in the compliance path |
| D7 | S-1 Mint Decision Tracker | Kaif | Jul 18 | `record_decision()` + `check_decision_rules()` + `trace_decision_chain()` all working |
| D8 | 4:1 Yield Compression Event | Kaif | Jul 18 | Breach → squeeze lock in < 100ms; full causal chain reconstructable |
| D9 | Next.js Sovereign Dashboard — 8 panels (Sigma.js + Tremor + Recharts) | Kaif | Jul 23 | All panels render live WebSocket data; breach/restore buttons trigger real graph state changes; Sigma.js hypergraph interactive |
| D10 | W3C PROV-O Turtle Export | Kaif | Jul 23 | Valid `.ttl` file with all required PROV-O triples for every minting event |
| D11 | FastAPI Backend — 7 endpoints | Kaif | Jul 24 | All endpoints return correct responses; OpenAPI schema published |
| D12 | End-to-End Demo Loop | Kaif | Jul 25 | All 9 steps run clean from cold start |
| D13 | DEMO_SCRIPT.md | Kaif | Jul 25 | Step-by-step script with expected outputs for each action |
| D14 | Docker Compose Package | Kaif | Jul 25 | `docker compose up` starts all services green in < 3 minutes |

---

## 8. Financial Calibration Baseline

The following values are hardcoded in the PoC tokenomics dashboard to represent the Sri Lanka case study at sovereign scale.

### Capital Structure

- **Phase 0 Fixed Deposit** — USD 100,000 (node mapping)
- **Multi-Country Pool Contribution** — ~USD 1,500,000
- **Multi-Country Pool Total** — USD 150,000,000
- **AMM Pool Scale by Day 120** — USD 500,000,000

### SIU Reserve & Yield

- **Annually Underwritten SIU Reserve Floor** — USD 24,000,000,000
- **Circulating SIU-T Liquidity Limit (2:1 lock)** — USD 12,000,000,000
- **Annual Gross Integrity Yield Rate** — 10% of TVL
- **Annual Gross Value Generated** — USD 2,400,000,000

### Waterfall Distribution

- **Sovereign Net Prosperity Allocation (75%)** — USD 1,800,000,000
  - 56% Net Liquid Treasury Payout → Central Bank of Sri Lanka: **USD 1,344,000,000**
  - 15% Hardware Refresh Escrow Vault: USD 360,000,000
  - 4% Parametric Insurance Wrap: USD 96,000,000

- **Institutional Pool Allocation (25%)** — USD 600,000,000
  - 3% Local Partner Carve-Out: USD 72,000,000
  - Tech Fee Sliding Scale: USD 528,000,000

### STOKR Volume-Weighted Fee Schedule

- **Tier 1 — Pilot** (USD 0 – 500M): 5.0% success fee
- **Tier 2 — Scale** (USD 500M – 50B): 2.5% success fee
- **Tier 3 — National** (USD 50B – 500B): 1.5% success fee
- **Tier 4 — Systemic** (USD 500B+): 0.5% – 1.0% success fee

---

## 9. Success Criteria & Acceptance Gates

### Binary Gates — PoC Fails If Any Of These Are Not Met

- **G1 — Deterministic compliance:** 1,000 Rete evaluations on identical inputs produce identical results with zero variance
- **G2 — Zero LLM in compliance path:** grep or trace confirms no LLM API call is made during any SHACL check or Rete evaluation
- **G3 — Squeeze fires < 100ms:** benchmark confirms node breach signal to 4:1 collateral lock in < 100ms at p99
- **G4 — Causal chain complete:** `trace_decision_chain()` traces every squeeze event back to the originating sensor node, timestamp, and breach value
- **G5 — PROV-O valid:** generated `.ttl` file parses with zero errors in rdflib and contains `prov:Entity`, `prov:wasDerivedFrom`, and `prov:wasAttributedTo` triples
- **G6 — Bi-temporal replay:** `graph.state_at("1990-01-01")` and `graph.state_at("2024-01-01")` return distinct, non-empty, structurally correct graphs
- **G7 — SHACL gate:** 100% of intentionally corrupted test packets are rejected before touching the knowledge graph

### Quality Targets — Tracked But Not Blockers

- C_B calculation over the 4-node graph: **< 50ms**
- SHACL validation latency per packet: **< 10ms**
- WebSocket telemetry push to dashboard UI: **≤ 200ms** end-to-end
- Sigma.js hypergraph initial render (4 nodes): **< 500ms**
- Next.js page initial load (cold): **< 2 seconds** (Lighthouse score ≥ 90)
- Docker cold-start to all-green: **< 3 minutes**
- End-to-end 9-step demo loop: **< 8 minutes**

---

## 10. Risk Register

### Risk 1 — LayoutLMv3 inference too slow for 40yr forensic ingest (Week 1)

- Probability: Medium · Impact: High
- Mitigation: Pre-process source documents to structured CSV; use LayoutLMv3 only for PDFs with complex layout structures

### Risk 2 — Semantica SDK surface differs from co-dev spec

- Probability: Medium · Impact: High
- Mitigation: Kaif confirms SDK availability on Day 1; build a thin adapter layer if the interface diverges

### Risk 3 — Synthetic data insufficiently matches Sri Lanka geophysical reality

- Probability: Low · Impact: Medium
- Mitigation: Use NOAA and Copernicus Level-2 open data as the floor; synthetic generation only for gap-fill

### Risk 4 — C_B computation does not hit the 50ms target

- Probability: Low · Impact: Medium
- Mitigation: 4-node graph is trivially fast; performance complexity only emerges at 10,000+ node scale; pre-compute and cache if needed

### Risk 5 — Next.js dashboard WebSocket drops or Sigma.js render stalls under high event rate

- Probability: Low · Impact: Low
- Mitigation: Throttle WebSocket broadcast to 10 events/sec on the FastAPI side; use Graphology's incremental graph mutation API (never rebuild the full graph object on each update)

### Risk 6 — Squeeze hook timing misses the 100ms SLA (Week 3)

- Probability: Medium · Impact: Medium
- Mitigation: Pre-compile the entire Rete ruleset at startup; never recompile on each evaluation call

---

## 11. Team & Responsibilities

### Kaif Ahmad — Lead Engineer

- Owns the full stack: ingestion pipeline, knowledge graph, reasoning engine, API, dashboard, and test suite
- Primary point of contact for all Day-1 to Day-20 engineering deliverables

### TFE Lead Architect — Systems Architect

- Defines hardware telemetry specifications, edge enclave data contracts, and node schema validation rules
- Reviews and signs off on the dual-telemetry simulator data contracts

### Mohd Mohd — Semantica Founder

- Provides Semantica SDK guidance, SHACL/Rete configuration, and PROV-O export specification
- Approves the graph architecture and provenance binding approach

### Tizian Rotermund & Egor Sukhanov — STOKR Integration

- Define the TaaS stub API schema, Blockstream AMP integration spec, and CSSF compliance requirements
- Review the STOKR endpoint contract on Day 18

### Mustafa — Demo Stakeholder

- Final demo approval and sovereign pilot acceptance criteria
- Attends the Week 4 rehearsal on July 24 and demo day on July 25

### Weekly Communication Cadence

- **Daily engineering standup** (Weeks 1–4) — 15 minutes, async if needed
- **Architecture gate review** (end of each week) — 30-minute live call with demo of that week's deliverables
- **Final demo rehearsal** — July 24, full 9-step run-through with all stakeholders present
- **Demo day** — July 25, Mustafa + full team

---

## Appendix A — Repository Structure

```
sir-poc/
├── docker-compose.yml
│
├── backend/
│   ├── ingestion/
│   │   ├── cleanroom.py          # LayoutLMv3 forensic ingest pipeline
│   │   ├── shacl_gates.py        # SHACL shape validation and packet rejection
│   │   └── ontology.ttl          # TFE node OWL ontology
│   ├── graph/
│   │   ├── context_graph.py      # Semantica ContextGraph wrapper
│   │   ├── temporal_graph.py     # Bi-temporal KG + Allen Interval Algebra
│   │   └── centrality.py         # Betweenness Centrality engine
│   ├── reasoning/
│   │   ├── rete_engine.py        # Deterministic Rete rule compilation
│   │   ├── rules/
│   │   │   ├── bad_neighbor.py   # Ecological liability rules (Rules 1–5)
│   │   │   └── covenants.py      # Sovereign debt covenant rules
│   │   └── decision_tracker.py   # record_decision + trace_decision_chain
│   ├── provenance/
│   │   ├── manager.py            # ProvenanceManager
│   │   └── exporter.py           # RDFExporter → W3C PROV-O Turtle
│   ├── api/
│   │   ├── main.py               # FastAPI (7 REST endpoints + 2 WebSocket routes)
│   │   └── stokr_stub.py         # STOKR TaaS mock endpoint
│   └── data/
│       ├── node1_highland/       # Synthetic hydrological time-series data
│       ├── node2_coastal/        # Synthetic coastal blue-carbon data
│       ├── node3_mining/         # Synthetic SCADA and phosphate extraction data
│       └── node4_port/           # Synthetic port logistics and manifest data
│
├── dashboard/                    # Next.js 14 App Router (TypeScript)
│   ├── app/
│   │   ├── layout.tsx            # Root layout — Tailwind, shadcn theme provider
│   │   ├── page.tsx              # Main dashboard (all 8 panels)
│   │   ├── graph/
│   │   │   └── page.tsx          # Full-screen sovereign hypergraph view
│   │   └── audit/
│   │       └── [id]/page.tsx     # PROV-O lineage explorer for a decision ID
│   ├── components/
│   │   ├── HypergraphView.tsx    # Sigma.js + Graphology 4-node force-directed graph
│   │   ├── ProvenanceGraph.tsx   # Sigma.js PROV-O lineage DAG explorer
│   │   ├── SIUValuationCard.tsx  # Tremor KPI card + Recharts donut + Ω gauge
│   │   ├── CollateralGauge.tsx   # Framer Motion 2:1 / 4:1 ratio badge + progress bar
│   │   ├── NodeTelemetry.tsx     # Recharts multi-line timeline with breach markers
│   │   ├── CompressionFeed.tsx   # WebSocket live compression event log
│   │   ├── MintFeed.tsx          # WebSocket live mint decision feed
│   │   └── TriggerPanel.tsx      # Breach simulation + restore buttons
│   ├── lib/
│   │   ├── api.ts                # Typed FastAPI REST client (fetch wrappers)
│   │   └── ws.ts                 # WebSocket manager with reconnect logic
│   ├── tailwind.config.ts
│   ├── next.config.ts
│   └── package.json              # sigma.js, graphology, @tremor/react, recharts,
│                                 #   framer-motion, shadcn/ui, tailwindcss
│
├── tests/
│   ├── test_shacl.py
│   ├── test_rete.py
│   ├── test_temporal.py
│   ├── test_provenance.py
│   └── test_e2e.py
└── DEMO_SCRIPT.md
```

---

## Appendix B — Key Code Contracts

### Minting Decision

```python
decision_id = graph.record_decision(
    category="s1_sovereign_mint",
    outcome="mint_siu_t",
    confidence=0.98,
    rationale="Baseline biophysical conditions satisfied. All 4 nodes stable.",
    entities=["node1_highland", "node2_coastal", "node3_mining", "node4_port"],
)

compliance = graph.check_decision_rules(decision_id, ruleset="sir_v4_2_compliance")
if not compliance.approved:
    raise ValueError(f"S-1 Minting Blocked: {compliance.failing_rule}")

causal_chain = graph.trace_decision_chain(decision_id)
```

### Temporal Replay

```python
graph = TemporalKnowledgeGraph(enable_allen_algebra=True)

snapshot_1990 = graph.state_at("1990-01-01")
snapshot_2024 = graph.state_at("2024-01-01")
delta = graph.compute_delta(snapshot_1990, snapshot_2024)
```

### Provenance Export

```python
prov = ProvenanceManager(storage_path="./sir_audit_trail.db")

prov.track_entity(
    "node1_highland_recharge",
    source="sri_lanka_hydrology_board_2024.pdf",
    metadata={
        "doi": "10.xxxx/slhydro.2024.001",
        "page": 42,
        "author": "Sri Lanka Water Resources Board",
        "confidence": 0.95,
    },
)

lineage = prov.get_lineage("node1_highland_recharge")
RDFExporter().export(lineage, "sir_sovereign_audit_trail.ttl", format="turtle")
```

---

*Next action: Kaif to confirm Semantica SDK access and begin Day 1 environment setup on July 1, 2026.*
