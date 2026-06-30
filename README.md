# SIR V.4.2 × Semantica

![Version](https://img.shields.io/badge/version-V2.0-0f172a?style=flat-square)
![Protocol](https://img.shields.io/badge/protocol-SIR%20V4.2-1e40af?style=flat-square)
![Status](https://img.shields.io/badge/status-In%20Development-f59e0b?style=flat-square)
![Jurisdictions](https://img.shields.io/badge/jurisdictions-Kuwait%20%7C%20Saudi%20Arabia-16a34a?style=flat-square)
![Classification](https://img.shields.io/badge/classification-RESTRICTED-dc2626?style=flat-square)

**Dual-sovereign Proof of Concept for the Sovereign Integrity Rail.** Semantica serves as the deterministic veracity and accountability middleware between TFE edge hardware and the STOKR settlement ledger, across eight Critical Resource Nodes in Kuwait and Saudi Arabia.

| Field | Value |
| --- | --- |
| Document ID | SEM-TFE-POC-2026-V2.0 |
| Date | June 27, 2026 |
| Jurisdictions | State of Kuwait (CBK) + Kingdom of Saudi Arabia (SAMA) |
| Classification | RESTRICTED — CO-DEVELOPMENT BRIEF |
| Prepared By | Semantica Engineering / Joint Systems Architecture |
| Timeline | July 1 – August 1, 2026 (25 working days) |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Problem Statement](#2-problem-statement)
3. [Architecture and Semantica Responsibilities](#3-architecture-and-semantica-responsibilities)
4. [Sovereign Node Topology](#4-sovereign-node-topology)
5. [Data Flow and Technology Stack](#5-data-flow-and-technology-stack)
6. [5-Week Delivery Plan](#6-5-week-delivery-plan)
7. [Deliverables](#7-deliverables)
8. [API Reference](#8-api-reference)
9. [Financial Calibration Baseline](#9-financial-calibration-baseline)
10. [Acceptance Gates](#10-acceptance-gates)
11. [Risk Register](#11-risk-register)
12. [Team](#12-team)
13. [Appendix A: Repository Structure](#appendix-a-repository-structure)
14. [Appendix B: Code Contracts](#appendix-b-code-contracts)

---

## 1. Executive Summary

This document defines the scope, architecture, and 5-week execution plan for integrating **Semantica** as the veracity and accountability middleware within **The Full Equation (TFE) Sovereign Integrity Rail (SIR) V.4.2**.

Two sovereign case studies run in parallel: the **State of Kuwait** and the **Kingdom of Saudi Arabia**. Each country contributes four Critical Resource Nodes, totalling eight nodes across the PoC. These nodes are drawn directly from the Phase 0 Core-Node activation specifications in the SIR V.4.2 Master Proposals for each sovereign.

The PoC proves that raw biophysical and industrial telemetry from these eight nodes can be converted into auditable, legally defensible **Sovereign Integrity Units (SIUs)**: reserve instruments structured to qualify as Tier-1 High-Quality Liquid Assets (HQLA) on the respective central bank balance sheets of the CBK and SAMA.

**This PoC produces a running system with 17 named deliverables. Not a slide deck.**

### At a Glance

| Metric | Value |
| --- | --- |
| Sovereign case studies | 2 (Kuwait + Saudi Arabia) |
| Critical Resource Nodes | 8 (4 per country) |
| Rete compliance rules | 12 ecological rules + 2 Covenant Rules |
| Acceptance gates | 8 binary pass/fail gates |
| Deliverables | 17 |
| Demo steps | 14 (7 per country) |
| Combined Year 1 TVL | $30,000,000,000 |
| Combined 3-year treasury payout | $7,560,000,000 |
| Squeeze hook SLA | p99 breach-to-lock under 100ms |
| LLM calls in compliance path | Zero |

---

## 2. Problem Statement

### 2.1 The Accountability Gap in Sovereign Asset Minting

When a central bank ingests national natural assets onto its balance sheet to satisfy Tier-1 HQLA reserve criteria, every financial figure and every programmatic decision must be **legally underwritable and mathematically defensible**. The current landscape fails on three axes.

**Traceability gap.** Standard RAG pipelines synthesize documents probabilistically. The synthesis path is invisible. Auditors cannot reconstruct the chain from a token valuation back to the raw sensor reading that caused it.

**Compliance enforcement gap.** Probabilistic LLM reasoning is used to evaluate regulatory rules. Results are inconsistent between runs, non-repeatable under audit, and legally indefensible in court.

**Temporal integrity gap.** Legacy systems use flat changelogs with no bi-temporal tracking. There is no mechanism to prove a historical baseline was untampered, and no way to replay the state of the world as it was on a specific past date.

### 2.2 Kuwait: Unmonetized Assets on the CBK Balance Sheet

Kuwait holds four high-value natural and industrial asset classes that are currently unmonetized:

| Node | Asset Class | At Stake |
| --- | --- | --- |
| KWT-1 | Kuwait Bay Intertidal Eco-Buffer | Desalination intake filter quality and wave attenuation |
| KWT-2 | Dammam Aquifer Matrix | Refinery cooling loops and industrial freshwater supply |
| KWT-3 | Mina Al-Ahmadi Refinery Complex | Primary crude export clearance and SCADA custody transfer |
| KWT-4 | Al-Zour Desalination Complex | National freshwater supply for Kuwait City metropolitan area |

Without a verifiable middleware layer, no international rating agency will underwrite the SIU reserve, no clearinghouse will accept the 4:1 collateral squeeze hook as legally mandated, and no regulator will accept the compliance audit without a deterministic, machine-readable lineage trail.

### 2.3 Saudi Arabia: Unmonetized Assets on the SAMA Balance Sheet

Saudi Arabia holds four high-value sovereign asset classes that are currently unmonetized:

| Node | Asset Class | At Stake |
| --- | --- | --- |
| SAU-1 | Red Sea Coastal Eco-Shield | Wave attenuation and draft depth at King Abdullah Port |
| SAU-2 | Wajid/Minjur Aquifer Plenum | Jubail cooling loops and Eastern Province industrial utility |
| SAU-3 | Jubail Industrial Complex | World's largest single petrochemical export cluster |
| SAU-4 | Port of King Abdullah (Rabigh) | Primary Red Sea deep-water logistics gateway |

Saudi Arabia's $20B initial TVL floor is the largest single-country SIU deployment in the IPCC network. The veracity middleware is more critical here, not less.

### 2.4 What This PoC Proves

Running code against real Kuwait and Saudi Arabian datasets will demonstrate three things:

1. Semantica's deterministic reasoning layer can sit between TFE edge hardware and the STOKR Liquid Network ledger and produce a legally defensible minting signal for both sovereign configurations simultaneously.
2. The resulting SIU minting decision is unbribable, fully auditable, and W3C PROV-O compliant for each jurisdiction independently.
3. The 4:1 Yield Compression Event fires with zero probabilistic dependency and no LLM in the loop, for both the CBK and SAMA configurations.

---

## 3. Architecture and Semantica Responsibilities

### 3.1 Three-Layer Stack

```
┌─────────────────────────────────────────────────────────────────┐
│                    TFE EDGE HARDWARE LAYER                      │
│  Sentinel Hub V.4 (biophysical) + Socket-7 Gateways (SCADA)    │
│  SRAM PUF silicon fingerprinting + ML-KEM-768 encryption        │
│  Kuwait: KWT-1 / KWT-2 / KWT-3 / KWT-4                         │
│  Saudi Arabia: SAU-1 / SAU-2 / SAU-3 / SAU-4                   │
└────────────────────────────┬────────────────────────────────────┘
                             │  Post-Quantum Encrypted Stream
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│            SEMANTICA VERACITY LAYER   (this PoC)                │
│                                                                 │
│  ├─ SHACL Ingestion Gates        kwt_shapes.ttl + sau_shapes.ttl│
│  ├─ LayoutLMv3 Forensic Cleanrooms        one container/country │
│  ├─ Bi-Temporal Knowledge Graphs   KWT hypergraph + SAU hypergraph
│  ├─ Betweenness Centrality Engines           one engine/country │
│  ├─ Rete Compliance Networks        KWT ruleset + SAU ruleset   │
│  ├─ record_decision() + trace_decision_chain()  jurisdiction-tagged
│  └─ W3C PROV-O Export                          one file/event  │
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

### 3.2 SIU Valuation Formula

Each minted SIU is valued by the following formula, computed independently per country:

```
SIU_adjusted = f(C_B × ΣE_D) × (1 − Ω_Threshold)
```

| Variable | Description |
| --- | --- |
| `C_B` | Betweenness Centrality of the node within the country hypergraph |
| `ΣE_D` | Cumulative Downstream Asset Exposure (refinery throughput, desalination output, port volume, infrastructure lifespan) |
| `Ω_Threshold` | Real-time risk probability derived from live SHACL-validated sensor readings |

### 3.3 Collateral Squeeze Rule

```
γ = { 2:1  if Ω_Threshold < Ω_Crit      (normal baseline)
    { 4:1  if Ω_Threshold ≥ Ω_Crit      (Yield Compression Event)
```

When a sensor breach fires in either country's graph, the Rete network (not an LLM) triggers the Yield Compression Event for that sovereign configuration and pushes the 4:1 lock signal to STOKR's TaaS endpoint with a complete, immutable causal path object. A Kuwait breach does not affect Saudi Arabia's collateral state, and vice versa.

---

### 3.4 Semantica Responsibilities

Semantica is the **sole middleware layer** between TFE edge hardware and STOKR's settlement ledger. The following table defines hard ownership boundaries. What Semantica does NOT own: physical hardware collection (TFE), token issuance and settlement (STOKR), SPV legal structuring (STOKR/Sicos), and the LayoutLMv3 model weights (Hugging Face, containerised by Kaif).

| # | Responsibility | SDK Component | Hard Guarantee |
| --- | --- | --- | --- |
| R1 | SHACL Ingestion Gate (KWT + SAU profiles) | `ingestion/shacl_gates.py` | 100% of corrupted packets rejected before graph contact |
| R2 | Bi-Temporal Knowledge Graphs (2 independent graphs) | `graph/temporal_graph.py` | `state_at("YYYY-MM-DD")` replay at any date, per country |
| R3 | Allen Interval Algebra Anomaly Detection | `graph/temporal_graph.py` | Timing anomalies flagged without any LLM call |
| R4 | Betweenness Centrality Engine (2 graphs) | `graph/centrality.py` | C_B for 4 nodes per country in under 50ms |
| R5 | SIU Valuation Formula (live, per country) | `graph/centrality.py` | No off-chain oracle, no LLM interpolation |
| R6 | Rete Compliance Engine (KWT + SAU rulesets) | `reasoning/rete_engine.py` | Deterministic, zero-LLM, 12 rules + 2 Covenant Rules |
| R7 | S-1 Mint Decision Tracker | `reasoning/decision_tracker.py` | Full causal chain to originating sensor, jurisdiction-tagged |
| R8 | 4:1 Yield Compression Event (jurisdiction-scoped) | `reasoning/rete_engine.py` | p99 breach-to-lock under 100ms, no cross-sovereign bleed |
| R9 | Provenance Manager (per-claim source attribution) | `provenance/manager.py` | Every entity traceable via 3+ hops to a DOI or government source |
| R10 | W3C PROV-O Turtle Export (per jurisdiction) | `provenance/exporter.py` | Zero-error rdflib parse on every generated file |

#### R1: SHACL Ingestion Validation Gate

Defines the OWL ontology for all TFE entity types: biophysical node, industrial node, telemetry reading, threshold event, and mint decision. Derives two country-specific SHACL profiles (`kwt_shapes.ttl` and `sau_shapes.ttl`) with jurisdiction-specific sensor ranges and unit constraints. Every raw telemetry packet must pass the appropriate country gate before touching the knowledge graph. Packets that fail are rejected with a plain-English report and never reach the graph layer.

SDK: `ingestion/shacl_gates.py` + `ingestion/ontology.ttl` + `ingestion/kwt_shapes.ttl` + `ingestion/sau_shapes.ttl`

#### R2: Bi-Temporal Knowledge Graph

Stores every asserted fact with two independent timestamps: `valid_time` (when the fact was true in the world) and `recorded_at` (when Semantica ingested it). Maintains two independent hypergraphs, one per country, each queryable at any historical date via `graph.state_at("YYYY-MM-DD")`. This satisfies bi-temporal audit requirements for both CBK and SAMA.

SDK: `graph/temporal_graph.py`

#### R3: Allen Interval Algebra Anomaly Detection

Applies the 13 Allen temporal relations to detect timing anomalies across SCADA and biophysical logs. Flags sequences where a downstream effect precedes its upstream cause, a strong indicator of data tampering or instrument miscalibration, with no LLM interpretation.

SDK: `TemporalKnowledgeGraph(enable_allen_algebra=True)`

#### R4: Betweenness Centrality Engine

Computes C_B for each of the four nodes in each country hypergraph (8 nodes total), quantifying how many shortest paths in the sovereign hypergraph route through each node. Both country calculators run independently. C_B must compute in under 50ms per country graph and feeds directly into each country's SIU valuation formula.

SDK: `graph/centrality.py`

#### R5: SIU Valuation Formula

Computes `SIU_adjusted = f(C_B × ΣE_D) × (1 − Ω_Threshold)` in real time for each country as graph state changes. No off-chain oracle. No LLM interpolation. All three variables are owned and computed by Semantica: `C_B` from the live graph, `ΣE_D` from the Genesis Matrix, and `Ω_Threshold` from live SHACL-validated sensor readings updated on every successful packet ingestion.

SDK: `graph/centrality.py` + `graph/context_graph.py`

#### R6: Rete Compliance Engine

Evaluates all regulatory and ecological rules against every telemetry packet and every mint decision using a pre-compiled Rete network. Maintains two jurisdiction-specific rulesets.

**Kuwait rules (KWT):**

| Rule | Trigger Condition | Effect |
| --- | --- | --- |
| KWT-1 | Dammam Aquifer piezometric drawdown velocity exceeds recharge rate | Reject Node KWT-2; flag `tfe:AquiferBreachEvent`; block KWT minting |
| KWT-2 | Kuwait Bay electrical conductivity spike breaches hypersalinity threshold | Reject Node KWT-1; flag `tfe:HypersalinityEvent`; block KWT minting |
| KWT-3 | Mina Al-Ahmadi SCADA harmonics outside ±2σ of genesis baseline | Reject SCADA stream; flag `tfe:HarmonicAnomalyEvent`; suspend Node KWT-3 |
| KWT-4 | Al-Zour pump thermodynamic signature variance exceeds bounds | Flag `tfe:PumpAnomalyEvent`; blocks minting only after 3 consecutive anomalies |
| KWT-5 | Kuwait Bay benthic sediment transport velocity above siltation threshold | Flag `tfe:SiltationEvent`; block desalination clearance at Node KWT-4 |
| KWT-C | SIU-T circulating supply exceeds 50% of SIU parent reserve | Reject mint; raise structured error immediately |

**Saudi Arabia rules (SAU):**

| Rule | Trigger Condition | Effect |
| --- | --- | --- |
| SAU-1 | Wajid/Minjur aquifer drawdown velocity exceeds recharge rate | Reject Node SAU-2; flag `tfe:AquiferBreachEvent`; block SAU minting |
| SAU-2 | Red Sea coastal thermal gradient or brine shift breaches threshold | Reject Node SAU-1; flag `tfe:BrineShiftEvent`; block SAU minting |
| SAU-3 | Jubail SCADA harmonics outside ±2σ of genesis baseline | Reject SCADA stream; flag `tfe:HarmonicAnomalyEvent`; suspend Node SAU-3 |
| SAU-4 | King Abdullah Port PLC crane load vs. bill of lading divergence exceeds 3% | Flag `tfe:ManifestDiscrepancyEvent`; blocks minting after 3 consecutive divergences |
| SAU-5 | Red Sea kinetic wave attenuation collapse below threshold | Flag `tfe:WaveAttenuationEvent`; block port clearance at Node SAU-4 |
| SAU-C | SIU-T circulating supply exceeds 50% of SIU parent reserve | Reject mint; raise structured error immediately |

**Guarantee:** 1,000 evaluations on identical inputs produce identical outputs. Non-compliance blocks the mint call with a structured error naming the exact failing rule and jurisdiction.

SDK: `reasoning/rete_engine.py` + `reasoning/rules/kwt_rules/` + `reasoning/rules/sau_rules/`

#### R7: S-1 Mint Decision Tracker

Creates an immutable, cryptographically-bound causal object for every minting and squeeze decision, tagged with the sovereign jurisdiction. Semantica must expose three API methods:

- `graph.record_decision()`: writes the decision object to the graph
- `graph.check_decision_rules()`: runs the Rete evaluation and binds the result to the decision
- `graph.trace_decision_chain()`: walks the causal graph backward from the decision to the originating sensor values, timestamps, and breach values

If `check_decision_rules()` returns `approved=False`, the mint call raises a structured error before any signal reaches STOKR.

SDK: `reasoning/decision_tracker.py`

#### R8: 4:1 Yield Compression Event Engine

When `Ω_Threshold ≥ Ω_Crit` in either country graph, the Rete network fires the Yield Compression Event within 100ms. No human in the loop. No LLM. No probabilistic delay. The event is jurisdiction-scoped: a Kuwait breach does not squeeze Saudi Arabia's SIU-T supply.

Sequence owned by Semantica per country:

1. Sensor breach detected in SHACL-validated packet (country-tagged)
2. `Ω_Threshold` updated in the country knowledge graph
3. Rete evaluates the compression rule and fires immediately
4. `record_decision(category="yield_compression", outcome="squeeze_4_1", jurisdiction="KWT"|"SAU")` creates the causal object
5. Causal object posted to STOKR TaaS `/collateral-squeeze` with jurisdiction header
6. Collateral ratio transitions from 2:1 to 4:1 on circulating SIU-T supply for that sovereign only

SLA: p99 latency from breach detection to 4:1 lock confirmation under 100ms.

SDK: `reasoning/rete_engine.py` + `reasoning/decision_tracker.py`

#### R9: Provenance Manager

Tracks every asserted fact in each country knowledge graph to its originating source: document filename, DOI, author, page number, ingestion timestamp, and confidence score. `ProvenanceManager.track_entity()` binds claims at ingestion time. `get_lineage()` walks the full multi-hop ancestor chain. Every entity in the graph must have a provenance chain of at least 3 hops traceable to a DOI or official government source.

SDK: `provenance/manager.py`

#### R10: W3C PROV-O Turtle Export

Converts the provenance graph into a compliance-grade W3C PROV-O Turtle (`.ttl`) file, one per jurisdiction per event. Required triples in every export:

| Triple | Content |
| --- | --- |
| `prov:Entity` | Every tracked data entity |
| `prov:wasDerivedFrom` | Lineage chain |
| `prov:wasAttributedTo` | Source authority (government body or DOI holder) |
| `prov:generatedAtTime` | Ingestion timestamp |
| `prov:wasAssociatedWith` | Sensor or parsing agent that generated the claim |

The generated `.ttl` must parse with zero errors in rdflib before it is accepted as a valid export artifact.

SDK: `provenance/exporter.py`

---

## 4. Sovereign Node Topology

All telemetry is **simulated** using public datasets and synthetic generators calibrated to real specifications for each country.

### 4.1 Kuwait — Four Critical Resource Nodes

#### KWT-1: Kuwait Bay Intertidal Eco-Buffer Strip

| Field | Detail |
| --- | --- |
| Location | Core coastal mudflat and hyper-saline shallow shelf ecosystems, northern Kuwait Bay |
| Track | TFE-ib (biophysical) |
| Hardware | Three Sentinel Hub V.4 marine modules, Inconel 625 chassis with The Shiver piezoelectric transducers |
| Live stream | Coastal thermal gradients, electrical conductivity, benthic sediment transport, intertidal wave attenuation |
| Forensic target | 40 years of daily water-temperature records, channel bathymetric surveys, historical bay water chemistry |
| Downstream effect | Hypersalinity spike degrades seawater intake quality at KWT-4, accelerating filter clogging |

**Data sources:**

| Source | Coverage |
| --- | --- |
| [Kuwait EPA](https://www.epa.gov.kw/) | 40yr daily water temperature, bathymetric surveys, water chemistry (primary baseline) |
| [KISR](https://www.kisr.edu.kw/) | Marine environment research archives, coastal ecosystem baseline studies |
| [Copernicus Marine (CMEMS)](https://marine.copernicus.eu/) | Arabian Gulf SST, salinity profiles, wave energy, sea level anomaly time series |
| [NOAA CoastWatch](https://coastwatch.noaa.gov/) | Satellite-derived SST and coastal chlorophyll concentration |
| [IOC-UNESCO ROPME](http://www.ropme.org/) | Historical Gulf oceanographic and pollution baseline data |
| [Global Mangrove Watch (JAXA)](https://www.eorc.jaxa.jp/ALOS/en/dataset/gmw_e.htm) | Mangrove and intertidal extent time series for Gulf coastlines |
| [Copernicus C3S](https://climate.copernicus.eu/) | Sea level rise projections and storm frequency trends for Ω_Threshold calibration |

---

#### KWT-2: Dammam Subsurface Aquifer Columns

| Field | Detail |
| --- | --- |
| Location | Strategic deep-well fields and subterranean fresh/brackish water columns, Dammam Aquifer Matrix |
| Track | TFE-ib (biophysical) |
| Hardware | Deep exploration probe strings wired to surface Sentinel Hub V.4 cores running neuromorphic SNN ASICs (under 150 mW idle) |
| Live stream | Piezometric hydraulic head indices, aquifer pressure levels, TDS profiles, drawdown recharge velocities |
| Forensic target | 30 years of daily pump registries, deep well pressure charts, geochemical metrics |
| Downstream effect | Piezometric head collapse compromises refinery cooling loops at KWT-3, causing thermodynamic imbalances |

**Data sources:**

| Source | Coverage |
| --- | --- |
| [Kuwait MEWA](https://www.mewa.gov.kw/) | 30yr daily pump registries, deep well pressure charts, geochemical metrics (primary source) |
| [Arab Water Council](https://arabwatercouncil.org/) | Regional aquifer assessments and transboundary water resource reports |
| [FAO AQUASTAT](https://www.fao.org/aquastat/en/) | Kuwait national freshwater resources statistics for ΣE_D coefficient calibration |
| [USGS Groundwater Program](https://www.usgs.gov/mission-areas/water-resources/science/groundwater) | Global fossil aquifer atlas data for Dammam formation baseline |
| [UNESCO-IHP](https://www.unesco.org/en/natural-sciences/water) | International non-renewable aquifer depletion benchmarks |
| [Copernicus Land Service](https://land.copernicus.eu/global/products/swi) | Near-real-time surface moisture for recharge velocity calibration |

---

#### KWT-3: Strategic Hydrocarbon Metabolism Enclave (Mina Al-Ahmadi)

| Field | Detail |
| --- | --- |
| Location | Main crude export pipeline headers, refinery blending manifolds, custody transfer weigh loops, Mina Al-Ahmadi |
| Track | TFE-gdp (SCADA/industrial) |
| Hardware | Socket-7 Industrial Gateways via optically isolated physical hardware taps into plant PLCs |
| Live stream | Multi-phase fluid mass velocities, wellhead pressure profiles, separation plant thermodynamics, custody transfer logs |
| Forensic target | 20 years of SCADA log streams, transport customs weight records, refinery output declarations |

**Data sources:**

| Source | Coverage |
| --- | --- |
| [KNPC Public Reports](https://www.knpc.com/) | 20yr refinery output declarations, annual capacity reports, SCADA utilization (primary source) |
| [Kuwait Petroleum Corporation](https://www.kpc.com.kw/) | Upstream and downstream production benchmarks |
| [OPEC Statistics](https://www.opec.org/opec_web/en/data_graphs/40.htm) | Historical Kuwait crude production and export volumes |
| [IEA Kuwait](https://www.iea.org/countries/kuwait) | Historical refinery throughput, product yield, energy intensity metrics |
| [UN Comtrade](https://comtradeplus.un.org/) | Kuwait petroleum export customs records for bill of lading cross-reference |
| [World Bank Commodity Markets](https://www.worldbank.org/en/research/commodity-markets) | Crude oil price time series for ΣE_D commodity value calibration |

---

#### KWT-4: Al-Zour Mega-Scale Desalination and Utility Complex

| Field | Detail |
| --- | --- |
| Location | Primary seawater intake manifolds, high-pressure pump distributions, chemical balancing lines, Al-Zour |
| Track | TFE-gdp (SCADA/industrial) |
| Hardware | Explosion-hardened Socket-7 Gateways in Mu-Metal and silver-plated copper Faraday cages |
| Live stream | Flow manifold volume velocity, pump thermodynamic signature variations, filter monitoring, terminal head pressures |
| Forensic target | Plant flow meter histories, municipal output logs, inter-utility balance sheets |
| Binding rule | S-1 Mint algorithm binds KWT-4 trade clearings directly to the biophysical risk values of KWT-1 and KWT-2 |

**Data sources:**

| Source | Coverage |
| --- | --- |
| [KAPP Al-Zour Project](https://www.kapp.gov.kw/) | Plant capacity, flow manifold specifications, and output logs |
| [IDA](https://idadesal.org/) | Global desalination plant performance benchmarks and energy intensity |
| [Global Water Intelligence](https://www.globalwaterintel.com/) | Desalination market statistics and operational performance |
| [Kuwait MEWA](https://www.mewa.gov.kw/) | National water production and distribution statistics |
| [World Bank Water Portal](https://data.worldbank.org/indicator/ER.H2O.FWTL.K3) | Kuwait freshwater withdrawal and productivity statistics |
| [IEA Water-Energy Nexus](https://www.iea.org/topics/water) | Desalination energy intensity benchmarks for ΣE_D calibration |

---

### 4.2 Saudi Arabia — Four Critical Resource Nodes

#### SAU-1: Red Sea Coastal Eco-Shield and Maritime Corridor

| Field | Detail |
| --- | --- |
| Location | Intertidal coral-mangrove shield flanking NEOM/Giga-project coastal approach arcs and deep shipment corridors |
| Track | TFE-ib (biophysical) |
| Hardware | Three Sentinel Hub V.4 Marine enclaves, Inconel 625 chassis with The Shiver piezoelectric transducers, 99.9% forensic uptime in hyper-saline spray |
| Live stream | Coastal thermal gradients, electrical conductivity, benthic sediment transport, intertidal wave attenuation |
| Forensic target | 40 years of bathymetric surveys, maritime salinity records, historical temperature logs |
| Downstream effect | Eco-shield degradation triggers wave energy buildup that silts shipping lanes and reduces harbor draft depth at SAU-4 |

**Data sources:**

| Source | Coverage |
| --- | --- |
| [KAUST Red Sea Research Center](https://www.kaust.edu.sa/en/research/center-of-excellence/red-sea-research-center) | Coral reef monitoring, Red Sea oceanographic baselines, temperature/salinity time series (primary source) |
| [Saudi MEWA](https://www.mewa.gov.sa/) | Coastal ecosystem surveys and environmental monitoring reports |
| [Copernicus Marine (CMEMS)](https://marine.copernicus.eu/) | Red Sea SST, salinity profiles, wave energy, tidal surge, sea level anomaly |
| [NOAA CoastWatch](https://coastwatch.noaa.gov/) | Satellite-derived SST and coastal chlorophyll for the Red Sea |
| [IOC-UNESCO ROPME](http://www.ropme.org/) | Red Sea oceanographic baseline data |
| [Global Mangrove Watch (JAXA)](https://www.eorc.jaxa.jp/ALOS/en/dataset/gmw_e.htm) | 40yr mangrove and intertidal extent time series for the Red Sea coastline |
| [Saudi Geological Survey](https://www.sgs.gov.sa/) | Coastal geomorphological surveys and sediment baseline assessments |

---

#### SAU-2: Wajid/Minjur Subterranean Aquifer Plenum

| Field | Detail |
| --- | --- |
| Location | Deep fossil water columns within the Wajid and Minjur aquifer formations, regulating Eastern Province industrial utility |
| Track | TFE-ib (biophysical) |
| Hardware | Deep-well probe strings wired to surface Sentinel Hub V.4 cores; telemetry sealed with SRAM PUF fingerprints and ML-KEM-768 container |
| Live stream | Piezometric hydraulic head indices, deep-formation pressure metrics, TDS profiles, drawdown recharge velocities |
| Forensic target | 30 years of daily pump registries, deep borehole logs, regional hydrogeologic archives |
| Downstream effect | Aquifer over-extraction causes Jubail cooling loop failure, thermodynamic imbalances, and mechanical wear at SAU-3 |

**Data sources:**

| Source | Coverage |
| --- | --- |
| [Saudi MEWA](https://www.mewa.gov.sa/) | Groundwater monitoring reports, borehole logs, extraction permit registries (primary source) |
| [Saudi Geological Survey](https://www.sgs.gov.sa/) | Wajid and Minjur aquifer formation mapping, pressure logs, TDS geochemical archives |
| [FAO AQUASTAT](https://www.fao.org/aquastat/en/) | National freshwater resources statistics and fossil aquifer depletion assessments |
| [Arab Water Council](https://arabwatercouncil.org/) | Transboundary aquifer assessments for the Arabian Shield and Rub al Khali basin |
| [UNESCO-IHP](https://www.unesco.org/en/natural-sciences/water) | Fossil aquifer depletion rate benchmarks |
| [ESA CCI Soil Moisture](https://www.esa-soilmoisture-cci.org/) | Regional recharge velocity calibration from surface moisture indices |

---

#### SAU-3: Strategic Industrial Metabolism Enclave (Jubail Complex Core)

| Field | Detail |
| --- | --- |
| Location | Primary pipeline manifolds, automated cracking plant arrays, refinery blending manifold headers, Jubail Industrial City |
| Track | TFE-gdp (SCADA/industrial) |
| Hardware | Socket-7 Gateways via optically isolated physical taps into plant PLCs and SCADA networks; runs Resonant Signature Identification (RSID) |
| Live stream | Multi-phase fluid mass velocities, wellhead pressure profiles, chemical separation thermodynamics, custody transfer logs |
| Forensic target | 20 years of SCADA log streams, customs weight records, refinery output declarations from Saudi Aramco and Jubail |

**Data sources:**

| Source | Coverage |
| --- | --- |
| [Saudi Aramco Annual Reports](https://www.aramco.com/en/investors/annual-report) | 20yr production data, downstream refining capacity, SCADA utilization (primary source) |
| [SABIC Annual Reports](https://www.sabic.com/en/investors/annual-reports) | Jubail petrochemical output, plant capacity, operational metrics |
| [Royal Commission for Jubail and Yanbu](https://www.rcjy.gov.sa/) | Industrial city production statistics, energy and water consumption |
| [OPEC Statistics](https://www.opec.org/opec_web/en/data_graphs/40.htm) | Saudi Arabia historical crude production and export volumes |
| [IEA Saudi Arabia](https://www.iea.org/countries/saudi-arabia) | Refinery throughput, product yield, energy intensity time series |
| [UN Comtrade](https://comtradeplus.un.org/) | Petroleum and petrochemical export customs records for bill of lading cross-reference |

---

#### SAU-4: Port of King Abdullah Logistics Terminal Gantries

| Field | Detail |
| --- | --- |
| Location | Automated container gantry crane networks, dry bulk loaders, outbound electronic scale networks, King Abdullah Port (Rabigh) |
| Track | TFE-gdp (SCADA/industrial) |
| Hardware | Hardened Socket-7 Gateways in Mu-Metal and silver-plated copper Faraday cages, shielding atomic clocks from port marine radar fields |
| Live stream | PLC crane load weights, container tracking manifests, freight velocity, gate-clearance manifests |
| Forensic target | Shipping bills of lading, automated freight weight logs, international customs tracking manifests |
| Binding rule | S-1 Mint algorithm binds SAU-4 trade volume clearings directly to the biophysical risk values of SAU-1 and SAU-2 |

**Data sources:**

| Source | Coverage |
| --- | --- |
| [Mawani (Saudi Ports Authority)](https://www.mawani.gov.sa/) | Container throughput, berth occupancy, crane utilization, gate-clearance manifests (primary source) |
| [UNCTAD Maritime Statistics](https://unctadstat.unctad.org/) | Red Sea port container TEU throughput for ΣE_D trade velocity calibration |
| [World Bank Container Port Traffic](https://datacatalog.worldbank.org/search/dataset/0038027) | Historical TEU benchmark series for regional ports |
| [IMO GISIS](https://gisis.imo.org/) | Vessel registration, cargo manifests, port state control records |
| [MarineTraffic AIS](https://www.marinetraffic.com/) | Vessel movement data for freight velocity simulation and anomaly detection |
| [Saudi Customs (Zatca)](https://www.zatca.gov.sa/) | Import/export declarations and bill of lading cross-reference |

---

## 5. Data Flow and Technology Stack

### 5.1 Data Flow

```
[Public + Synthetic Kuwait Data]       [Public + Synthetic Saudi Arabia Data]
          │                                           │
          ▼                                           ▼
┌──────────────────────────┐           ┌──────────────────────────┐
│  LayoutLMv3 Cleanroom    │           │  LayoutLMv3 Cleanroom    │
│  KWT — 4 nodes           │           │  SAU — 4 nodes           │
│  output: Genesis Matrix  │           │  output: Genesis Matrix  │
└────────────┬─────────────┘           └─────────────┬────────────┘
             │                                       │
      ┌──────┴───────┐                       ┌───────┴──────┐
      ▼              ▼                       ▼              ▼
┌──────────┐  ┌──────────┐           ┌──────────┐  ┌──────────┐
│  TFE-ib  │  │  TFE-gdp │           │  TFE-ib  │  │  TFE-gdp │
│  KWT-1,2 │  │  KWT-3,4 │           │  SAU-1,2 │  │  SAU-3,4 │
└────┬─────┘  └────┬─────┘           └────┬─────┘  └────┬─────┘
     └──────┬──────┘                       └──────┬──────┘
            ▼                                     ▼
  ┌───────────────────┐                 ┌───────────────────┐
  │  SHACL Gate (KWT) │                 │  SHACL Gate (SAU) │
  │  kwt_shapes.ttl   │                 │  sau_shapes.ttl   │
  └─────────┬─────────┘                 └─────────┬─────────┘
            ▼                                     ▼
  ┌─────────────────────┐             ┌─────────────────────┐
  │  KWT Knowledge Graph│             │  SAU Knowledge Graph│
  │  Bi-Temporal        │             │  Bi-Temporal        │
  │  Centrality Engine  │             │  Centrality Engine  │
  │  Rete (KWT rules)   │             │  Rete (SAU rules)   │
  │  ProvenanceManager  │             │  ProvenanceManager  │
  └────┬──────────┬──────┘             └────┬──────────┬─────┘
       │          │                         │          │
  record_    PROV-O                    record_    PROV-O
  decision   export                    decision   export
       │          │                         │          │
       └──────────┴──────────┬──────────────┴──────────┘
                             ▼
                  ┌─────────────────────┐
                  │  FastAPI + WebSocket │
                  │  Unified API Layer   │
                  └──────────┬──────────┘
                             │
              ┌──────────────┴────────────────┐
              ▼                               ▼
  ┌─────────────────────┐         ┌─────────────────────┐
  │  Next.js Dashboard  │         │  STOKR TaaS Stub    │
  │  Dual Sovereign View│         │  /collateral-squeeze│
  │  KWT + SAU panels   │         │  /mint-signal       │
  └─────────────────────┘         └─────────────────────┘
```

### 5.2 Backend Stack

| Layer | Technology | Purpose |
| --- | --- | --- |
| Document parsing | LayoutLMv3 (Hugging Face) in Docker | Two parallel forensic cleanroom containers, one per country |
| Knowledge graph | Semantica ContextGraph + TemporalKnowledgeGraph | Instantiated twice: KWT and SAU |
| Validation | pySHACL + rdflib + OWL ontology | Two country-specific SHACL shape profiles |
| Reasoning | Semantica ReteEngine | Deterministic, zero-LLM; two country-specific rulesets compiled at startup |
| Provenance | Semantica ProvenanceManager + RDFExporter | Per-claim attribution and W3C PROV-O Turtle generation |
| Graph algorithms | Semantica CentralityCalculator | Betweenness Centrality computed per country graph |
| API | FastAPI with WebSocket support | 8 REST endpoints + 4 WebSocket routes, all jurisdiction-aware |
| Data simulation | NumPy + Pandas + synthetic generators | Gap-fill on top of public data |
| Containerisation | Docker Compose | Single `docker compose up` boots all services |
| Testing | pytest (unit + integration) + locust (load) | Per-country test suites + jurisdiction isolation tests |

### 5.3 Frontend Stack

| Layer | Technology | Purpose |
| --- | --- | --- |
| Framework | Next.js 14 (App Router, TypeScript) | SSR + client components, App Router file-based routing |
| Styling | Tailwind CSS + shadcn/ui | Consistent component primitives and dark/light theming |
| Dashboard components | Tremor | KPI cards, sparklines, area charts, progress bars |
| Sovereign hypergraph | Sigma.js + Graphology | Force-directed hypergraphs for KWT and SAU, rendered side-by-side or toggled |
| Time-series charts | Recharts | Node telemetry timelines, C_B trend lines, Ω_Threshold history |
| Live data | Native WebSocket client | `/ws/telemetry/kwt` and `/ws/telemetry/sau` push streams, no polling |
| Animations | Framer Motion | Collateral ratio transitions, breach pulse alerts, panel state changes |

---

## 6. 5-Week Delivery Plan

**Timeline:** July 1 to August 1, 2026. 25 working days. Hard milestone at the end of each week.

---

### Week 1: Foundation, Dual-Country Data and Ingestion

**July 1 to 4 (4 days)**

**Goal:** The skeleton runs for both countries. All eight nodes have synthetic data flowing through the ingestion pipelines and SHACL is catching bad packets for both Kuwait and Saudi Arabia.

#### Days 1 and 2: Environment and Data Setup

- [ ] Initialise monorepo structure: `/ingestion`, `/graph`, `/reasoning`, `/api`, `/dashboard`, `/tests`, `/data/kuwait`, `/data/saudi_arabia`
- [ ] Docker Compose stack: two LayoutLMv3 cleanroom services (KWT + SAU), Semantica service, FastAPI service, dashboard dev server
- [ ] Generate synthetic telemetry for all 8 nodes:
  - **KWT-1:** 40yr Kuwait Bay water temperature, conductivity, bathymetric charts (CSV)
  - **KWT-2:** 30yr Dammam Aquifer pump registries, piezometric head charts, TDS logs
  - **KWT-3:** 20yr Mina Al-Ahmadi SCADA vibration logs in Modbus/TCP simulation format
  - **KWT-4:** Al-Zour plant flow meter histories, pump thermodynamic signatures, municipal output logs
  - **SAU-1:** 40yr Red Sea bathymetric surveys, maritime salinity records, coastal temperature logs
  - **SAU-2:** 30yr Wajid/Minjur daily pump registries, borehole logs, hydrogeologic archives
  - **SAU-3:** 20yr Jubail SCADA log streams, refinery output declarations, customs weight records
  - **SAU-4:** King Abdullah Port shipping manifests, PLC crane load weights, gate-clearance records
- [ ] Seed with public data: CMEMS (Red Sea + Arabian Gulf), Copernicus Level-2, FAO AQUASTAT, UNCTAD, UN Comtrade

#### Days 3 and 4: Forensic Cleanrooms and SHACL Gates

- [ ] Containerise two LayoutLMv3 document parsing pipelines, one per country
- [ ] Build `ingestion/cleanroom.py` with `jurisdiction` parameter: ingests CSVs and PDFs, purges anomalous entries, outputs Genesis Matrix per country as Parquet
- [ ] Define base OWL ontology for TFE entity types: biophysical node, industrial node, telemetry reading, threshold event
- [ ] Derive `kwt_shapes.ttl` and `sau_shapes.ttl` with country-specific sensor unit ranges, conductivity thresholds, and pressure bounds
- [ ] SHACL gate behaviour: out-of-range or malformed packets are rejected with a plain-English validation report and never reach the graph
- [ ] Unit tests: inject 10 corrupted packets per country (20 total); assert all 20 rejected

**Week 1 exit gate:**

- [ ] All 8 node datasets loaded and versioned in `/data/kuwait/` and `/data/saudi_arabia/`
- [ ] Both LayoutLMv3 cleanrooms producing valid Genesis Matrix Parquet files with no tampered entries passing
- [ ] Both SHACL gates demonstrably rejecting malformed telemetry on every run
- [ ] `docker compose up` starts all services clean with no errors

---

### Week 2: Dual Knowledge Graphs, Temporal Engines and Centrality

**July 7 to 11 (5 days)**

**Goal:** Both 4-node hypergraphs are live. Bi-temporal state replay works at any historical date for each country. Betweenness Centrality fires sub-50ms per graph.

#### Days 5 and 6: Bi-Temporal Knowledge Graphs

- [ ] Initialise `ContextGraph(jurisdiction="KWT", advanced_analytics=True)` with 4 nodes and interdependency edges:
  - KWT-1 to KWT-4 (hypersalinity drives desalination intake quality)
  - KWT-2 to KWT-3 (piezometric head drives refinery cooling loop)
- [ ] Initialise `ContextGraph(jurisdiction="SAU", advanced_analytics=True)` with 4 nodes and interdependency edges:
  - SAU-1 to SAU-4 (wave attenuation drives port structural integrity and draft depth)
  - SAU-2 to SAU-3 (aquifer drawdown drives Jubail cooling loop efficiency)
- [ ] Tag every graph edge with `valid_time` and `recorded_at` in both graphs
- [ ] Implement `graph.state_at("YYYY-MM-DD")` for both graphs
- [ ] Load KWT Genesis Matrix into KWT graph; SAU Genesis Matrix into SAU graph
- [ ] Enable Allen Interval Algebra anomaly detection on both graphs
- [ ] Tests: `kwt_graph.state_at("1990-01-01")` and `sau_graph.state_at("1990-01-01")` both return valid non-empty graphs distinct from their 2024 states

#### Days 7 and 8: Betweenness Centrality

- [ ] `CentralityCalculator(graph=kwt_graph)` computing C_B for all four Kuwait nodes:
  - KWT-1: high ecological C_B; hypersalinity cascades to KWT-4 and the industrial supply chain
  - KWT-2: moderate-high C_B; water-table drawdown propagates to refinery cooling at KWT-3
  - KWT-3: high economic C_B; crude export clearance routes through this node
  - KWT-4: highest national utility C_B; municipal freshwater for all of Kuwait City
- [ ] `CentralityCalculator(graph=sau_graph)` computing C_B for all four Saudi Arabia nodes:
  - SAU-1: high ecological C_B; coral-mangrove buffer stabilises port draft depth at SAU-4
  - SAU-2: high resource C_B; Wajid/Minjur is the primary industrial water tower for the Eastern Province
  - SAU-3: highest economic C_B; Jubail is the world's largest single petrochemical export complex
  - SAU-4: high logistics C_B; King Abdullah Port is the primary deep-water gateway for industrial export
- [ ] Implement ΣE_D coefficients for both countries from Genesis Matrix
- [ ] Implement live SIU valuation for both countries:

  ```python
  kwt_siu = f(kwt_C_B * kwt_sum_E_D) * (1 - kwt_omega)
  sau_siu = f(sau_C_B * sau_sum_E_D) * (1 - sau_omega)
  ```

- [ ] Benchmark: C_B for 4 nodes per country in under 50ms each

#### Day 9: Provenance Binding

- [ ] Implement `ProvenanceManager(jurisdiction="KWT")` and `ProvenanceManager(jurisdiction="SAU")`
- [ ] Bind KWT-1 coastal data to KISR/EPA synthetic records with DOI metadata
- [ ] Bind KWT-2 aquifer data to MEWA pump registry synthetic source
- [ ] Bind SAU-1 Red Sea data to KAUST RSRC synthetic records with DOI metadata
- [ ] Bind SAU-2 aquifer data to Saudi Geological Survey synthetic borehole source
- [ ] Unit tests: `prov.get_lineage("kwt_node1_bay_salinity")` and `prov.get_lineage("sau_node2_wajid_piezometric")` both return at least 3-hop chains

**Week 2 exit gate:**

- [ ] `kwt_graph.state_at("2010-01-01")` and `sau_graph.state_at("2010-01-01")` return distinct, structurally correct snapshots from their 2024 states
- [ ] C_B computed for all 8 nodes, confirmed sub-50ms per country
- [ ] `KWT_SIU_adjusted` and `SAU_SIU_adjusted` both computing live against real graph state
- [ ] Full provenance chain traced for at least one fact per node (8 nodes total)

---

### Week 3: Dual Rete Engine, Mint Logic and Squeeze Hooks

**July 14 to 18 (5 days)**

**Goal:** Both policy engines are live. Minting is gated by deterministic rules per jurisdiction. The 4:1 squeeze fires within 100ms of any threshold breach without cross-contaminating the other sovereign's collateral state.

#### Days 10 and 11: Rete Network Compilation

Compile the full rule libraries into `ReteEngine(jurisdiction="KWT")` and `ReteEngine(jurisdiction="SAU")` as specified in Section 3.4, R6.

- [ ] All 12 ecological rules compiled (6 KWT + 6 SAU)
- [ ] Both Covenant Rules compiled (KWT-C + SAU-C)
- [ ] `ReteEngine(jurisdiction).evaluate(telemetry_packet)` returning `{approved: bool, failing_rule: str | None, jurisdiction: str}`
- [ ] Test: 5 compliant packets per country pass; 5 non-compliant per country fail naming the exact rule and jurisdiction

#### Days 12 and 13: S-1 Mint Decision Engine

- [ ] Implement `graph.record_decision()` with `jurisdiction` field (see Appendix B for contract)
- [ ] Implement `graph.check_decision_rules(decision_id, ruleset="sir_v4_2_kwt_compliance")` and `...sau_compliance`
- [ ] Implement `graph.trace_decision_chain(decision_id)` returning full causal path to originating sensor per country
- [ ] Enforce 2:1 over-collateralisation lock at mint time, per country
- [ ] Blocked minting: Rete returning `approved=False` raises `MintBlockedError` containing `jurisdiction`, `failing_rule`, and partial causal chain

#### Day 14: Jurisdiction-Scoped Yield Compression Events

- [ ] Implement independent Ω_Threshold monitors for KWT and SAU
- [ ] Implement jurisdiction-scoped squeeze: KWT breach locks KWT at 4:1 and leaves SAU at 2:1; SAU breach locks SAU at 4:1 and leaves KWT at 2:1
- [ ] `record_decision(category="yield_compression", outcome="squeeze_4_1", jurisdiction="KWT"|"SAU")`
- [ ] STOKR stub `/collateral-squeeze` endpoint receives `{jurisdiction, decision_id, causal_chain, new_ratio: "4:1"}`
- [ ] E2E test (KWT): inject KWT-2 aquifer drawdown breach → KWT Rete fires in under 100ms → KWT 4:1 lock confirmed → SAU unaffected
- [ ] E2E test (SAU): inject SAU-1 Red Sea brine shift → SAU Rete fires in under 100ms → SAU 4:1 lock confirmed → KWT unaffected

**Week 3 exit gate:**

- [ ] All 12 rules plus both Covenant Rules enforce deterministically with zero LLM calls in any compliance path
- [ ] Minting is blocked correctly per jurisdiction whenever any rule fails
- [ ] Yield Compression Event fires and locks 4:1 within 100ms per country with no cross-sovereign contamination
- [ ] `trace_decision_chain()` returns a complete causal path for both mint and squeeze events in both countries

---

### Week 4: Dashboard, PROV-O Export and Integration Testing

**July 21 to 25 (5 days)**

**Goal:** Everything is wired end-to-end across both sovereign configurations. The 14-step demo loop runs cleanly from cold start. PROV-O exports are valid for both jurisdictions. The system is presentation-ready.

#### Days 15 and 16: Next.js Sovereign Intelligence Dashboard

Build `dashboard/` as a Next.js 14 App Router project. All 8 panels consume live data via WebSocket or REST. Zero mocked state in the UI.

| Panel | Component | Data Source |
| --- | --- | --- |
| Global header: country selector | `CountrySelector.tsx` | Toggle KWT/SAU or side-by-side; per-country health indicator |
| 1: Sovereign Hypergraph | `HypergraphView.tsx` | Sigma.js + Graphology; node size = C_B; node color = health; click for flyout |
| 2: SIU Valuation | `SIUValuationCard.tsx` | Tremor KPI card; 24hr sparkline; Recharts donut (C_B breakdown); Ω gauge |
| 3: Collateral Ratio | `CollateralGauge.tsx` | Framer Motion badge (2:1 or 4:1); SIU-T progress bar; compression timer |
| 4: PROV-O Lineage | `ProvenanceGraph.tsx` | Sigma.js DAG; click node for entity IRI, DOI, author, confidence; one-click .ttl download |
| 5: Node Telemetry Timeline | `NodeTelemetry.tsx` | Recharts multi-line chart; breach markers as vertical red lines; date range: 7d/30d/1yr/genesis |
| 6: Compression Event Feed | `CompressionFeed.tsx` | WebSocket `/ws/events/kwt` and `/ws/events/sau`; KWT/SAU badge; expandable causal chain |
| 7: Mint Decision Feed | `MintFeed.tsx` | WebSocket; APPROVED (green) or BLOCKED (red, failing rule); click to open Panel 4 |
| 8: Trigger Control Panel | `TriggerPanel.tsx` | 8 breach buttons (4 KWT + 4 SAU) wired to `POST /simulate/breach`; restore buttons per country |

#### Day 17: W3C PROV-O Audit Export

- [ ] Implement `RDFExporter.export(lineage, output_path, format="turtle", jurisdiction="KWT"|"SAU")`
- [ ] Each export must include: jurisdiction IRI, entity IRI, source DOI, SRAM PUF flag, ML-KEM flag, confidence score
- [ ] Kuwait exports: `kwt_sovereign_audit_trail_{decision_id}.ttl`
- [ ] Saudi Arabia exports: `sau_sovereign_audit_trail_{decision_id}.ttl`
- [ ] Validate: both Turtle files parse with zero errors in rdflib
- [ ] Generate and validate exports for all 8 node lineages + most recent mint and squeeze events for both countries

#### Day 18: FastAPI Finalisation and STOKR Stub

Finalise all endpoints in `api/main.py`. All endpoints are jurisdiction-aware. See Section 8 for the full API reference.

- [ ] All 8 REST endpoints returning correct responses for both KWT and SAU
- [ ] All 4 WebSocket routes streaming live telemetry per country
- [ ] `api/stokr_stub.py` logging all mint triggers and squeeze signals with jurisdiction, timestamps, and ratio transitions
- [ ] OpenAPI schema auto-generated and accessible at `/docs`

#### Day 19: End-to-End Integration Testing

Run the full 14-step demo loop and fix all failures before Week 5.

**Kuwait (Steps 1 to 7):**

1. **Cold start.** KWT Genesis Matrix loads; all 4 KWT nodes appear in the Kuwait hypergraph.
2. **Live stream.** 10 packets per KWT node (40 total); 2 corrupted per node; SHACL rejects all 8 bad packets.
3. **Centrality.** KWT C_B computed; `KWT_SIU_adjusted` updates live in the dashboard.
4. **Mint.** `POST /mint?jurisdiction=KWT` for Node KWT-3 (Mina Al-Ahmadi); approved; STOKR stub receives the signal.
5. **Breach.** `POST /simulate/breach?jurisdiction=KWT&node=2` triggers a Dammam Aquifer drawdown event.
6. **Squeeze.** KWT dashboard shows 4:1 lock within 100ms; SAU collateral ratio remains at 2:1.
7. **Audit.** KWT PROV-O Turtle file generated, validated, and downloadable from the dashboard.

**Saudi Arabia (Steps 8 to 14):**

8. **Cold start.** SAU Genesis Matrix loads; all 4 SAU nodes appear in the Saudi Arabia hypergraph.
9. **Live stream.** 10 packets per SAU node (40 total); 2 corrupted per node; SAU SHACL rejects all 8 bad packets.
10. **Centrality.** SAU C_B computed; `SAU_SIU_adjusted` updates live; Jubail (SAU-3) holds highest economic C_B.
11. **Mint.** `POST /mint?jurisdiction=SAU` for Node SAU-4 (Port of King Abdullah); approved; STOKR stub receives the signal.
12. **Breach.** `POST /simulate/breach?jurisdiction=SAU&node=1` triggers a Red Sea brine shift event.
13. **Squeeze.** SAU dashboard shows 4:1 lock within 100ms; KWT collateral ratio remains at 2:1.
14. **Audit.** SAU PROV-O Turtle file generated, validated, and downloadable from the dashboard.

- [ ] Fix all integration failures surfaced during the run
- [ ] Performance test: 100 concurrent telemetry packets (50 KWT + 50 SAU) through respective SHACL gates and graphs in under 5 seconds

**Week 4 exit gate:**

- [ ] All 8 dashboard panels render live WebSocket/REST data for both KWT and SAU with zero mocked state
- [ ] Both PROV-O Turtle exports valid and parse with zero rdflib errors
- [ ] All 8 REST endpoints and 4 WebSocket routes return correct, jurisdiction-aware responses
- [ ] Full 14-step demo loop (7 KWT + 7 SAU) runs end-to-end from cold start with all failures logged for Week 5 burn-down

---

### Week 5: Hardening, Contingency Buffer and Demo Readiness

**July 28 to August 1 (5 days)**

**Goal:** No new features. This week exists to absorb risk: burn down whatever Week 4 testing surfaced, run a full regression against all 8 binary acceptance gates, and rehearse the demo until it is boring.

#### Day 20: Full Gate Regression and Contingency Burn-Down

- [ ] Re-run G1 to G8 (Section 10) back-to-back in a single automated suite; log pass/fail per gate per jurisdiction
- [ ] Fix any failures carried over from the Day 19 integration run, prioritised by which acceptance gate they block
- [ ] Re-run the 1,000-evaluation Rete determinism check (G1) and the p99 squeeze latency benchmark (G3) under load

#### Day 21: Demo Hardening

- [ ] Freeze the demo scenario script with exact click sequence, expected outputs, and talking points
- [ ] Pre-seed both graphs with full Genesis Matrix data so the demo starts with no load lag
- [ ] Capture backup screenshots of every panel for both country views, in case of live failure
- [ ] Write `DEMO_SCRIPT.md` covering both KWT and SAU sequences

#### Day 22: Clean-Environment Build Verification

- [ ] Final build test: `docker compose up --build` from a clean environment (no cached layers, no pre-pulled images)
- [ ] Confirm all services reach green health checks within 3 minutes
- [ ] Re-validate both `.ttl` exports and the OpenAPI schema against the clean-build instance

#### Day 23: Final Demo Rehearsal

- [ ] Full 14-step run-through with all stakeholders (Section 12 communication cadence)
- [ ] Time the run against the under-12-minute target; trim or reorder steps if needed
- [ ] Collect and resolve any last feedback from TFE, STOKR, and Mustafa

#### Day 24: Demo Day Buffer

- [ ] Reserve day for any fixes surfaced in rehearsal; no new scope introduced
- [ ] Final `docker compose up` smoke test immediately before the live session

**Week 5 exit gate:**

- [ ] All 8 binary acceptance gates (G1 to G8) pass in a single clean regression run, for both KWT and SAU
- [ ] `DEMO_SCRIPT.md` finalised and matches the actual rehearsed sequence
- [ ] `docker compose up --build` from a clean environment reaches all-green in under 3 minutes
- [ ] Final demo rehearsal completed with stakeholder sign-off ahead of demo day

---

## 7. Deliverables

| # | Deliverable | Owner | Due | Acceptance Criteria |
| --- | --- | --- | --- | --- |
| D1 | Genesis Matrix: KWT (4 nodes, synthetic + public data) | Kaif | Jul 4 | LayoutLMv3 cleanroom produces valid Parquet; no tampered entries pass |
| D2 | Genesis Matrix: SAU (4 nodes, synthetic + public data) | Kaif | Jul 4 | LayoutLMv3 cleanroom produces valid Parquet; no tampered entries pass |
| D3 | SHACL Ingestion Gates: KWT and SAU profiles | Kaif | Jul 4 | 100% of injected corrupted packets rejected before graph contact, per country |
| D4 | Bi-Temporal Knowledge Graph: 4 KWT nodes | Kaif | Jul 11 | `kwt_graph.state_at()` returns distinct valid snapshots for 1994, 2010, and 2024 |
| D5 | Bi-Temporal Knowledge Graph: 4 SAU nodes | Kaif | Jul 11 | `sau_graph.state_at()` returns distinct valid snapshots for 1990, 2010, and 2024 |
| D6 | Betweenness Centrality Engine: both countries | Kaif | Jul 11 | C_B for all 8 nodes in under 50ms per graph; both `SIU_adjusted` formulas live |
| D7 | Provenance Manager: 8 nodes, per-claim attribution | Kaif | Jul 11 | `trace_lineage()` returns at least 3-hop chain to DOI for all 8 nodes |
| D8 | Rete Compliance Engine: KWT ruleset (6 rules + covenant) | Kaif | Jul 18 | All KWT rules fire deterministically; zero LLM calls in the compliance path |
| D9 | Rete Compliance Engine: SAU ruleset (6 rules + covenant) | Kaif | Jul 18 | All SAU rules fire deterministically; zero LLM calls in the compliance path |
| D10 | S-1 Mint Decision Tracker: jurisdiction-tagged | Kaif | Jul 18 | `record_decision()`, `check_decision_rules()`, and `trace_decision_chain()` working for both KWT and SAU |
| D11 | 4:1 Yield Compression Event: jurisdiction-scoped | Kaif | Jul 18 | KWT breach locks KWT at 4:1 in under 100ms with SAU unaffected; SAU breach locks SAU at 4:1 in under 100ms with KWT unaffected |
| D12 | Next.js Sovereign Dashboard: 8 panels, dual view | Kaif | Jul 23 | All panels render live WebSocket data for both countries; breach/restore buttons trigger real graph state changes; two interactive Sigma.js hypergraphs |
| D13 | W3C PROV-O Turtle Export: KWT and SAU | Kaif | Jul 23 | Valid `.ttl` files with all required PROV-O triples for all minting events in both jurisdictions |
| D14 | FastAPI Backend: 8 jurisdiction-aware endpoints | Kaif | Jul 24 | All endpoints return correct responses for both KWT and SAU; OpenAPI schema published at `/docs` |
| D15 | End-to-End Demo Loop: 14 steps (7 KWT + 7 SAU) | Kaif | Jul 25 | All 14 steps run clean from cold start |
| D16 | DEMO_SCRIPT.md and Docker Compose package | Kaif | Aug 1 | Step-by-step script for both country sequences; `docker compose up --build` from a clean environment starts all services green in under 3 minutes |
| D17 | Full Acceptance Gate Regression (G1–G8) | Kaif | Aug 1 | All 8 binary acceptance gates pass in a single automated run for both KWT and SAU, with results logged |

---

## 8. API Reference

All endpoints are jurisdiction-aware. The `jurisdiction` parameter accepts `KWT` or `SAU`.

### REST Endpoints

| Method | Endpoint | Description |
| --- | --- | --- |
| `POST` | `/ingest?jurisdiction=KWT\|SAU` | Accepts a telemetry packet; routes to the correct SHACL gate and knowledge graph |
| `GET` | `/siu-value?jurisdiction=KWT\|SAU` | Returns live `SIU_adjusted` with full C_B, ΣE_D, and Ω breakdown |
| `GET` | `/compliance/{decision_id}` | Returns Rete evaluation result and causal chain; jurisdiction inferred from decision ID |
| `POST` | `/mint?jurisdiction=KWT\|SAU` | Records an S-1 mint decision for the specified sovereign; checks country rules before confirming |
| `GET` | `/audit/{entity_id}?jurisdiction=KWT\|SAU` | Returns full W3C PROV-O provenance lineage for a given entity |
| `GET` | `/graph/state?jurisdiction=KWT\|SAU&date=YYYY-MM-DD` | Returns a bi-temporal knowledge graph snapshot at the given date |
| `POST` | `/simulate/breach?jurisdiction=KWT\|SAU&node={1\|2\|3\|4}` | Injects a synthetic threshold breach into the specified node |
| `POST` | `/simulate/restore?jurisdiction=KWT\|SAU` | Restores all nodes to baseline for the specified country |

### WebSocket Routes

| Route | Stream |
| --- | --- |
| `/ws/telemetry/kwt` | Real-time validated telemetry packets from all four Kuwait nodes |
| `/ws/telemetry/sau` | Real-time validated telemetry packets from all four Saudi Arabia nodes |
| `/ws/events/kwt` | Kuwait compression events, mint decisions, and SHACL rejection alerts |
| `/ws/events/sau` | Saudi Arabia compression events, mint decisions, and SHACL rejection alerts |

### Key Request/Response Shapes

```python
# POST /ingest — telemetry packet
{
  "jurisdiction": "KWT",
  "node_id": "kwt_node2_dammam",
  "reading_type": "piezometric_head",
  "value": 12.3,
  "unit": "m",
  "valid_time": "2026-07-15T09:42:00Z"
}

# GET /siu-value response
{
  "jurisdiction": "KWT",
  "siu_adjusted": 9_824_000_000.0,
  "C_B": { "kwt_node1": 0.31, "kwt_node2": 0.28, "kwt_node3": 0.22, "kwt_node4": 0.19 },
  "sum_E_D": 18_400_000_000.0,
  "omega_threshold": 0.062,
  "computed_at": "2026-07-15T09:42:01Z"
}

# POST /mint response — blocked
{
  "jurisdiction": "KWT",
  "approved": false,
  "failing_rule": "KWT-1",
  "error": "MintBlockedError: Dammam Aquifer drawdown velocity exceeds recharge rate",
  "partial_causal_chain": [...]
}
```

---

## 9. Financial Calibration Baseline

These values are hardcoded in the PoC tokenomics dashboard. Numbers are sourced directly from the SIR V.4.2 Forensic Analysis documents for each jurisdiction.

### Kuwait (CBK)

| Metric | Year 1 | Year 2 | Year 3 |
| --- | --- | --- | --- |
| Total Value Locked | $10.0B | $15.0B | $20.0B |
| SIU-T Circulation Limit (50% of TVL) | $5.0B | $7.5B | $10.0B |
| Annual Gross Integrity Yield (10%) | $1.0B | $1.5B | $2.0B |
| Net Liquid Treasury Payout to CBK (56%) | $560M | $840M | $1,120M |
| Hardware Refresh Escrow (15%) | $150M | $225M | $300M |
| Parametric Insurance Wrap (4%) | $40M | $60M | $80M |
| Local Partner Carve-Out (3%) | $30M | $45M | $60M |
| Tech Fee (22%) | $220M | $330M | $440M |
| **3-year CBK treasury influx** | | | **$2,520,000,000** |
| **3-year hardware escrow accumulated** | | | **$675,000,000** |

**Capital structure:** Phase 0 Fixed Deposit of $100,000 (node mapping activation). GDP-proportional share of the $150M IPCC Multi-Country Pool.

### Saudi Arabia (SAMA)

| Metric | Year 1 | Year 2 | Year 3 |
| --- | --- | --- | --- |
| Total Value Locked | $20.0B | $30.0B | $40.0B |
| SIU-T Circulation Limit (50% of TVL) | $10.0B | $15.0B | $20.0B |
| Annual Gross Integrity Yield (10%) | $2.0B | $3.0B | $4.0B |
| Net Liquid Treasury Payout to SAMA (56%) | $1,120M | $1,680M | $2,240M |
| Hardware Refresh Escrow (15%) | $300M | $450M | $600M |
| Parametric Insurance Wrap (4%) | $80M | $120M | $160M |
| Local Partner Carve-Out (3%) | $60M | $90M | $120M |
| Tech Fee (22%) | $440M | $660M | $880M |
| **3-year SAMA treasury influx** | | | **$5,040,000,000** |
| **3-year hardware escrow accumulated** | | | **$1,350,000,000** |

**Capital structure:** Phase 0 Fixed Deposit of $100,000 (node mapping activation). GDP-proportional share of the $150M IPCC Multi-Country Pool.

### Combined IPCC Consortium Metrics

| Metric | Value |
| --- | --- |
| Total IPCC Pool Capitalisation (35 nations) | $150,000,000 |
| AMM Liquidity Pool (70% of total) | $105,000,000 |
| AMM projected scale by Day 120 | $500,000,000 |
| Combined KWT + SAU Year 1 TVL | $30,000,000,000 |
| Combined KWT + SAU 3-year net treasury payout | $7,560,000,000 |

---

## 10. Acceptance Gates

### Binary Gates — PoC Fails if Any Are Not Met

| Gate | Name | Pass Condition |
| --- | --- | --- |
| G1 | Deterministic compliance | 1,000 Rete evaluations on identical inputs produce identical results with zero variance for both KWT and SAU rulesets independently |
| G2 | Zero LLM in compliance path | grep or trace confirms no LLM API call is made during any SHACL check or Rete evaluation in either jurisdiction |
| G3 | Squeeze fires under 100ms | p99 latency from node breach signal to 4:1 collateral lock is under 100ms for both KWT and SAU |
| G4 | Jurisdiction isolation | A KWT squeeze event does NOT alter the SAU collateral ratio and vice versa; confirmed by `test_jurisdiction_isolation.py` |
| G5 | Causal chain complete | `trace_decision_chain()` traces every squeeze event back to the originating sensor node, timestamp, and breach value for both countries |
| G6 | PROV-O valid | Generated `.ttl` files for both KWT and SAU parse with zero errors in rdflib and contain all required PROV-O triples |
| G7 | Bi-temporal replay | `kwt_graph.state_at("1994-01-01")` and `sau_graph.state_at("1990-01-01")` return distinct, non-empty, structurally correct graphs compared to their 2024 states |
| G8 | SHACL gate | 100% of intentionally corrupted test packets are rejected before touching the knowledge graph for both KWT and SAU profiles |

### Quality Targets (Tracked, Not Blockers)

| Metric | Target |
| --- | --- |
| C_B calculation per 4-node graph | Under 50ms |
| SHACL validation latency per packet | Under 10ms |
| WebSocket telemetry push to dashboard | Under 200ms end-to-end |
| Sigma.js hypergraph initial render (4 nodes) | Under 500ms |
| Next.js page initial cold load | Under 2 seconds (Lighthouse score at least 90) |
| Docker cold-start to all-green | Under 3 minutes |
| End-to-end 14-step demo loop | Under 12 minutes |

---

## 11. Risk Register

| # | Risk | Probability | Impact | Mitigation |
| --- | --- | --- | --- | --- |
| R1 | Dual cleanroom data volume doubles LayoutLMv3 processing time in Week 1 | Medium | Medium | Two parallel Docker containers; pre-process sources to structured CSV; use LayoutLMv3 only for complex-layout PDFs |
| R2 | 12-rule Rete compilation increases startup latency | Low | Low | Rulesets compiled once at service startup; KWT and SAU engines compile in parallel; expected total under 200ms |
| R3 | Semantica SDK surface diverges from co-dev spec | Medium | High | Confirm SDK availability on Day 1; build a thin adapter layer if needed; `jurisdiction` field added as tagged metadata if not natively supported |
| R4 | Synthetic data insufficiently matches Kuwait/Saudi Arabia geophysical reality | Low | Medium | Use CMEMS, Copernicus Level-2, FAO AQUASTAT, KISR, KAUST, and OPEC open data as the floor; synthetic generation only for gap-fill |
| R5 | C_B computation misses the 50ms target with two independent graphs | Low | Low | 4-node graphs are trivially fast; KWT and SAU C_B computed concurrently in two async threads |
| R6 | Jurisdiction isolation failure: KWT squeeze bleeds into SAU state | Medium | High | Rete engines and graph instances are fully separate Python objects with no shared mutable state; Ω_Threshold variables namespaced by country; automated isolation test on Day 14 |
| R7 | WebSocket drops or Sigma.js render stalls with two simultaneous graph streams | Low | Low | Two independent WebSocket connections; broadcast throttled to 10 events/sec per channel; Graphology incremental mutation API used for both graphs |
| R8 | Squeeze hook timing misses the 100ms SLA in Week 3 | Medium | Medium | Rete ruleset pre-compiled at startup; never recompiled per evaluation call; 6-rule sets evaluate in O(1) pattern matching |

---

## 12. Team

| Name | Role | Scope |
| --- | --- | --- |
| **Kaif Ahmad** | Lead Engineer | Full stack for both jurisdictions: ingestion, knowledge graphs, reasoning engines, API, dashboard, and test suite |
| **TFE Lead Architect** | Systems Architect | Hardware telemetry specifications, edge enclave data contracts, and node schema validation rules for Kuwait and Saudi Arabia |
| **Mohd Mohd** | Semantica Founder | SDK guidance, SHACL/Rete configuration, PROV-O export specification, and dual-graph architecture approval |
| **Tizian Rotermund and Egor Sukhanov** | STOKR Integration | TaaS stub API schema for multi-jurisdiction squeeze and mint signals; endpoint contract review on Day 18 |
| **Mustafa** | Demo Stakeholder | Final demo approval and sovereign pilot acceptance for both Kuwait and Saudi Arabia configurations |

### Communication Cadence

| Meeting | Frequency | Duration |
| --- | --- | --- |
| Engineering standup | Daily (Weeks 1 to 5) | 15 minutes, async if needed |
| Architecture gate review | End of each week | 30-minute live call with deliverable demo |
| Final demo rehearsal | July 31 | Full 14-step run-through with all stakeholders |
| Demo day | August 1 | Mustafa and full team |

---

## Appendix A: Repository Structure

```
sir-poc/
├── docker-compose.yml
│
├── backend/
│   ├── ingestion/
│   │   ├── cleanroom.py              # LayoutLMv3 forensic ingest; jurisdiction param
│   │   ├── shacl_gates.py            # SHACL shape validation and packet rejection
│   │   ├── ontology.ttl              # Base TFE node OWL ontology
│   │   ├── kwt_shapes.ttl            # Kuwait-specific SHACL sensor ranges
│   │   └── sau_shapes.ttl            # Saudi Arabia-specific SHACL sensor ranges
│   │
│   ├── graph/
│   │   ├── context_graph.py          # Semantica ContextGraph wrapper; jurisdiction param
│   │   ├── temporal_graph.py         # Bi-temporal KG with Allen Interval Algebra
│   │   └── centrality.py             # Betweenness Centrality engine; one instance per graph
│   │
│   ├── reasoning/
│   │   ├── rete_engine.py            # Deterministic Rete rule compilation; jurisdiction param
│   │   ├── decision_tracker.py       # record_decision + trace_decision_chain; jurisdiction-tagged
│   │   └── rules/
│   │       ├── kwt_rules/
│   │       │   ├── ecological.py     # KWT-1 through KWT-5 ecological rules
│   │       │   └── covenants.py      # KWT Covenant Rule
│   │       └── sau_rules/
│   │           ├── ecological.py     # SAU-1 through SAU-5 ecological rules
│   │           └── covenants.py      # SAU Covenant Rule
│   │
│   ├── provenance/
│   │   ├── manager.py                # ProvenanceManager; jurisdiction param
│   │   └── exporter.py               # RDFExporter to W3C PROV-O Turtle; per jurisdiction
│   │
│   ├── api/
│   │   ├── main.py                   # FastAPI: 8 REST endpoints + 4 WebSocket routes
│   │   └── stokr_stub.py             # STOKR TaaS mock endpoint; jurisdiction-aware
│   │
│   └── data/
│       ├── kuwait/
│       │   ├── node1_kwt_bay/        # Kuwait Bay coastal telemetry
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
│   │   ├── layout.tsx                # Root layout; Tailwind and shadcn theme provider
│   │   ├── page.tsx                  # Main dashboard: all 8 panels with country selector
│   │   ├── graph/
│   │   │   └── [jurisdiction]/
│   │   │       └── page.tsx          # Full-screen hypergraph per country (kwt or sau)
│   │   └── audit/
│   │       └── [id]/page.tsx         # PROV-O lineage explorer for a decision ID
│   │
│   ├── components/
│   │   ├── CountrySelector.tsx       # KWT/SAU toggle and comparison mode
│   │   ├── HypergraphView.tsx        # Sigma.js + Graphology per-country force graph
│   │   ├── ProvenanceGraph.tsx       # Sigma.js PROV-O lineage DAG explorer
│   │   ├── SIUValuationCard.tsx      # Tremor KPI card per country
│   │   ├── CollateralGauge.tsx       # Framer Motion 2:1/4:1 badge per country
│   │   ├── NodeTelemetry.tsx         # Recharts multi-line timeline per node
│   │   ├── CompressionFeed.tsx       # WebSocket live compression event log (both countries)
│   │   ├── MintFeed.tsx              # WebSocket live mint decision feed (both countries)
│   │   └── TriggerPanel.tsx          # 8-node breach buttons and per-country restore controls
│   │
│   ├── lib/
│   │   ├── api.ts                    # Typed FastAPI REST client with jurisdiction param
│   │   └── ws.ts                     # WebSocket manager for kwt and sau channels
│   │
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
│   ├── test_jurisdiction_isolation.py   # Gate G4: KWT squeeze must not affect SAU state
│   ├── test_provenance.py
│   └── test_e2e.py
│
└── DEMO_SCRIPT.md
```

---

## Appendix B: Code Contracts

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

kwt_compliance = kwt_graph.check_decision_rules(
    kwt_decision_id,
    ruleset="sir_v4_2_kwt_compliance",
)
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

sau_compliance = sau_graph.check_decision_rules(
    sau_decision_id,
    ruleset="sir_v4_2_sau_compliance",
)
if not sau_compliance.approved:
    raise MintBlockedError(f"SAU S-1 Minting Blocked: {sau_compliance.failing_rule}")

sau_causal_chain = sau_graph.trace_decision_chain(sau_decision_id)
```

### Jurisdiction Isolation: Squeeze Event

```python
# Kuwait breach fires only the KWT engine
kwt_breach = TelemetryPacket(
    jurisdiction="KWT",
    node_id="kwt_node2_dammam",
    reading_type="piezometric_head",
    value=12.3,
    unit="m",
    valid_time="2026-07-15T09:42:00Z",
)

if kwt_shacl_gate.validate(kwt_breach).accepted:
    kwt_graph.assert_fact(kwt_breach)
    kwt_omega = kwt_graph.recompute_omega()

    if kwt_omega >= KWT_OMEGA_CRIT:
        # Only kwt_rete fires; sau_rete is a completely separate object
        kwt_rete.trigger_yield_compression(jurisdiction="KWT")
        # SAU collateral ratio: still 2:1
        # Verified by test_jurisdiction_isolation.py (Gate G4)
```

### Bi-Temporal Replay

```python
kwt_graph = TemporalKnowledgeGraph(jurisdiction="KWT", enable_allen_algebra=True)
sau_graph = TemporalKnowledgeGraph(jurisdiction="SAU", enable_allen_algebra=True)

# Point-in-time replay for each country
kwt_snapshot_1994 = kwt_graph.state_at("1994-01-01")   # Kuwait EPA water records baseline
sau_snapshot_1990 = sau_graph.state_at("1990-01-01")   # Saudi Aramco SCADA log baseline

kwt_delta = kwt_graph.compute_delta(kwt_snapshot_1994, kwt_graph.state_at("2024-01-01"))
sau_delta = sau_graph.compute_delta(sau_snapshot_1990, sau_graph.state_at("2024-01-01"))
```

### PROV-O Audit Export

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
RDFExporter().export(
    kwt_lineage,
    "kwt_sovereign_audit_trail.ttl",
    format="turtle",
    jurisdiction="KWT",
)

# Saudi Arabia audit trail
sau_prov = ProvenanceManager(jurisdiction="SAU", storage_path="./sau_audit_trail.db")
sau_prov.track_entity(
    "sau_node2_wajid_piezometric",
    source="saudi_geological_survey_wajid_aquifer_2024.pdf",
    metadata={
        "doi": "10.xxxx/sgs.wajid.2024.001",
        "page": 34,
        "author": "Saudi Geological Survey, Hydrogeology Division",
        "confidence": 0.96,
    },
)
sau_lineage = sau_prov.get_lineage("sau_node2_wajid_piezometric")
RDFExporter().export(
    sau_lineage,
    "sau_sovereign_audit_trail.ttl",
    format="turtle",
    jurisdiction="SAU",
)
```

---

*Next action: Kaif to confirm Semantica SDK access and begin Day 1 environment setup on July 1, 2026. Both Kuwait and Saudi Arabia data pipelines initialised simultaneously on Day 1. Week 5 (July 28 – August 1) is reserved as a hardening and contingency buffer ahead of demo day.*
