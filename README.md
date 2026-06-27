# SIR V.4.2 × Semantica — Proof of Concept

**Document ID:** SEM-TFE-POC-2026-V2.0
**Date:** June 27, 2026
**Classification:** RESTRICTED — CO-DEVELOPMENT BRIEF
**Prepared By:** Semantica Engineering / Joint Systems Architecture
**Jurisdictions:** State of Kuwait AND Kingdom of Saudi Arabia

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

**Two sovereign case studies are demonstrated in parallel: the State of Kuwait and the Kingdom of Saudi Arabia.** Each country contributes four Critical Resource Nodes — eight nodes total across the PoC — drawn directly from the Phase 0 Core-Node activation specifications in the SIR V.4.2 Master Proposals for each sovereign.

The PoC demonstrates that raw biophysical and industrial telemetry from these eight nodes can be converted into auditable, legally defensible **Sovereign Integrity Units (SIUs)** — assets structured to qualify as Tier-1 High-Quality Liquid Assets (HQLA) on the respective central bank balance sheets: the Central Bank of Kuwait (CBK) and the Saudi Central Bank (SAMA).

**The PoC must be fully functional and demo-ready in 28 working days.** It produces a running system with 16 named deliverables — not a slide deck.

---

## 2. Problem Statement

### 2.1 The Accountability Gap in Sovereign Asset Minting

When a central bank ingests national natural assets onto its balance sheet to satisfy Tier-1 HQLA reserve criteria, every financial figure and every programmatic decision must be **legally underwritable and mathematically defensible**. The current landscape fails on three axes:

- **Traceability gap** — Standard RAG pipelines synthesize documents probabilistically. The synthesis path is invisible. Auditors cannot reconstruct the chain from a token valuation back to the raw sensor reading that caused it.

- **Compliance enforcement gap** — Probabilistic LLM reasoning is used to evaluate regulatory rules. Results are inconsistent between runs, non-repeatable under audit, and legally indefensible in court.

- **Temporal integrity gap** — Legacy systems use flat changelogs with no bi-temporal tracking. There is no mechanism to prove a historical baseline was untampered, and no way to replay the state of the world as it was on a specific past date.

### 2.2 The Specific Problem for Kuwait

Kuwait holds four high-value natural and industrial asset classes that are currently **unmonetized on the Central Bank balance sheet**:

- **Kuwait Bay intertidal eco-buffer** — hyper-saline shallow shelf ecosystems flanking the northern industrial approach arcs
- **Dammam Aquifer Matrix** — strategic subterranean fresh and brackish water columns regulating industrial cooling and desalination intake
- **Mina Al-Ahmadi refinery complex** — main crude export pipeline headers, refinery blending manifolds, and SCADA custody transfer networks
- **Al-Zour Mega-Scale Desalination** — primary seawater intake manifolds and high-pressure pump distributions for national freshwater supply

No existing system can convert the raw biophysical and industrial reality of these nodes into a financially auditable, legally compliant reserve instrument. Without a verifiable middleware layer:

- No international rating agency will underwrite the SIU reserve
- No clearinghouse will accept the 4:1 collateral squeeze hook as legally mandated
- No regulator will accept the compliance audit without a deterministic, machine-readable lineage trail

### 2.3 The Specific Problem for Saudi Arabia

Saudi Arabia holds four high-value sovereign asset classes that are currently **unmonetized on the SAMA balance sheet**:

- **Red Sea coastal eco-shield** — critical intertidal coral-mangrove protective shield flanking the NEOM/Giga-project coastal approach arcs and deep shipment corridors
- **Wajid/Minjur Aquifer Plenum** — deep fossil water columns regulating regional agricultural extraction and industrial utility drawdowns across the Eastern Province
- **Jubail Industrial City complex** — primary pipeline collection manifolds, automated cracking plant arrays, and refinery blending manifold headers
- **Port of King Abdullah (Rabigh)** — automated container gantry terminal crane networks and deep-water logistics clearance

The same accountability gaps that apply to Kuwait apply here at larger scale. Saudi Arabia's $20B initial TVL floor (Year 1) is the largest single-country SIU deployment in the IPCC network, making the veracity middleware more critical, not less.

### 2.4 Why This PoC Is Necessary Now

This PoC proves — in running code against real Kuwait and Saudi Arabian datasets — three things:

1. Semantica's deterministic reasoning layer can sit between TFE edge hardware and STOKR's Liquid Network ledger and produce a legally defensible minting signal **for both sovereign configurations simultaneously**
2. The resulting SIU minting decision is unbribable, fully auditable, and W3C PROV-O compliant for each jurisdiction independently
3. The 4:1 Yield Compression Event fires with zero probabilistic dependency — no LLM in the loop — for both the CBK and SAMA configurations

---

## 3. Solution Overview

### 3.1 Three-Layer Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    TFE EDGE HARDWARE LAYER                      │
│  Sentinel Hub V.4 (biophysical) + Socket-7 Gateways (SCADA)    │
│  SRAM PUF silicon fingerprinting + ML-KEM-768 encryption        │
│  [Kuwait: 4 nodes] + [Saudi Arabia: 4 nodes]                    │
└────────────────────────────┬────────────────────────────────────┘
                             │  Post-Quantum Encrypted Stream
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│               SEMANTICA VERACITY LAYER  ← this PoC              │
│                                                                 │
│  ├─ SHACL Ingestion Gates (KWT + SAU country schemas)           │
│  ├─ LayoutLMv3 Forensic Clean Rooms (per country)               │
│  ├─ Bi-Temporal Knowledge Graphs (KWT hypergraph + SAU hypergraph)│
│  ├─ Betweenness Centrality Engines (per graph)                  │
│  ├─ Rete Network Compliance Rules (KWT ruleset + SAU ruleset)   │
│  ├─ record_decision() + trace_decision_chain()                  │
│  └─ W3C PROV-O Export (per jurisdiction)                        │
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

Every minted SIU (per country) is valued by:

```
SIU_adjusted = f(C_B × ΣE_D) × (1 − Ω_Threshold)
```

- **C_B** — Betweenness Centrality of the node within the sovereign hypergraph
- **ΣE_D** — Downstream Asset Exposure (refinery throughput, desalination output, port volume, infrastructure lifespan)
- **Ω_Threshold** — Real-time risk probability derived from live edge sensor readings

Each country maintains independent C_B, ΣE_D, and Ω_Threshold computations over its own 4-node hypergraph.

### 3.3 The Collateral Squeeze Rule

```
γ = { 2:1  if Ω_Threshold < Ω_Crit      ← normal baseline conditions
    { 4:1  if Ω_Threshold ≥ Ω_Crit      ← Yield Compression Event
```

When a sensor breach fires in either country's graph, the **Rete network — not an LLM** — triggers the Yield Compression Event for that sovereign configuration and pushes the 4:1 lock signal to STOKR's TaaS endpoint along with a complete, immutable causal path object.

---

### 3.4 Semantica's Core Responsibilities

Semantica is the **sole middleware layer** between TFE's edge hardware and STOKR's settlement ledger. Everything that makes a minting or squeeze decision legally defensible is Semantica's responsibility. The table below defines hard ownership boundaries.

> **What Semantica does NOT own:** Physical edge hardware collection (TFE), token issuance and settlement (STOKR), SPV legal structuring (STOKR/Sicos), and the LayoutLMv3 document model itself (Hugging Face, containerised by Kaif).

---

#### Responsibility 1 — SHACL Ingestion Validation Gate

- **What:** Defines the OWL ontology for all TFE entity types (biophysical node, industrial node, telemetry reading, threshold event, mint decision). Maintains **two country-specific SHACL profiles** — `kwt_shapes.ttl` and `sau_shapes.ttl` — auto-derived from the base ontology with jurisdiction-specific sensor ranges and unit constraints.
- **How:** Every raw telemetry packet arriving from TFE-ib or TFE-gdp simulators must pass the appropriate country SHACL gate before any data touches the knowledge graph. Packets that fail structural validation are rejected with a plain-English report; they never reach the graph layer.
- **Success bar:** 100% of intentionally corrupted test packets rejected. Zero false passes.
- **SDK component:** `ingestion/shacl_gates.py` + `ingestion/ontology.ttl` + `ingestion/kwt_shapes.ttl` + `ingestion/sau_shapes.ttl`

---

#### Responsibility 2 — Bi-Temporal Knowledge Graph

- **What:** Stores every asserted fact with two independent timestamps — `valid_time` (when the fact was true in the real world) and `recorded_at` (when Semantica ingested it). Maintains **two independent hypergraphs** — one for Kuwait (4 nodes) and one for Saudi Arabia (4 nodes) — each queryable at any historical date.
- **How:** `TemporalKnowledgeGraph(jurisdiction="KWT")` and `TemporalKnowledgeGraph(jurisdiction="SAU")` wrap every graph edge with this dual timestamp. `graph.state_at("YYYY-MM-DD")` reconstructs the full 4-node country hypergraph as it existed on any past date, enabling forensic replay without modifying the live graph.
- **Why this matters:** Satisfies bi-temporal audit requirements for CBK and SAMA. Any claim that "Kuwait Bay hypersalinity was X in 2003" can be replayed and proven.
- **SDK component:** `graph/temporal_graph.py`

---

#### Responsibility 3 — Allen Interval Algebra Anomaly Detection

- **What:** Applies the 13 Allen temporal relations to detect timing anomalies in the ingested SCADA and biophysical logs for both countries.
- **How:** Flags event sequences where a downstream effect precedes its upstream cause — a strong signal of data tampering or instrument miscalibration — without any LLM interpretation.
- **SDK component:** Enabled via `TemporalKnowledgeGraph(enable_allen_algebra=True)`

---

#### Responsibility 4 — Betweenness Centrality Engine

- **What:** Computes C_B (Betweenness Centrality) for each of the 4 nodes in each country hypergraph (8 nodes total), quantifying how many shortest paths in each sovereign hypergraph pass through each node.
- **How:** `CentralityCalculator(graph=kwt_graph)` and `CentralityCalculator(graph=sau_graph)` run independently. C_B for all 4 nodes per country must compute in < 50ms. The result feeds directly into each country's SIU valuation formula.
- **SDK component:** `graph/centrality.py`

---

#### Responsibility 5 — SIU Valuation Formula (Live Computation)

- **What:** Computes `SIU_adjusted = f(C_B × ΣE_D) × (1 − Ω_Threshold)` in real time for each country as graph state changes. No off-chain oracle. No LLM interpolation.
- **Variables owned by Semantica (per country):**
  - `C_B` — computed from the live country graph
  - `ΣE_D` — summed Downstream Asset Exposure from the Genesis Matrix for that country
  - `Ω_Threshold` — derived from live SHACL-validated sensor readings; updated on every successful packet ingestion
- **SDK component:** `graph/centrality.py` + `graph/context_graph.py`

---

#### Responsibility 6 — Rete Compliance Engine (Deterministic, Zero-LLM)

- **What:** Evaluates all regulatory and ecological rules against every telemetry packet and every mint decision. Uses a pre-compiled Rete network. Maintains **two jurisdiction-specific rulesets** — `kwt_rules/` and `sau_rules/` — each with 5 ecological rules plus the universal Covenant Rule.
- **Kuwait Rules (KWT):**
  - Rule KWT-1 — Dammam Aquifer piezometric drawdown velocity ≤ recharge rate (Node KWT-2)
  - Rule KWT-2 — Kuwait Bay electrical conductivity / hypersalinity index below threshold (Node KWT-1)
  - Rule KWT-3 — Mina Al-Ahmadi SCADA thermodynamic harmonics within ±2σ of genesis baseline (Node KWT-3)
  - Rule KWT-4 — Al-Zour pump thermodynamic signature variance within bounds (Node KWT-4)
  - Rule KWT-5 — Kuwait Bay benthic sediment transport velocity below siltation threshold (Node KWT-1)
  - Covenant Rule — SIU-T circulating supply ≤ 50% of SIU parent reserve at all times
- **Saudi Arabia Rules (SAU):**
  - Rule SAU-1 — Wajid/Minjur aquifer drawdown velocity ≤ recharge rate (Node SAU-2)
  - Rule SAU-2 — Red Sea coastal thermal gradient / brine shift within safe range (Node SAU-1)
  - Rule SAU-3 — Jubail SCADA thermodynamic harmonics within ±2σ of genesis baseline (Node SAU-3)
  - Rule SAU-4 — Port of King Abdullah PLC crane load weight vs. bill of lading divergence < 3% (Node SAU-4)
  - Rule SAU-5 — Red Sea wave attenuation collapse / kinetic energy threshold (Node SAU-1)
  - Covenant Rule — SIU-T circulating supply ≤ 50% of SIU parent reserve at all times
- **Guarantee:** 1,000 evaluations on identical inputs produce identical outputs. Non-compliance blocks the mint call with a structured error naming the exact failing rule and jurisdiction.
- **SDK component:** `reasoning/rete_engine.py` + `reasoning/rules/kwt_rules/` + `reasoning/rules/sau_rules/`

---

#### Responsibility 7 — S-1 Mint Decision Tracker

- **What:** Creates an immutable, cryptographically-bound causal object for every minting and squeeze decision, tagged with the sovereign jurisdiction (`jurisdiction: "KWT"` or `jurisdiction: "SAU"`).
- **Three API methods Semantica must expose:**
  - `graph.record_decision()` — writes the decision object to the graph
  - `graph.check_decision_rules()` — runs the Rete evaluation and binds the result to the decision
  - `graph.trace_decision_chain()` — walks the causal graph backward from the decision to the originating sensor values, timestamps, and breach values
- **Constraint:** If `check_decision_rules()` returns `approved=False`, the mint call raises a structured error before any signal reaches STOKR.
- **SDK component:** `reasoning/decision_tracker.py`

---

#### Responsibility 8 — 4:1 Yield Compression Event Engine

- **What:** When `Ω_Threshold ≥ Ω_Crit` in either country graph, Semantica's Rete network fires the Yield Compression Event within 100ms — no human in the loop, no LLM, no probabilistic delay. The compression event is jurisdiction-scoped: a Kuwait breach does not squeeze Saudi Arabia's SIU-T supply.
- **Sequence Semantica owns (per country):**
  1. Sensor breach detected in SHACL-validated packet (country-tagged)
  2. `Ω_Threshold` value updated in the country knowledge graph
  3. Rete evaluates the compression rule — fires immediately
  4. `record_decision(category="yield_compression", outcome="squeeze_4_1", jurisdiction="KWT"|"SAU")` creates the causal object
  5. Causal object posted to STOKR TaaS `/collateral-squeeze` endpoint with jurisdiction header
  6. Collateral ratio transitions from 2:1 → 4:1 on the circulating SIU-T supply for that sovereign
- **SLA:** p99 latency from breach detection to 4:1 lock confirmation < 100ms
- **SDK component:** `reasoning/rete_engine.py` + `reasoning/decision_tracker.py`

---

#### Responsibility 9 — Provenance Manager (Per-Claim Source Attribution)

- **What:** Tracks every asserted fact in each country knowledge graph to its originating source: document filename, DOI, author, page number, ingestion timestamp, and confidence score.
- **How:** `ProvenanceManager.track_entity()` binds claims at ingestion time. `get_lineage()` walks the full multi-hop ancestor chain.
- **Minimum standard:** Every entity in the graph must have a ≥ 3-hop provenance chain traceable to a DOI or official government source.
- **SDK component:** `provenance/manager.py`

---

#### Responsibility 10 — W3C PROV-O Turtle Export

- **What:** Converts the provenance graph into a compliance-grade W3C PROV-O Turtle (`.ttl`) file — one exportable file per jurisdiction per event.
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
| R1 | SHACL Ingestion Gate (KWT + SAU profiles) | `ingestion/shacl_gates.py` | 100% corrupted packets rejected |
| R2 | Bi-Temporal Knowledge Graphs (2 graphs) | `graph/temporal_graph.py` | Point-in-time replay at any date, per country |
| R3 | Allen Interval Algebra | `graph/temporal_graph.py` | Timing anomalies flagged without LLM |
| R4 | Betweenness Centrality (2 graphs) | `graph/centrality.py` | C_B for 8 nodes in < 50ms per graph |
| R5 | SIU Valuation Formula (per country) | `graph/centrality.py` | Live, no off-chain oracle |
| R6 | Rete Compliance Engine (KWT + SAU rulesets) | `reasoning/rete_engine.py` | Deterministic, zero-LLM, 12 rules total |
| R7 | S-1 Mint Decision Tracker | `reasoning/decision_tracker.py` | Full causal chain to sensor, jurisdiction-tagged |
| R8 | 4:1 Compression Event (jurisdiction-scoped) | `reasoning/rete_engine.py` | < 100ms p99 breach-to-lock |
| R9 | Provenance Manager | `provenance/manager.py` | ≥ 3-hop lineage to DOI |
| R10 | W3C PROV-O Export (per jurisdiction) | `provenance/exporter.py` | Zero-error rdflib parse |

---

## 4. POC Scope & Boundaries

### 4.1 What Is In Scope

- **Forensic Ingestion Clean Rooms** — Two containerized LayoutLMv3 pipelines (one per country) parsing historical Kuwait and Saudi Arabian datasets, purging invalid entries, and outputting the Genesis Matrix for each
- **Dual-Telemetry Simulators** — TFE-ib (biophysical) and TFE-gdp (SCADA/industrial) stream generators for all 8 nodes across both countries
- **SHACL Validation Gates** — Country-specific OWL ontology shapes that reject structurally invalid telemetry packets before any ledger contact
- **Bi-Temporal Knowledge Graphs** — Two independent graphs, one per country, with `valid_time` + `recorded_at` on every graph edge and `graph.state_at()` for point-in-time replay
- **Betweenness Centrality Engine** — C_B calculation over the 4-node hypergraph for each country
- **Rete Compliance Engine** — 12 deterministic, non-probabilistic ecological and industrial rules across both countries (6 per country) plus the universal Covenant Rule
- **S-1 Mint Decision Tracker** — `record_decision()`, `check_decision_rules()`, and `trace_decision_chain()` for every minting and throttle event, jurisdiction-tagged
- **Next.js Sovereign Dashboard** — Premium web UI with Sigma.js dual hypergraph view (KWT + SAU), live WebSocket telemetry, Tremor KPI cards, Recharts timelines, and PROV-O lineage explorer
- **W3C PROV-O Audit Export** — Automated Turtle file generation from any minting or compression event, per jurisdiction
- **4:1 Squeeze Hook Demo** — Live triggered Yield Compression Event from a simulated sensor threshold breach in each country

### 4.2 What Is Out of Scope

The following are post-PoC deliverables and will **not** be built during these 4 weeks:

- Physical Sentinel Hub V.4 and Socket-7 hardware deployment in Kuwait or Saudi Arabia
- Live STOKR Liquid Network mainnet token issuance
- CSSF / CBK / SAMA regulatory submission and legal filing
- Production SRAM PUF silicon fabrication and ML-KEM-768 hardware integration (simulated in PoC)
- ORO Fund SPV legal structuring and CSSF registration

---

### 4.3 Kuwait — Four Critical Resource Nodes

All telemetry is **simulated** using public datasets and synthetic generators calibrated to real Kuwaiti specifications.

---

#### Node KWT-1 — Kuwait Bay Intertidal Eco-Buffer Strip

- **Location:** Core coastal mudflat and hyper-saline shallow shelf ecosystems flanking the northern industrial approach arcs of Kuwait Bay
- **Track:** TFE-ib (biophysical)
- **Live stream:** Real-time coastal thermal gradients, electrical conductivity/salinity tracking, benthic sediment transport metrics, and intertidal kinetic wave attenuation curves (simulated via Sentinel Hub V.4 marine module model)
- **Hardware model:** Three ruggedized Sentinel Hub V.4 marine modules. Inconel 625 monocoque chassis with The Shiver integrated piezoelectric transducers.
- **Forensic ingestion target:** 40 years of daily water-temperature records, channel bathymetric depth surveys, and historical bay water chemistry charts
- **Key interdependency:** Upstream environmental monitor for Node KWT-4 (Al-Zour Desalination). A hypersalinity spike at this node degrades seawater intake quality, accelerating filter clogging and pump anomalies.

**Data Sources:**

- [Kuwait Environment Public Authority (EPA)](https://www.epa.gov.kw/) — 40yr daily water temperature records, channel bathymetric surveys, and historical Kuwait Bay water chemistry charts (primary historical baseline)
- [Kuwait Institute for Scientific Research (KISR)](https://www.kisr.edu.kw/) — marine environment research archives, coastal ecosystem baseline studies
- [Copernicus Marine Service (CMEMS)](https://marine.copernicus.eu/) — Arabian Gulf SST, salinity profiles, wave energy, and sea level anomaly time series
- [NOAA CoastWatch](https://coastwatch.noaa.gov/) — satellite-derived sea surface temperature and coastal chlorophyll concentration
- [IOC-UNESCO Regional Marine Pollution Emergency Response Centre for the Wider Arabian Area (ROPME)](http://www.ropme.org/) — historical Gulf oceanographic and pollution baseline data
- [FAO Regional Fisheries and Ecosystem Assessment](https://www.fao.org/fishery/en/area/57/en) — Arabian Gulf ecosystem baseline reports for benthic habitat
- [Global Mangrove Watch — JAXA/EORC](https://www.eorc.jaxa.jp/ALOS/en/dataset/gmw_e.htm) — mangrove and intertidal extent time series for Gulf coastlines
- [Copernicus Climate Change Service (C3S)](https://climate.copernicus.eu/) — sea level rise projections and storm frequency trends for Ω_Threshold calibration

---

#### Node KWT-2 — Dammam Subsurface Aquifer Columns

- **Location:** Strategic deep-well baseline fields and subterranean fresh/brackish water columns, Dammam Aquifer Matrix
- **Track:** TFE-ib (biophysical)
- **Live stream:** Groundwater piezometric hydraulic head indices, aquifer baseline pressure levels, total dissolved solids (TDS) profiles, and localized drawdown recharge velocities (simulated via Sentinel Hub V.4 SNN ASIC model)
- **Hardware model:** Subterranean deep exploration probe strings direct-wired to surface Sentinel Hub V.4 computing cores running neuromorphic SNN ASICs (<150 mW idle)
- **Forensic ingestion target:** 30 years of daily water pump registries, deep well pressure charts, and geochemical metrics
- **Key interdependency:** Primary subsurface water regulator for Node KWT-3 (Mina Al-Ahmadi Refinery). A piezometric head collapse and TDS spike compromises refinery cooling loops and causes thermodynamic imbalances.

**Data Sources:**

- [Kuwait Ministry of Electricity, Water and Renewable Energy (MEWA)](https://www.mewa.gov.kw/) — 30yr daily water pump registries, deep well pressure charts, and geochemical metrics (primary source)
- [Kuwait Water Authority](https://www.mewa.gov.kw/) — historical groundwater extraction records and aquifer recharge studies
- [Arab Water Council](https://arabwatercouncil.org/) — regional aquifer assessments and transboundary water resource reports for the Arabian Gulf basin
- [FAO AQUASTAT](https://www.fao.org/aquastat/en/) — Kuwait national freshwater resources statistics for ΣE_D coefficient calibration
- [USGS Groundwater Resources Program](https://www.usgs.gov/mission-areas/water-resources/science/groundwater) — global fossil aquifer atlas data for Dammam formation baseline
- [UNESCO-IHP Non-Renewable Groundwater Resources Program](https://www.unesco.org/en/natural-sciences/water) — international non-renewable aquifer depletion benchmarks
- [Copernicus Land Service — Soil Water Index](https://land.copernicus.eu/global/products/swi) — near-real-time surface moisture for recharge velocity calibration

---

#### Node KWT-3 — Strategic Hydrocarbon Metabolism Enclave (Mina Al-Ahmadi)

- **Location:** Main crude export pipeline headers, refinery blending manifolds, and automated custody transfer weigh loops, Mina Al-Ahmadi industrial infrastructure
- **Track:** TFE-gdp (SCADA/industrial)
- **Live stream:** Multi-phase fluid mass velocities, wellhead pressure profiles, separation plant thermodynamic metrics, and automated custody transfer logs (simulated via Modbus/TCP SCADA model)
- **Hardware model:** Socket-7 Industrial Gateways hooked directly into downstream plant sorting PLCs and automated conveyor SCADA lines via optically isolated physical hardware taps
- **Forensic ingestion target:** 20 years of electronic SCADA log streams, transport customs weight records, and refinery output declarations

**Data Sources:**

- [Kuwait National Petroleum Company (KNPC) Public Reports](https://www.knpc.com/) — 20yr refinery output declarations, annual capacity reports, and SCADA utilization statistics (primary source)
- [Kuwait Petroleum Corporation (KPC)](https://www.kpc.com.kw/) — upstream and downstream production benchmarks and annual reports
- [OPEC Production Statistics](https://www.opec.org/opec_web/en/data_graphs/40.htm) — historical Kuwait crude production and export volumes for RSID baseline calibration
- [IEA Kuwait Energy Statistics](https://www.iea.org/countries/kuwait) — historical refinery throughput, product yield, and energy intensity metrics
- [UN Comtrade Database](https://comtradeplus.un.org/) — Kuwait petroleum export customs records for bill of lading cross-reference
- [World Bank Commodity Markets (Pink Sheet)](https://www.worldbank.org/en/research/commodity-markets) — crude oil price time series for ΣE_D commodity value calibration

---

#### Node KWT-4 — Al-Zour Mega-Scale Desalination & Utility Complex

- **Location:** Primary seawater intake manifolds, high-pressure pump distributions, and centralized chemical balancing lines, Al-Zour Desalination Complex
- **Track:** TFE-gdp (SCADA/industrial)
- **Live stream:** Flow manifold volume velocity metrics, pump thermodynamic signature variations, volumetric filter monitoring streams, and terminal head pressures (simulated via explosion-hardened Socket-7 Gateway model)
- **Hardware model:** Explosion-hardened Socket-7 Gateways housed in Mu-Metal and silver-plated copper Faraday cages to shield internal atomic clocks from industrial electromagnetic fields
- **Forensic ingestion target:** Plant flow meter histories, municipal output logs, and inter-utility balance sheets
- **Key interdependency (binding):** The S-1 Mint algorithm binds Node KWT-4 industrial trade clearings directly to the biophysical risk containment values of Nodes KWT-1 and KWT-2, computing The Full-Equation to automatically throttle or freeze token clearing states.

**Data Sources:**

- [Kuwait Authority for Partnership Projects (KAPP) — Al-Zour Project](https://www.kapp.gov.kw/) — Al-Zour desalination plant capacity, flow manifold specifications, and output logs
- [International Desalination Association (IDA)](https://idadesal.org/) — global desalination plant performance benchmarks and energy intensity metrics
- [Global Water Intelligence](https://www.globalwaterintel.com/) — desalination market statistics and operational performance data
- [Ministry of Electricity, Water and Renewable Energy (MEWA)](https://www.mewa.gov.kw/) — national water production and distribution statistics
- [World Bank Water Data Portal](https://data.worldbank.org/indicator/ER.H2O.FWTL.K3) — Kuwait freshwater withdrawal and productivity statistics
- [IEA Water-Energy Nexus Reports](https://www.iea.org/topics/water) — desalination energy intensity benchmarks for ΣE_D coefficient calibration

---

### 4.4 Saudi Arabia — Four Critical Resource Nodes

All telemetry is **simulated** using public datasets and synthetic generators calibrated to real Saudi Arabian specifications.

---

#### Node SAU-1 — Red Sea Coastal Eco-Shield & Maritime Corridor

- **Location:** Critical intertidal coral-mangrove protective shield flanking the NEOM/Giga-project coastal approach arcs and deep shipment corridors
- **Track:** TFE-ib (biophysical)
- **Live stream:** Real-time coastal thermal gradients, electrical conductivity/salinity tracking, benthic sediment transport metrics, and intertidal kinetic wave attenuation curves (simulated via Sentinel Hub V.4 Marine enclaves)
- **Hardware model:** Three ruggedized Sentinel Hub V.4 (Marine) enclaves. Inconel 625 monocoque chassis with The Shiver piezoelectric transducers guaranteeing 99.9% forensic uptime in hyper-saline maritime spray.
- **Forensic ingestion target:** 40 years of bathymetric surveys, maritime salinity records, and historical temperature logs
- **Key interdependency:** Coastal buffer for Node SAU-4 (Port of King Abdullah). Eco-shield degradation triggers wave energy buildup battering port infrastructure, siltating shipping lanes, and reducing harbor draft depth.

**Data Sources:**

- [King Abdullah University of Science and Technology (KAUST) — Red Sea Research Center](https://www.kaust.edu.sa/en/research/center-of-excellence/red-sea-research-center) — coral reef monitoring data, Red Sea oceanographic baselines, and temperature/salinity time series (primary source)
- [Saudi Ministry of Environment, Water and Agriculture (MEWA/NCWE)](https://www.mewa.gov.sa/) — coastal ecosystem surveys and environmental monitoring reports
- [Copernicus Marine Service (CMEMS)](https://marine.copernicus.eu/) — Red Sea SST, salinity profiles, wave energy, tidal surge, and sea level anomaly data
- [NOAA CoastWatch](https://coastwatch.noaa.gov/) — satellite-derived sea surface temperature and coastal chlorophyll for Red Sea
- [IOC-UNESCO Regional Marine Pollution Emergency Response — ROPME](http://www.ropme.org/) — Red Sea oceanographic baseline data
- [Global Mangrove Watch — JAXA/EORC](https://www.eorc.jaxa.jp/ALOS/en/dataset/gmw_e.htm) — 40yr mangrove and intertidal extent time series for the Red Sea coastline
- [Saudi Geological Survey](https://www.sgs.gov.sa/) — coastal geomorphological surveys and sediment baseline assessments
- [Copernicus Climate Change Service (C3S)](https://climate.copernicus.eu/) — Red Sea sea level rise projections and storm frequency trends for Ω_Threshold calibration

---

#### Node SAU-2 — Wajid/Minjur Subterranean Aquifer Plenum

- **Location:** Strategic deep-well baseline fields and deep fossil water columns within the Wajid and Minjur deep aquifer formations (regulating regional agricultural extraction and industrial utility drawdowns)
- **Track:** TFE-ib (biophysical)
- **Live stream:** Groundwater piezometric hydraulic head indices, deep-formation pressure metrics, total dissolved solids (TDS) profiles, and localized drawdown recharge velocities (simulated via Sentinel Hub V.4 SNN ASIC model, <150 mW idle)
- **Hardware model:** Deep-well sensory probe strings direct-wired to surface-level Sentinel Hub V.4 computing cores. Telemetry sealed with SRAM PUF fingerprints and ML-KEM-768 post-quantum container.
- **Forensic ingestion target:** 30 years of daily pump registries, deep borehole logs, and regional hydrogeologic test archives
- **Key interdependency:** Subsurface water tower for Node SAU-3 (Jubail Industrial Complex). Aquifer over-extraction causes cooling loop failure, thermodynamic imbalances, and mechanical wear on heavy cracking pumps.

**Data Sources:**

- [Saudi Ministry of Environment, Water and Agriculture (MEWA)](https://www.mewa.gov.sa/) — groundwater monitoring reports, borehole logs, and extraction permit registries (primary source)
- [Saudi Geological Survey — Hydrogeology Division](https://www.sgs.gov.sa/) — Wajid and Minjur aquifer formation mapping, pressure logs, and TDS geochemical archives
- [FAO AQUASTAT — Saudi Arabia](https://www.fao.org/aquastat/en/) — national freshwater resources statistics and fossil aquifer depletion assessments for ΣE_D calibration
- [Arab Water Council](https://arabwatercouncil.org/) — regional transboundary aquifer assessments for the Arabian Shield and Rub' al Khali basin
- [UNESCO-IHP Non-Renewable Groundwater Resources](https://www.unesco.org/en/natural-sciences/water) — fossil aquifer depletion rate benchmarks
- [USGS Groundwater Resources Program](https://www.usgs.gov/mission-areas/water-resources/science/groundwater) — global fossil aquifer atlas data for formation baseline calibration
- [ESA CCI Soil Moisture](https://www.esa-soilmoisture-cci.org/) — regional recharge velocity calibration from surface moisture indices

---

#### Node SAU-3 — Strategic Industrial Metabolism Enclave (Jubail Complex Core)

- **Location:** Primary pipeline collection manifolds, automated cracking plant arrays, and refinery blending manifold headers, Jubail Industrial City refining complexes
- **Track:** TFE-gdp (SCADA/industrial)
- **Live stream:** Multi-phase fluid mass velocities, wellhead pressure profiles, chemical separation circuit thermodynamic metrics, and automated custody transfer logs (simulated via Socket-7 Industrial Gateway / Modbus-TCP SCADA model)
- **Hardware model:** Socket-7 Industrial Gateways hooked directly into downstream plant sorting PLCs and automated conveyor SCADA networks via optically isolated physical hardware taps; runs Resonant Signature Identification (RSID)
- **Forensic ingestion target:** 20 years of electronic SCADA log streams, transport customs weight records, and refinery output declarations from Saudi Aramco and Jubail complexes

**Data Sources:**

- [Saudi Aramco Annual Reports (Public)](https://www.aramco.com/en/investors/annual-report) — 20yr production data, downstream refining capacity, and SCADA utilization statistics (primary source)
- [SABIC Annual Reports](https://www.sabic.com/en/investors/annual-reports) — Jubail complex petrochemical output, plant capacity, and operational metrics
- [Royal Commission for Jubail and Yanbu (RCJY)](https://www.rcjy.gov.sa/) — industrial city production statistics, energy and water consumption, and plant operational records
- [OPEC Production Statistics](https://www.opec.org/opec_web/en/data_graphs/40.htm) — Saudi Arabia historical crude production and export volumes
- [IEA Saudi Arabia Energy Statistics](https://www.iea.org/countries/saudi-arabia) — refinery throughput, product yield, and energy intensity time series
- [UN Comtrade Database](https://comtradeplus.un.org/) — Saudi Arabia petroleum and petrochemical export customs records for bill of lading cross-reference
- [World Bank Commodity Markets (Pink Sheet)](https://www.worldbank.org/en/research/commodity-markets) — crude oil and petrochemical price time series for ΣE_D commodity value floor calibration

---

#### Node SAU-4 — Port of King Abdullah Logistics Terminal Gantries

- **Location:** Automated container gantry terminal crane networks, dry bulk loaders, and outbound electronic scale networks, King Abdullah Port (Rabigh)
- **Track:** TFE-gdp (SCADA/industrial)
- **Live stream:** Crane gantry PLC load weights, container automated tracking manifests, freight logistics velocity tracking, and gate-clearance manifests (simulated inside Mu-Metal Faraday cage Socket-7 model)
- **Hardware model:** Hardened Socket-7 Gateways housed in Mu-Metal and silver-plated copper Faraday cages shielding internal atomic clocks from heavy port marine radar fields
- **Forensic ingestion target:** Shipping bills of lading, automated freight weight logs, and international customs tracking manifests
- **Key interdependency (binding):** The S-1 Mint algorithm binds Node SAU-4 industrial trade volume clearings directly to the biophysical risk containment values of Nodes SAU-1 and SAU-2.

**Data Sources:**

- [King Abdullah Port Authority (Mawani)](https://www.mawani.gov.sa/) — container throughput statistics, berth occupancy records, crane utilization rates, and gate-clearance manifests (primary source)
- [Saudi Ports Authority (Mawani) — Annual Reports](https://www.mawani.gov.sa/en/reports) — national port throughput benchmarks and logistics performance data
- [UNCTAD Maritime Statistics](https://unctadstat.unctad.org/) — Red Sea port container TEU throughput for ΣE_D trade velocity calibration
- [World Bank — Container Port Traffic Data](https://datacatalog.worldbank.org/search/dataset/0038027) — historical TEU benchmark series for regional ports
- [IMO — Global Integrated Shipping Information System (GISIS)](https://gisis.imo.org/) — vessel registration, cargo manifests, and port state control records
- [MarineTraffic AIS Historical Data](https://www.marinetraffic.com/) — vessel movement data for freight velocity simulation and gate-clearance anomaly detection
- [Saudi Customs (Zatca)](https://www.zatca.gov.sa/) — import/export declaration data and bill of lading cross-reference for PLC load weight anomaly detection

---

## 5. System Architecture

### 5.1 Data Flow

```
[Public + Synthetic Kuwait Data]    [Public + Synthetic Saudi Arabia Data]
          │                                      │
          ▼                                      ▼
┌────────────────────────┐          ┌────────────────────────┐
│  LayoutLMv3 Clean Room │          │  LayoutLMv3 Clean Room │
│  KWT — 4 nodes         │          │  SAU — 4 nodes         │
│  → Genesis Matrix KWT  │          │  → Genesis Matrix SAU  │
└───────────┬────────────┘          └────────────┬───────────┘
            │                                    │
     ┌──────┴───────┐                    ┌───────┴──────┐
     ▼              ▼                    ▼              ▼
┌──────────┐ ┌──────────┐          ┌──────────┐ ┌──────────┐
│ TFE-ib   │ │ TFE-gdp  │          │ TFE-ib   │ │ TFE-gdp  │
│ KWT-1,2  │ │ KWT-3,4  │          │ SAU-1,2  │ │ SAU-3,4  │
└────┬─────┘ └────┬─────┘          └────┬─────┘ └────┬─────┘
     └──────┬─────┘                     └──────┬──────┘
            ▼                                  ▼
  ┌─────────────────────┐          ┌─────────────────────┐
  │ SHACL Gate (KWT)    │          │ SHACL Gate (SAU)    │
  │ kwt_shapes.ttl      │          │ sau_shapes.ttl      │
  └──────────┬──────────┘          └──────────┬──────────┘
             ▼                                ▼
  ┌──────────────────────┐        ┌──────────────────────┐
  │ KWT Knowledge Graph  │        │ SAU Knowledge Graph  │
  │ Bi-Temporal (4 nodes)│        │ Bi-Temporal (4 nodes)│
  │ Centrality Engine    │        │ Centrality Engine    │
  │ Rete (KWT rules)     │        │ Rete (SAU rules)     │
  │ ProvenanceManager    │        │ ProvenanceManager    │
  └────┬─────────┬───────┘        └────┬─────────┬───────┘
       │         │                     │         │
  record_      PROV-O             record_      PROV-O
  decision     export             decision     export
       │         │                     │         │
       └─────────┴──────────┬──────────┴─────────┘
                            ▼
                 ┌─────────────────────┐
                 │  FastAPI + WebSocket│
                 │  Unified API Layer  │
                 └──────────┬──────────┘
                            │
               ┌────────────┴──────────────┐
               ▼                           ▼
  ┌────────────────────────┐    ┌──────────────────────────┐
  │  Next.js Dashboard     │    │  STOKR TaaS Stub         │
  │  Dual Sovereign View   │    │  /collateral-squeeze     │
  │  KWT + SAU panels      │    │  /mint-signal            │
  └────────────────────────┘    └──────────────────────────┘
```

### 5.2 Technology Stack

#### Backend

- **Document parsing** — LayoutLMv3 (Hugging Face), Docker (two parallel cleanroom containers)
- **Knowledge graph** — Semantica ContextGraph + TemporalKnowledgeGraph (instantiated twice — KWT and SAU)
- **Validation** — SHACL shapes (pySHACL), OWL ontology (rdflib), two country-specific shape profiles
- **Reasoning** — Semantica ReteEngine (deterministic, zero-LLM), two country-specific rulesets
- **Provenance** — Semantica ProvenanceManager + RDFExporter
- **Graph algorithms** — Semantica CentralityCalculator (C_B per country)
- **API layer** — FastAPI (Python) with WebSocket support (`/ws/telemetry/{country}`, `/ws/events/{country}`)
- **Data simulation** — NumPy, Pandas, synthetic generators
- **Containerisation** — Docker Compose
- **Testing** — pytest (unit + integration), locust (load)

#### Frontend — Sovereign Intelligence Dashboard

- **Framework** — Next.js 14 (App Router, TypeScript, SSR + client components)
- **Styling** — Tailwind CSS + shadcn/ui component primitives
- **Dashboard components** — Tremor for KPI cards, sparklines, area charts, and progress bars
- **Sovereign hypergraph** — Sigma.js + Graphology for force-directed hypergraphs — one KWT view, one SAU view, rendered side-by-side or toggled via country selector
- **Time-series charts** — Recharts for node telemetry timelines, C_B trend lines, and Ω_Threshold history
- **Live data** — Native WebSocket client (`/ws/telemetry/kwt`, `/ws/telemetry/sau`) for real-time telemetry push — no polling
- **Animations** — Framer Motion for collateral ratio transitions, breach alerts, and panel state changes

---

## 6. 4-Week Delivery Plan

> **Timeline:** July 1 – July 28, 2026 · **20 working days** · Hard milestone at end of each week

---

### Week 1 — Foundation, Dual-Country Data & Ingestion

**July 1–4 · 4 days**

**Goal:** The skeleton runs for both countries. All eight nodes have synthetic data flowing through the ingestion pipelines and SHACL is catching bad packets for both Kuwait and Saudi Arabia.

#### Day 1–2 · Environment & Dual-Country Data Setup

- [ ] Initialise monorepo folder structure: `/ingestion`, `/graph`, `/reasoning`, `/api`, `/dashboard`, `/tests`, `/data/kuwait`, `/data/saudi_arabia`
- [ ] Docker Compose stack up: two LayoutLMv3 cleanroom services (KWT + SAU) · Semantica service · FastAPI service · Dashboard dev server
- [ ] Generate synthetic telemetry datasets for all 8 nodes:
  - **KWT-1:** 40yr Kuwait Bay water temperature records, conductivity time series, bathymetric charts (CSV)
  - **KWT-2:** 30yr Dammam Aquifer pump registries, piezometric head charts, TDS geochemical logs
  - **KWT-3:** 20yr Mina Al-Ahmadi SCADA vibration logs in Modbus/TCP format simulation
  - **KWT-4:** Al-Zour plant flow meter histories, pump thermodynamic signatures, municipal output logs
  - **SAU-1:** 40yr Red Sea bathymetric surveys, maritime salinity records, coastal temperature logs
  - **SAU-2:** 30yr Wajid/Minjur daily pump registries, borehole logs, hydrogeologic archives
  - **SAU-3:** 20yr Jubail SCADA log streams, refinery output declarations, customs weight records
  - **SAU-4:** King Abdullah Port shipping manifests, PLC crane load weights, gate-clearance records
- [ ] Seed with public data where available — CMEMS (Red Sea + Arabian Gulf), Copernicus Level-2, FAO AQUASTAT, UNCTAD, UN Comtrade

#### Day 3–4 · Dual Ingestion Clean Rooms + SHACL Gates

- [ ] Containerise two LayoutLMv3 document parsing pipelines — one per country
- [ ] Build `ingestion/cleanroom.py` with `jurisdiction` parameter — ingests CSVs and PDFs, purges anomalous entries, outputs Genesis Matrix per country as Parquet
- [ ] Define base OWL ontology for TFE entity types: biophysical node, industrial node, telemetry reading, threshold event
- [ ] Derive `ingestion/kwt_shapes.ttl` and `ingestion/sau_shapes.ttl` — country-specific sensor unit ranges, conductivity thresholds, pressure bounds
- [ ] SHACL gate behaviour: out-of-range or malformed packets generate a plain-English validation report and are dropped before graph contact
- [ ] Unit tests: inject 10 corrupted packets per country (20 total) → assert all 20 rejected

**Week 1 Exit Gate:**

- [ ] All 8 node datasets loaded and versioned in `/data/kuwait/` and `/data/saudi_arabia/`
- [ ] Both LayoutLMv3 cleanrooms producing valid Genesis Matrix Parquet files with no tampered entries
- [ ] Both SHACL gates demonstrably rejecting malformed telemetry on every run
- [ ] `docker compose up` starts all services clean with no errors

---

### Week 2 — Dual Knowledge Graphs, Temporal Engines & Centrality

**July 7–11 · 5 days**

**Goal:** Both 4-node hypergraphs are live. Bi-temporal state replay works at any historical date for each country. Betweenness Centrality fires sub-50ms per graph.

#### Day 5–6 · Bi-Temporal Knowledge Graphs — KWT and SAU

- [ ] Initialise `ContextGraph(jurisdiction="KWT", advanced_analytics=True)` with 4 nodes and inter-node edges:
  - KWT-1 → KWT-4 (hypersalinity → desalination intake quality)
  - KWT-2 → KWT-3 (piezometric head → refinery cooling loop)
- [ ] Initialise `ContextGraph(jurisdiction="SAU", advanced_analytics=True)` with 4 nodes and inter-node edges:
  - SAU-1 → SAU-4 (wave attenuation → port structural integrity, draft depth)
  - SAU-2 → SAU-3 (aquifer drawdown → Jubail cooling loop efficiency)
- [ ] Tag every graph edge with `valid_time` and `recorded_at` in both graphs
- [ ] Implement `graph.state_at("YYYY-MM-DD")` for both country graphs
- [ ] Load KWT Genesis Matrix into KWT graph; SAU Genesis Matrix into SAU graph
- [ ] Implement Allen Interval Algebra anomaly detection on both graphs
- [ ] Tests: `kwt_graph.state_at("1990-01-01")` and `sau_graph.state_at("1990-01-01")` both return valid non-empty graphs distinct from their 2024 states

#### Day 7–8 · Betweenness Centrality — Per Country

- [ ] Implement `CentralityCalculator(graph=kwt_graph)` — compute C_B for KWT-1, KWT-2, KWT-3, KWT-4
  - **KWT-1 interpretation:** High ecological C_B — hypersalinity events cascade to desalination (KWT-4) and stress overall industrial supply chain
  - **KWT-2 interpretation:** Moderate-high C_B — water-table drawdown propagates to refinery cooling (KWT-3)
  - **KWT-3 interpretation:** High economic C_B — crude export clearance routes through this node
  - **KWT-4 interpretation:** Highest national utility C_B — municipal freshwater supply for entire Kuwait City metropolitan area
- [ ] Implement `CentralityCalculator(graph=sau_graph)` — compute C_B for SAU-1, SAU-2, SAU-3, SAU-4
  - **SAU-1 interpretation:** High ecological C_B — coral-mangrove buffer stabilises port draft depth (SAU-4) and shields NEOM coastal infrastructure
  - **SAU-2 interpretation:** High resource C_B — Wajid/Minjur is the primary industrial water tower for the entire Eastern Province
  - **SAU-3 interpretation:** Highest economic C_B — Jubail is the single largest petrochemical export complex in the world
  - **SAU-4 interpretation:** High logistics C_B — King Abdullah Port is the primary deep-water gateway for industrial export volumes
- [ ] Implement ΣE_D coefficients for both countries from Genesis Matrix:
  - KWT: refinery throughput (KWT-3), desalination output (KWT-4), bay buffer value (KWT-1), aquifer recharge contribution (KWT-2)
  - SAU: port TEU throughput (SAU-4), Jubail refining value (SAU-3), Red Sea buffer value (SAU-1), Wajid recharge contribution (SAU-2)
- [ ] Implement live SIU valuation formula for both countries:

  ```python
  kwt_siu = f(kwt_C_B * kwt_sum_E_D) * (1 - kwt_omega)
  sau_siu = f(sau_C_B * sau_sum_E_D) * (1 - sau_omega)
  ```

- [ ] Benchmark: C_B for 4 nodes per country in < 50ms each

#### Day 9 · Provenance Binding — Both Countries

- [ ] Implement `ProvenanceManager(jurisdiction="KWT")` and `ProvenanceManager(jurisdiction="SAU")`
- [ ] Bind KWT-1 coastal data to KISR/EPA synthetic records with DOI metadata
- [ ] Bind KWT-2 aquifer data to MEWA pump registry synthetic source
- [ ] Bind SAU-1 Red Sea data to KAUST RSRC synthetic records with DOI metadata
- [ ] Bind SAU-2 aquifer data to Saudi Geological Survey synthetic borehole source
- [ ] Unit test: `prov.get_lineage("kwt_node1_bay_salinity")` and `prov.get_lineage("sau_node2_wajid_piezometric")` both return ≥ 3-hop chains to source files

**Week 2 Exit Gate:**

- [ ] `kwt_graph.state_at("2010-01-01")` and `sau_graph.state_at("2010-01-01")` return distinct, structurally correct graph states from their 2024 versions
- [ ] C_B computed for all 8 nodes (4 KWT + 4 SAU), confirmed sub-50ms per country
- [ ] `KWT_SIU_adjusted` and `SAU_SIU_adjusted` both computing live against real graph state
- [ ] Full provenance chain traced for at least one fact per node (8 nodes total)

---

### Week 3 — Dual Rete Compliance Engine, Mint Logic & Squeeze Hooks

**July 14–18 · 5 days**

**Goal:** Both policy brains are live. Minting is gated by deterministic rules per jurisdiction. The 4:1 squeeze fires within 100ms of any threshold breach in either country, without cross-contaminating the other sovereign's collateral state.

#### Day 10–11 · Rete Network Rule Compilation — KWT and SAU

Compile the full rule libraries into `ReteEngine(jurisdiction="KWT")` and `ReteEngine(jurisdiction="SAU")`:

**Kuwait Rules:**

- [ ] **Rule KWT-1** — Dammam Aquifer piezometric drawdown velocity > recharge rate → reject Node KWT-2; flag `tfe:AquiferBreachEvent`; block SIU-T minting for KWT
- [ ] **Rule KWT-2** — Kuwait Bay electrical conductivity spike breaches hypersalinity threshold → reject Node KWT-1; flag `tfe:HypersalinityEvent`; block SIU-T minting for KWT
- [ ] **Rule KWT-3** — Mina Al-Ahmadi SCADA thermodynamic harmonics outside ±2σ genesis baseline → reject SCADA stream; flag `tfe:HarmonicAnomalyEvent`; suspend Node KWT-3
- [ ] **Rule KWT-4** — Al-Zour pump thermodynamic signature variance exceeds bounds → flag `tfe:PumpAnomalyEvent`; does not block minting unless anomaly persists 3 consecutive readings
- [ ] **Rule KWT-5** — Kuwait Bay benthic sediment transport velocity above siltation threshold → flag `tfe:SiltationEvent`; block desalination clearance at Node KWT-4
- [ ] **Covenant Rule (KWT)** — SIU-T circulating supply > 50% of SIU parent reserve → reject mint; raise structured error

**Saudi Arabia Rules:**

- [ ] **Rule SAU-1** — Wajid/Minjur aquifer drawdown velocity > recharge rate → reject Node SAU-2; flag `tfe:AquiferBreachEvent`; block SIU-T minting for SAU
- [ ] **Rule SAU-2** — Red Sea coastal thermal gradient / brine shift breaches threshold → reject Node SAU-1; flag `tfe:BrineShiftEvent`; block SIU-T minting for SAU
- [ ] **Rule SAU-3** — Jubail SCADA thermodynamic harmonics outside ±2σ genesis baseline → reject SCADA stream; flag `tfe:HarmonicAnomalyEvent`; suspend Node SAU-3
- [ ] **Rule SAU-4** — Port of King Abdullah PLC crane load weight vs. bill of lading divergence > 3% → flag `tfe:ManifestDiscrepancyEvent`; does not block minting unless divergence persists across 3 consecutive manifests
- [ ] **Rule SAU-5** — Red Sea kinetic wave attenuation collapse → flag `tfe:WaveAttenuationEvent`; block port clearance at Node SAU-4
- [ ] **Covenant Rule (SAU)** — SIU-T circulating supply > 50% of SIU parent reserve → reject mint; raise structured error

- [ ] Implement `ReteEngine(jurisdiction).evaluate(telemetry_packet)` → `{approved: bool, failing_rule: str | None, jurisdiction: str}`
- [ ] Test: 5 compliant packets per country → all pass; 5 non-compliant packets per country → all fail naming the correct rule and jurisdiction

#### Day 12–13 · S-1 Mint Decision Engine — Both Countries

- [ ] Implement `graph.record_decision()` with `jurisdiction` field:

```python
# Kuwait mint
kwt_decision = kwt_graph.record_decision(
    category="s1_sovereign_mint",
    outcome="mint_siu_t",
    jurisdiction="KWT",
    confidence=0.97,
    rationale="Kuwait Bay baseline stable. Dammam Aquifer within recharge bounds. All 4 KWT nodes green.",
    entities=["kwt_node1_bay", "kwt_node2_dammam", "kwt_node3_mina_ahmadi", "kwt_node4_alzour"],
)

# Saudi Arabia mint
sau_decision = sau_graph.record_decision(
    category="s1_sovereign_mint",
    outcome="mint_siu_t",
    jurisdiction="SAU",
    confidence=0.98,
    rationale="Red Sea eco-shield stable. Wajid/Minjur within recharge bounds. All 4 SAU nodes green.",
    entities=["sau_node1_red_sea", "sau_node2_wajid", "sau_node3_jubail", "sau_node4_king_abdullah"],
)
```

- [ ] Implement `graph.check_decision_rules(decision_id, ruleset="sir_v4_2_kwt_compliance")` and `...sau_compliance`
- [ ] Implement `graph.trace_decision_chain(decision_id)` — returns full causal path back to originating sensor for each country independently
- [ ] Enforce 2:1 over-collateralisation lock at mint time, per country
- [ ] Blocked minting: if Rete returns `approved=False`, raise `MintBlockedError` containing `jurisdiction`, `failing_rule`, and partial causal chain

#### Day 14 · 4:1 Yield Compression Events — Jurisdiction-Scoped

- [ ] Implement independent Ω_Threshold monitors for KWT and SAU
- [ ] Implement jurisdiction-scoped Yield Compression Event:
  - KWT breach → KWT SIU-T locked at 4:1; SAU SIU-T **not affected**
  - SAU breach → SAU SIU-T locked at 4:1; KWT SIU-T **not affected**
- [ ] `record_decision(category="yield_compression", outcome="squeeze_4_1", jurisdiction="KWT"|"SAU")`
- [ ] STOKR stub `/collateral-squeeze` endpoint receives `{jurisdiction, decision_id, causal_chain, new_ratio: "4:1"}`
- [ ] End-to-end test (KWT): inject Node KWT-2 aquifer drawdown breach → KWT Rete fires in < 100ms → KWT 4:1 lock confirmed → SAU unaffected
- [ ] End-to-end test (SAU): inject Node SAU-1 Red Sea brine shift → SAU Rete fires in < 100ms → SAU 4:1 lock confirmed → KWT unaffected

**Week 3 Exit Gate:**

- [ ] All 12 rules (6 KWT + 6 SAU) plus both Covenant Rules enforce deterministically — zero LLM calls in any compliance path
- [ ] Minting is blocked correctly per jurisdiction whenever any rule fails
- [ ] Yield Compression Event fires and locks 4:1 within 100ms per country, with no cross-sovereign contamination
- [ ] `trace_decision_chain()` returns a complete causal path for both mint and squeeze events in both countries

---

### Week 4 — Dashboard, PROV-O Export, Integration Testing & Demo Polish

**July 21–25 · 5 days**

**Goal:** Everything is wired end-to-end across both sovereign configurations. The 14-step demo loop runs cleanly from cold start. PROV-O Turtle exports are valid for both jurisdictions. The system is presentation-ready.

#### Day 15–16 · Next.js Sovereign Intelligence Dashboard — Dual Sovereign View

Build `dashboard/` as a Next.js 14 App Router project. All 8 panels consume live data via WebSocket or REST — zero mocked state in the UI.

##### Global Header — Country Selector

- [ ] Toggle between KWT (Kuwait) and SAU (Saudi Arabia) views — or side-by-side comparison mode
- [ ] Live status indicator per country (green: all nodes healthy / amber: degraded / red: squeeze active)

**Panel 1 — Sovereign Hypergraph (`HypergraphView.tsx`)**

- [ ] Sigma.js + Graphology force-directed graph, rendered per selected country (or side-by-side)
- [ ] Node size = C_B weight; node color = health status (green / amber / red); edge thickness = interdependency strength
- [ ] Click any node → right-side flyout showing live telemetry stream, C_B value, ΣE_D contribution, and Ω_Threshold for that node
- [ ] Animate node color transition on threshold breach (Framer Motion pulse)
- [ ] KWT graph shows KWT-1 → KWT-4 and KWT-2 → KWT-3 interdependency edges
- [ ] SAU graph shows SAU-1 → SAU-4 and SAU-2 → SAU-3 interdependency edges

**Panel 2 — SIU Valuation (`SIUValuationCard.tsx`)**

- [ ] Tremor KPI card with animated counter showing live `SIU_adjusted` per country (separate cards or tabbed)
- [ ] 24hr sparkline beneath the main figure
- [ ] Donut chart (Recharts) breaking down each node's C_B contribution to the final value
- [ ] Ω_Threshold radial gauge — sweeps red as the value approaches Ω_Crit; one gauge per country

**Panel 3 — Collateral Ratio (`CollateralGauge.tsx`)**

- [ ] Two ratio badges side by side: KWT `2:1` / SAU `2:1` (or `4:1` on breach) with Framer Motion spring transition
- [ ] SIU-T circulating supply progress bar vs SIU parent reserve floor per country (Tremor)
- [ ] Countdown timer showing seconds since last compression event, per country

**Panel 4 — PROV-O Lineage Explorer (`ProvenanceGraph.tsx`)**

- [ ] Sigma.js instance rendering the provenance DAG for the currently selected minting decision (jurisdiction-tagged)
- [ ] Click any DAG node → tooltip showing entity IRI, source DOI, author, page number, and confidence score
- [ ] One-click `.ttl` export button wired to `GET /audit/{entity_id}?jurisdiction=KWT|SAU`

**Panel 5 — Node Telemetry Timeline (`NodeTelemetry.tsx`)**

- [ ] Recharts multi-line chart per node showing key sensor metric vs historical baseline
- [ ] Country selector drives which 4-node set is shown
- [ ] Threshold breach markers rendered as vertical red lines
- [ ] Date range selector: 7d / 30d / 1yr / genesis

**Panel 6 — Compression Event Feed (`CompressionFeed.tsx`)**

- [ ] Real-time WebSocket push from `/ws/events/kwt` and `/ws/events/sau` merged into a unified feed
- [ ] Country badge (KWT / SAU) on each event row — color-coded by jurisdiction
- [ ] Expandable causal chain view per event showing `trace_decision_chain()` output

**Panel 7 — Mint Decision Feed (`MintFeed.tsx`)**

- [ ] Live WebSocket feed of all mint and block decisions from both countries
- [ ] Country badge + green `APPROVED` badge or red `BLOCKED — {failing_rule}` badge per row
- [ ] Click decision ID → opens PROV-O Lineage Explorer (Panel 4) for that decision

**Panel 8 — Trigger Control Panel (`TriggerPanel.tsx`)**

- [ ] Node breach buttons for all 8 nodes (4 KWT + 4 SAU), each wired to `POST /simulate/breach`
- [ ] Restore Baseline buttons (per country) wired to `POST /simulate/restore?jurisdiction=KWT|SAU`
- [ ] WebSocket connection status indicator per country in the header

#### Day 17 · W3C PROV-O Audit Export — Per Jurisdiction

- [ ] Implement `RDFExporter.export(lineage, output_path, format="turtle", jurisdiction="KWT"|"SAU")`
- [ ] Each exported file must include jurisdiction IRI, entity IRI, source DOI, PUF flag, ML-KEM flag, and confidence score
- [ ] Kuwait exports named: `kwt_sovereign_audit_trail_{decision_id}.ttl`
- [ ] Saudi Arabia exports named: `sau_sovereign_audit_trail_{decision_id}.ttl`
- [ ] Validate: both Turtle files parse with zero errors in rdflib
- [ ] Generate and validate exports for: all 8 node lineages + most recent KWT mint + most recent SAU mint + most recent KWT squeeze + most recent SAU squeeze

#### Day 18 · FastAPI Integration + STOKR TaaS Stub

Finalise all endpoints in `api/main.py` — all jurisdiction-aware:

- [ ] `POST /ingest?jurisdiction=KWT|SAU` — accepts telemetry packet, routes to correct SHACL gate and graph
- [ ] `GET /siu-value?jurisdiction=KWT|SAU` — returns live `SIU_adjusted` with full C_B, ΣE_D, and Ω breakdown
- [ ] `GET /compliance/{decision_id}` — returns Rete result and causal chain (jurisdiction inferred from decision_id)
- [ ] `POST /mint?jurisdiction=KWT|SAU` — records mint decision for the specified sovereign; checks country rules
- [ ] `GET /audit/{entity_id}?jurisdiction=KWT|SAU` — returns full provenance lineage for a given entity
- [ ] `GET /graph/state?jurisdiction=KWT|SAU&date=YYYY-MM-DD` — bi-temporal snapshot at given date
- [ ] `POST /simulate/breach?jurisdiction=KWT|SAU&node={1|2|3|4}` — injects synthetic threshold breach
- [ ] `POST /simulate/restore?jurisdiction=KWT|SAU` — restores all nodes to baseline for the specified country

Build `api/stokr_stub.py`:

- [ ] Logs all incoming mint triggers and collateral squeeze signals with `jurisdiction`, timestamps, and ratio transitions
- [ ] Document all endpoints with OpenAPI schema auto-generated by FastAPI

#### Day 19 · End-to-End Integration Testing

Run the full 14-step demo loop (7 Kuwait steps + 7 Saudi Arabia steps) and fix all failures before Day 20:

**Kuwait (Steps 1–7):**

1. **Cold start** — KWT Genesis Matrix loads, all 4 KWT nodes appear in the Kuwait hypergraph
2. **Live stream** — 10 packets per KWT node (40 total); 2 corrupted per node → SHACL rejects all 8 bad packets
3. **Centrality** — KWT C_B computed; `KWT_SIU_adjusted` value updates live in the dashboard
4. **Mint** — `POST /mint?jurisdiction=KWT` for Node KWT-3 (Mina Al-Ahmadi) → approved → STOKR stub receives the signal
5. **Breach** — `POST /simulate/breach?jurisdiction=KWT&node=2` triggers a Dammam Aquifer drawdown event
6. **Squeeze** — KWT dashboard shows 4:1 lock within 100ms; SAU collateral ratio remains unchanged at 2:1
7. **Audit** — KWT PROV-O Turtle file generated, validated, and downloadable from the dashboard

**Saudi Arabia (Steps 8–14):**
8. **Cold start verification** — SAU Genesis Matrix loads, all 4 SAU nodes appear in the Saudi Arabia hypergraph
9. **Live stream** — 10 packets per SAU node (40 total); 2 corrupted per node → SAU SHACL rejects all 8 bad packets
10. **Centrality** — SAU C_B computed; `SAU_SIU_adjusted` value updates live; Jubail (SAU-3) holds highest economic C_B
11. **Mint** — `POST /mint?jurisdiction=SAU` for Node SAU-4 (Port of King Abdullah) → approved → STOKR stub receives the signal
12. **Breach** — `POST /simulate/breach?jurisdiction=SAU&node=1` triggers a Red Sea brine shift / coastal eco-shield degradation event
13. **Squeeze** — SAU dashboard shows 4:1 lock within 100ms; KWT collateral ratio remains unchanged at 2:1
14. **Audit** — SAU PROV-O Turtle file generated, validated, and downloadable from the dashboard

- [ ] Fix all integration failures surfaced during the run
- [ ] Performance test: 100 concurrent telemetry packets (50 KWT + 50 SAU) through their respective SHACL gates + graphs in < 5 seconds

#### Day 20 · Demo Hardening & Documentation

- [ ] Freeze the demo scenario script — exact click sequence for the presentation
- [ ] Pre-seed both graphs with full Genesis Matrix data so the demo starts instantly with no load lag
- [ ] Capture backup screenshots of every panel for both country views
- [ ] Write `DEMO_SCRIPT.md` — exact steps, expected outputs, and talking points for every screen, for both KWT and SAU demo sequences
- [ ] Final build test: `docker compose up --build` from a clean environment → all services green within 3 minutes

---

## 7. Deliverables Matrix

| # | Deliverable | Owner | Due | Acceptance Criteria |
|---|---|---|---|---|
| D1 | Genesis Matrix — KWT (4 nodes, synthetic + public data) | Kaif | Jul 4 | LayoutLMv3 cleanroom produces valid Parquet; no tampered entries pass |
| D2 | Genesis Matrix — SAU (4 nodes, synthetic + public data) | Kaif | Jul 4 | LayoutLMv3 cleanroom produces valid Parquet; no tampered entries pass |
| D3 | SHACL Ingestion Gates — KWT + SAU profiles | Kaif | Jul 4 | 100% of injected corrupted packets rejected before graph contact, per country |
| D4 | Bi-Temporal Knowledge Graph — 4 KWT nodes | Kaif | Jul 11 | `kwt_graph.state_at()` returns distinct valid snapshots for 1994, 2010, 2024 |
| D5 | Bi-Temporal Knowledge Graph — 4 SAU nodes | Kaif | Jul 11 | `sau_graph.state_at()` returns distinct valid snapshots for 1990, 2010, 2024 |
| D6 | Betweenness Centrality Engine — both countries | Kaif | Jul 11 | C_B for all 8 nodes in < 50ms per graph; both `SIU_adjusted` formulas live |
| D7 | Provenance Manager — 8 nodes, per-claim attribution | Kaif | Jul 11 | `trace_lineage()` returns ≥ 3-hop chain to DOI for all 8 nodes |
| D8 | Rete Compliance Engine — KWT ruleset (6 rules + covenant) | Kaif | Jul 18 | All KWT rules fire deterministically; zero LLM calls in the compliance path |
| D9 | Rete Compliance Engine — SAU ruleset (6 rules + covenant) | Kaif | Jul 18 | All SAU rules fire deterministically; zero LLM calls in the compliance path |
| D10 | S-1 Mint Decision Tracker — jurisdiction-tagged | Kaif | Jul 18 | `record_decision()` + `check_decision_rules()` + `trace_decision_chain()` working for both KWT and SAU |
| D11 | 4:1 Yield Compression Event — jurisdiction-scoped | Kaif | Jul 18 | KWT breach locks KWT 4:1 in < 100ms, SAU unaffected; SAU breach locks SAU 4:1 in < 100ms, KWT unaffected |
| D12 | Next.js Sovereign Dashboard — 8 panels, dual sovereign view | Kaif | Jul 23 | All panels render live WebSocket data for both countries; breach/restore buttons trigger real graph state changes; two Sigma.js hypergraphs interactive |
| D13 | W3C PROV-O Turtle Export — KWT + SAU | Kaif | Jul 23 | Valid `.ttl` files with all required PROV-O triples for all minting events in both jurisdictions |
| D14 | FastAPI Backend — 8 endpoints (jurisdiction-aware) | Kaif | Jul 24 | All endpoints return correct responses for both KWT and SAU; OpenAPI schema published |
| D15 | End-to-End Demo Loop — 14 steps (7 KWT + 7 SAU) | Kaif | Jul 25 | All 14 steps run clean from cold start |
| D16 | DEMO_SCRIPT.md + Docker Compose Package | Kaif | Jul 25 | Step-by-step script for both country sequences; `docker compose up` starts all services green in < 3 minutes |

---

## 8. Financial Calibration Baseline

The following values are hardcoded in the PoC tokenomics dashboard to represent the Kuwait and Saudi Arabia case studies at sovereign scale. Numbers sourced directly from the SIR V.4.2 Forensic Analysis documents for each jurisdiction.

---

### Kuwait Financial Calibration

#### Kuwait Capital Structure

- **Phase 0 Fixed Deposit** — USD 100,000 (node mapping activation)
- **Multi-Country Pool Contribution** — GDP-proportional share of USD 150,000,000
- **AMM Pool Scale by Day 120** — USD 500,000,000 (shared across all 35 IPCC members)

#### SIU Reserve & Yield — Kuwait

- **Year 1 Total Value Locked (SIU Vault Reserve)** — USD 10,000,000,000
- **Year 2 TVL** — USD 15,000,000,000
- **Year 3 TVL** — USD 20,000,000,000
- **SIU-T Limit (2:1 Over-Collateralisation Lock)** — 50% of TVL
- **Annual Gross Integrity Yield Rate** — 10% of TVL per annum

#### Kuwait Waterfall Distribution (Year 1 Example)

- **Annual Gross Yield** — USD 1,000,000,000
- **Sovereign Net Prosperity Allocation (75%)** — USD 750,000,000
  - 56% Net Liquid Treasury Payout → Central Bank of Kuwait (CBK): **USD 560,000,000**
  - 15% Hardware Refresh Escrow Vault: USD 150,000,000
  - 4% Parametric Insurance Wrap: USD 40,000,000
- **Institutional Pool Allocation (25%)** — USD 250,000,000
  - 3% Local Partner Carve-Out: USD 30,000,000
  - Tech Fee Sliding Scale: USD 220,000,000

#### Kuwait 3-Year Proforma (Dashboard Display)

| Metric | Year 1 | Year 2 | Year 3 |
|---|---|---|---|
| Total Value Locked | $10.0B | $15.0B | $20.0B |
| SIU-T Circulation Limit | $5.0B | $7.5B | $10.0B |
| Annual Gross Integrity Yield | $1.0B | $1.5B | $2.0B |
| Net Liquid Treasury Payout (56%) | $560M | $840M | $1,120M |
| Hardware Refresh Escrow (15%) | $150M | $225M | $300M |
| Parametric Insurance Wrap (4%) | $40M | $60M | $80M |
| **3-Year CBK Treasury Influx** | | | **$2,520,000,000** |
| **3-Year Hardware Escrow Accumulated** | | | **$675,000,000** |

---

### Saudi Arabia Financial Calibration

#### Saudi Arabia Capital Structure

- **Phase 0 Fixed Deposit** — USD 100,000 (node mapping activation)
- **Multi-Country Pool Contribution** — GDP-proportional share of USD 150,000,000
- **AMM Pool Scale by Day 120** — USD 500,000,000 (shared across all 35 IPCC members)

#### SIU Reserve & Yield — Saudi Arabia

- **Year 1 Total Value Locked (SIU Vault Reserve)** — USD 20,000,000,000
- **Year 2 TVL** — USD 30,000,000,000
- **Year 3 TVL** — USD 40,000,000,000
- **SIU-T Limit (2:1 Over-Collateralisation Lock)** — 50% of TVL
- **Annual Gross Integrity Yield Rate** — 10% of TVL per annum

#### Saudi Arabia Waterfall Distribution (Year 1 Example)

- **Annual Gross Yield** — USD 2,000,000,000
- **Sovereign Net Prosperity Allocation (75%)** — USD 1,500,000,000
  - 56% Net Liquid Treasury Payout → Saudi Central Bank (SAMA): **USD 1,120,000,000**
  - 15% Hardware Refresh Escrow Vault: USD 300,000,000
  - 4% Parametric Insurance Wrap: USD 80,000,000
- **Institutional Pool Allocation (25%)** — USD 500,000,000
  - 3% Local Partner Carve-Out: USD 60,000,000
  - Tech Fee Sliding Scale (22%): USD 440,000,000

#### Saudi Arabia 3-Year Proforma (Dashboard Display)

| Metric | Year 1 | Year 2 | Year 3 |
|---|---|---|---|
| Total Value Locked | $20.0B | $30.0B | $40.0B |
| SIU-T Circulation Limit | $10.0B | $15.0B | $20.0B |
| Annual Gross Integrity Yield | $2.0B | $3.0B | $4.0B |
| Net Liquid Treasury Payout (56%) | $1,120M | $1,680M | $2,240M |
| Hardware Refresh Escrow (15%) | $300M | $450M | $600M |
| Parametric Insurance Wrap (4%) | $80M | $120M | $160M |
| **3-Year SAMA Treasury Influx** | | | **$5,040,000,000** |
| **3-Year Hardware Escrow Accumulated** | | | **$1,350,000,000** |

---

### Combined IPCC Consortium Context

- **Total IPCC Pool Capitalization** — USD 150,000,000 (35 participating nations)
- **AMM Liquidity Pool (70% of Total)** — USD 105,000,000
- **AMM Projected Scale by Day 120** — USD 500,000,000
- **Combined KWT + SAU Year 1 TVL** — USD 30,000,000,000
- **Combined KWT + SAU 3-Year Net Treasury Payout** — USD 7,560,000,000

---

## 9. Success Criteria & Acceptance Gates

### Binary Gates — PoC Fails If Any Of These Are Not Met

- **G1 — Deterministic compliance:** 1,000 Rete evaluations on identical inputs produce identical results with zero variance — for both KWT and SAU rulesets independently
- **G2 — Zero LLM in compliance path:** grep or trace confirms no LLM API call is made during any SHACL check or Rete evaluation in either jurisdiction
- **G3 — Squeeze fires < 100ms:** benchmark confirms node breach signal to 4:1 collateral lock in < 100ms at p99 for both KWT and SAU squeeze events
- **G4 — Jurisdiction isolation:** a KWT squeeze event does NOT alter the SAU collateral ratio, and vice versa — confirmed by automated test
- **G5 — Causal chain complete:** `trace_decision_chain()` traces every squeeze event back to the originating sensor node, timestamp, and breach value — for both countries
- **G6 — PROV-O valid:** generated `.ttl` files for both KWT and SAU parse with zero errors in rdflib and contain `prov:Entity`, `prov:wasDerivedFrom`, and `prov:wasAttributedTo` triples
- **G7 — Bi-temporal replay:** `kwt_graph.state_at("1994-01-01")` and `sau_graph.state_at("1990-01-01")` return distinct, non-empty, structurally correct graphs from their 2024 states
- **G8 — SHACL gate:** 100% of intentionally corrupted test packets are rejected before touching the knowledge graph — for both KWT and SAU SHACL profiles

### Quality Targets — Tracked But Not Blockers

- C_B calculation over each 4-node graph: **< 50ms**
- SHACL validation latency per packet: **< 10ms**
- WebSocket telemetry push to dashboard UI: **≤ 200ms** end-to-end
- Sigma.js hypergraph initial render (4 nodes per country): **< 500ms**
- Next.js page initial load (cold): **< 2 seconds** (Lighthouse score ≥ 90)
- Docker cold-start to all-green: **< 3 minutes**
- End-to-end 14-step demo loop: **< 12 minutes**

---

## 10. Risk Register

### Risk 1 — Dual country data volume doubles LayoutLMv3 processing time (Week 1)

- Probability: Medium · Impact: Medium
- Mitigation: Run two parallel Docker containers (one per country cleanroom); pre-process source documents to structured CSV; use LayoutLMv3 only for PDFs with complex layout structures

### Risk 2 — 12-rule Rete compilation increases startup latency

- Probability: Low · Impact: Low
- Mitigation: All rulesets compiled once at service startup; separated into KWT and SAU engines that compile in parallel; expected total startup < 200ms

### Risk 3 — Semantica SDK surface differs from co-dev spec

- Probability: Medium · Impact: High
- Mitigation: Kaif confirms SDK availability on Day 1; build a thin adapter layer if the interface diverges; `jurisdiction` field added as a tagged metadata parameter if not natively supported

### Risk 4 — Synthetic data insufficiently matches Kuwait/Saudi Arabia geophysical reality

- Probability: Low · Impact: Medium
- Mitigation: Use CMEMS, Copernicus Level-2, FAO AQUASTAT, KISR, KAUST, and OPEC open data as the floor; synthetic generation only for gap-fill

### Risk 5 — C_B computation does not hit the 50ms target with two independent graphs

- Probability: Low · Impact: Low
- Mitigation: 4-node graphs are trivially fast; compute KWT and SAU C_B concurrently in two async threads; performance complexity only emerges at 10,000+ node scale

### Risk 6 — Jurisdiction isolation failure — KWT squeeze bleeds into SAU state

- Probability: Medium · Impact: High
- Mitigation: Rete engines and graph instances are fully separate Python objects with no shared mutable state; Ω_Threshold variables namespaced by country; automated test on Day 14 verifies isolation before Week 3 exit gate

### Risk 7 — Next.js dashboard WebSocket drops or Sigma.js render stalls with two simultaneous graph streams

- Probability: Low · Impact: Low
- Mitigation: Two independent WebSocket connections (`/ws/telemetry/kwt` and `/ws/telemetry/sau`); throttle broadcast to 10 events/sec per channel; use Graphology incremental mutation API for both graph instances

### Risk 8 — Squeeze hook timing misses the 100ms SLA (Week 3)

- Probability: Medium · Impact: Medium
- Mitigation: Pre-compile the entire Rete ruleset at startup; never recompile per evaluation call; rule sets are small (6 rules each) and evaluate in O(1) pattern matching

---

## 11. Team & Responsibilities

### Kaif Ahmad — Lead Engineer

- Owns the full stack for both jurisdictions: ingestion pipelines, knowledge graphs, reasoning engines, API, dashboard, and test suite
- Primary point of contact for all Day-1 to Day-20 engineering deliverables

### TFE Lead Architect — Systems Architect

- Defines hardware telemetry specifications, edge enclave data contracts, and node schema validation rules for Kuwait and Saudi Arabia
- Reviews and signs off on the dual-telemetry simulator data contracts for both countries

### Mohd Mohd — Semantica Founder

- Provides Semantica SDK guidance, SHACL/Rete configuration, and PROV-O export specification
- Approves the dual-graph architecture and jurisdiction-tagging approach

### Tizian Rotermund & Egor Sukhanov — STOKR Integration

- Define the TaaS stub API schema for multi-jurisdiction squeeze and mint signals
- Review the STOKR endpoint contract on Day 18

### Mustafa — Demo Stakeholder

- Final demo approval and sovereign pilot acceptance criteria for both Kuwait and Saudi Arabia configurations
- Attends the Week 4 rehearsal on July 24 and demo day on July 25

### Weekly Communication Cadence

- **Daily engineering standup** (Weeks 1–4) — 15 minutes, async if needed
- **Architecture gate review** (end of each week) — 30-minute live call with demo of that week's deliverables
- **Final demo rehearsal** — July 24, full 14-step run-through with all stakeholders present
- **Demo day** — July 25, Mustafa + full team

---

## Appendix A — Repository Structure

```
sir-poc/
├── docker-compose.yml
│
├── backend/
│   ├── ingestion/
│   │   ├── cleanroom.py              # LayoutLMv3 forensic ingest (jurisdiction param)
│   │   ├── shacl_gates.py            # SHACL shape validation and packet rejection
│   │   ├── ontology.ttl              # Base TFE node OWL ontology
│   │   ├── kwt_shapes.ttl            # Kuwait-specific SHACL sensor ranges
│   │   └── sau_shapes.ttl            # Saudi Arabia-specific SHACL sensor ranges
│   ├── graph/
│   │   ├── context_graph.py          # Semantica ContextGraph wrapper (jurisdiction)
│   │   ├── temporal_graph.py         # Bi-temporal KG + Allen Interval Algebra
│   │   └── centrality.py             # Betweenness Centrality engine (per graph)
│   ├── reasoning/
│   │   ├── rete_engine.py            # Deterministic Rete rule compilation (jurisdiction)
│   │   ├── rules/
│   │   │   ├── kwt_rules/
│   │   │   │   ├── bad_neighbor.py   # KWT ecological rules (KWT-1 to KWT-5)
│   │   │   │   └── covenants.py      # KWT sovereign debt covenant rule
│   │   │   └── sau_rules/
│   │   │       ├── bad_neighbor.py   # SAU ecological rules (SAU-1 to SAU-5)
│   │   │       └── covenants.py      # SAU sovereign debt covenant rule
│   │   └── decision_tracker.py       # record_decision + trace_decision_chain (jurisdiction)
│   ├── provenance/
│   │   ├── manager.py                # ProvenanceManager (jurisdiction param)
│   │   └── exporter.py               # RDFExporter → W3C PROV-O Turtle (per jurisdiction)
│   ├── api/
│   │   ├── main.py                   # FastAPI (8 REST endpoints + 4 WebSocket routes)
│   │   └── stokr_stub.py             # STOKR TaaS mock endpoint (jurisdiction-aware)
│   └── data/
│       ├── kuwait/
│       │   ├── node1_kwt_bay/        # Kuwait Bay coastal telemetry data
│       │   ├── node2_kwt_dammam/     # Dammam Aquifer piezometric data
│       │   ├── node3_kwt_mina/       # Mina Al-Ahmadi SCADA and refinery data
│       │   └── node4_kwt_alzour/     # Al-Zour desalination plant data
│       └── saudi_arabia/
│           ├── node1_sau_red_sea/    # Red Sea eco-shield coastal data
│           ├── node2_sau_wajid/      # Wajid/Minjur aquifer data
│           ├── node3_sau_jubail/     # Jubail Industrial City SCADA data
│           └── node4_sau_king_abd/   # King Abdullah Port logistics data
│
├── dashboard/                        # Next.js 14 App Router (TypeScript)
│   ├── app/
│   │   ├── layout.tsx                # Root layout — Tailwind, shadcn theme provider
│   │   ├── page.tsx                  # Main dashboard (all 8 panels, country selector)
│   │   ├── graph/
│   │   │   └── [jurisdiction]/
│   │   │       └── page.tsx          # Full-screen hypergraph per country (kwt | sau)
│   │   └── audit/
│   │       └── [id]/page.tsx         # PROV-O lineage explorer for a decision ID
│   ├── components/
│   │   ├── CountrySelector.tsx       # KWT / SAU toggle + comparison mode
│   │   ├── HypergraphView.tsx        # Sigma.js + Graphology per-country graph
│   │   ├── ProvenanceGraph.tsx       # Sigma.js PROV-O lineage DAG explorer
│   │   ├── SIUValuationCard.tsx      # Tremor KPI card per country
│   │   ├── CollateralGauge.tsx       # Framer Motion 2:1/4:1 badge per country
│   │   ├── NodeTelemetry.tsx         # Recharts multi-line timeline
│   │   ├── CompressionFeed.tsx       # WebSocket live compression event log (both)
│   │   ├── MintFeed.tsx              # WebSocket live mint decision feed (both)
│   │   └── TriggerPanel.tsx          # 8-node breach buttons + per-country restore
│   ├── lib/
│   │   ├── api.ts                    # Typed FastAPI REST client (jurisdiction param)
│   │   └── ws.ts                     # WebSocket manager (kwt + sau channels)
│   ├── tailwind.config.ts
│   ├── next.config.ts
│   └── package.json
│
├── tests/
│   ├── test_shacl_kwt.py
│   ├── test_shacl_sau.py
│   ├── test_rete_kwt.py
│   ├── test_rete_sau.py
│   ├── test_temporal_kwt.py
│   ├── test_temporal_sau.py
│   ├── test_jurisdiction_isolation.py  # Verifies KWT squeeze ≠ SAU squeeze
│   ├── test_provenance.py
│   └── test_e2e.py
└── DEMO_SCRIPT.md
```

---

## Appendix B — Key Code Contracts

### Kuwait Minting Decision

```python
kwt_decision_id = kwt_graph.record_decision(
    category="s1_sovereign_mint",
    outcome="mint_siu_t",
    jurisdiction="KWT",
    confidence=0.97,
    rationale="Kuwait Bay baseline stable. Dammam Aquifer within recharge bounds. All 4 KWT nodes green.",
    entities=["kwt_node1_bay", "kwt_node2_dammam", "kwt_node3_mina_ahmadi", "kwt_node4_alzour"],
)

kwt_compliance = kwt_graph.check_decision_rules(kwt_decision_id, ruleset="sir_v4_2_kwt_compliance")
if not kwt_compliance.approved:
    raise MintBlockedError(f"KWT S-1 Minting Blocked: {kwt_compliance.failing_rule}")

kwt_causal_chain = kwt_graph.trace_decision_chain(kwt_decision_id)
```

### Saudi Arabia Minting Decision

```python
sau_decision_id = sau_graph.record_decision(
    category="s1_sovereign_mint",
    outcome="mint_siu_t",
    jurisdiction="SAU",
    confidence=0.98,
    rationale="Red Sea eco-shield stable. Wajid/Minjur within recharge bounds. All 4 SAU nodes green.",
    entities=["sau_node1_red_sea", "sau_node2_wajid", "sau_node3_jubail", "sau_node4_king_abdullah"],
)

sau_compliance = sau_graph.check_decision_rules(sau_decision_id, ruleset="sir_v4_2_sau_compliance")
if not sau_compliance.approved:
    raise MintBlockedError(f"SAU S-1 Minting Blocked: {sau_compliance.failing_rule}")

sau_causal_chain = sau_graph.trace_decision_chain(sau_decision_id)
```

### Jurisdiction Isolation — Squeeze Event

```python
# Kuwait breach — only KWT collateral ratio changes
kwt_breach = TelemetryPacket(
    jurisdiction="KWT",
    node_id="kwt_node2_dammam",
    reading_type="piezometric_head",
    value=12.3,  # below recharge floor
    unit="m",
    valid_time="2026-07-15T09:42:00Z",
)

ingest_result = kwt_shacl_gate.validate(kwt_breach)
if ingest_result.accepted:
    kwt_graph.assert_fact(...)
    kwt_omega = kwt_graph.recompute_omega()
    if kwt_omega >= KWT_OMEGA_CRIT:
        # ONLY kwt_rete fires — sau_rete is a completely separate instance
        kwt_rete.trigger_yield_compression(jurisdiction="KWT")
        # SAU collateral ratio: still 2:1  ← verified by test_jurisdiction_isolation.py
```

### Temporal Replay — Per Country

```python
kwt_graph = TemporalKnowledgeGraph(jurisdiction="KWT", enable_allen_algebra=True)
sau_graph = TemporalKnowledgeGraph(jurisdiction="SAU", enable_allen_algebra=True)

kwt_snapshot_1994 = kwt_graph.state_at("1994-01-01")  # Kuwait EPA water records begin
sau_snapshot_1990 = sau_graph.state_at("1990-01-01")  # Saudi Aramco SCADA log baseline

kwt_delta = kwt_graph.compute_delta(kwt_snapshot_1994, kwt_graph.state_at("2024-01-01"))
sau_delta = sau_graph.compute_delta(sau_snapshot_1990, sau_graph.state_at("2024-01-01"))
```

### Provenance Export — Per Jurisdiction

```python
# Kuwait audit trail
kwt_prov = ProvenanceManager(jurisdiction="KWT", storage_path="./kwt_audit_trail.db")
kwt_prov.track_entity(
    "kwt_node2_dammam_piezometric",
    source="kuwait_mewa_groundwater_report_2024.pdf",
    metadata={
        "doi": "10.xxxx/kwt.mewa.gw.2024.001",
        "page": 18,
        "author": "Kuwait Ministry of Electricity, Water and Renewable Energy",
        "confidence": 0.94,
    },
)
kwt_lineage = kwt_prov.get_lineage("kwt_node2_dammam_piezometric")
RDFExporter().export(kwt_lineage, "kwt_sovereign_audit_trail.ttl", format="turtle", jurisdiction="KWT")

# Saudi Arabia audit trail
sau_prov = ProvenanceManager(jurisdiction="SAU", storage_path="./sau_audit_trail.db")
sau_prov.track_entity(
    "sau_node2_wajid_piezometric",
    source="saudi_geological_survey_wajid_aquifer_2024.pdf",
    metadata={
        "doi": "10.xxxx/sgs.wajid.2024.001",
        "page": 34,
        "author": "Saudi Geological Survey — Hydrogeology Division",
        "confidence": 0.96,
    },
)
sau_lineage = sau_prov.get_lineage("sau_node2_wajid_piezometric")
RDFExporter().export(sau_lineage, "sau_sovereign_audit_trail.ttl", format="turtle", jurisdiction="SAU")
```

---

*Next action: Kaif to confirm Semantica SDK access and begin Day 1 environment setup on July 1, 2026. Both Kuwait and Saudi Arabia synthetic data pipelines to be initialised simultaneously on Day 1.*
