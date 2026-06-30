# Semantica — Full Responsibility Specification

**Document ID:** SEM-RESP-2026-V2.0
**Date:** June 27, 2026
**Classification:** RESTRICTED — CO-DEVELOPMENT BRIEF
**Project:** SIR V.4.2 Proof of Concept · Kuwait + Saudi Arabia Dual-Sovereign Case Study
**Author:** Semantica Engineering

---

## Overview

Semantica is the **sole veracity and accountability middleware layer** in the SIR V.4.2 stack. It sits between TFE's physical edge hardware and STOKR's settlement ledger, and is the only component that produces the legally defensible, auditor-readable, machine-verifiable signal that authorises every Sovereign Integrity Unit (SIU) minted and every 4:1 collateral lock triggered — independently, for each of the two sovereign configurations: the **State of Kuwait (CBK)** and the **Kingdom of Saudi Arabia (SAMA)**.

**Nothing in the compliance, valuation, or provenance path is delegated outside Semantica.** No LLM. No probabilistic reasoner. No off-chain oracle. Every component below is instantiated **twice** — once per jurisdiction — as fully separate objects with no shared mutable state.

---

## Ownership Boundary

### What Semantica Owns — Full Responsibility

- Every data validation decision from the moment a telemetry packet arrives, for both KWT and SAU streams
- Every knowledge graph write and every graph-state query, across two independent country hypergraphs
- Every compliance rule evaluation, against two jurisdiction-specific rulesets
- Every minting and squeeze decision object, from creation to causal trace, jurisdiction-tagged
- Every provenance record and every W3C PROV-O export, one file per jurisdiction per event
- The full data contract powering all 8 dashboard panels, in dual-country view

### What Semantica Does NOT Own

- **TFE** owns the physical hardware: Sentinel Hub V.4 edge enclaves (biophysical), Socket-7 Consolidated Gateways (SCADA/industrial), SRAM PUF silicon fingerprinting, and ML-KEM-768 post-quantum encryption — deployed across all eight Critical Resource Nodes (KWT-1 through KWT-4, SAU-1 through SAU-4)
- **STOKR** owns the settlement ledger: Liquid Network token issuance, Blockstream AMP, ORO Fund SPV, CSSF licensing, and the TaaS API endpoint
- **Hugging Face** supplies the LayoutLMv3 model weights — Semantica containerises and orchestrates two parallel cleanroom instances (one per country) but does not own the model
- **Legal and regulatory filings** (CBK, SAMA, CSSF, international rating agency submissions) are post-PoC deliverables owned by TFE/STOKR

---

## Full Pipeline

```
TFE EDGE HARDWARE
(Sentinel Hub V.4 + Socket-7, SRAM PUF, ML-KEM-768)
Kuwait: KWT-1 / KWT-2 / KWT-3 / KWT-4
Saudi Arabia: SAU-1 / SAU-2 / SAU-3 / SAU-4
        │
        │  Post-Quantum Encrypted Stream
        ▼
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        SEMANTICA OWNS EVERYTHING BELOW THIS LINE
        (every layer instantiated twice: KWT + SAU)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        │
        ▼
Layer 1 · SHACL Ingestion Gate          (packet → accept / reject, per country profile)
        │
        ▼
Layer 2 · LayoutLMv3 Forensic Clean Room (documents → Genesis Matrix, per country)
        │
        ▼
Layer 3 · Bi-Temporal Knowledge Graph   (facts → timestamped graph, two hypergraphs)
        │
        ▼
Layer 4 · Betweenness Centrality Engine (graph → C_B → SIU_adjusted, per country)
        │
        ▼
Layer 5 · Rete Compliance Engine        (facts → approved / blocked, per ruleset)
        │
        ▼
Layer 6 · S-1 Mint Decision Tracker     (decision → causal object, jurisdiction-tagged)
        │
        ▼
Layer 7 · Yield Compression Event Engine (breach → 4:1 lock < 100ms, jurisdiction-scoped)
        │
        ▼
Layer 8 · Provenance Manager            (entity → DOI chain, per country)
        │
        ▼
Layer 9 · W3C PROV-O Turtle Export      (lineage → .ttl audit file, per jurisdiction)
        │
        ▼
Layer 10 · FastAPI + WebSocket Surface  (data → REST + WS endpoints, jurisdiction-aware)
        │
        ▼
Layer 11 · Dashboard Data Feeds         (endpoints → 8 UI panels, dual sovereign view)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        │
        │  Verified Oracle Handshake
        ▼
STOKR INFRASTRUCTURE
(Liquid Network, Blockstream AMP, ORO Fund SPV)
```

---

## Layer 1 — SHACL Ingestion Gate

**File:** `backend/ingestion/shacl_gates.py` + `backend/ingestion/ontology.ttl` + `backend/ingestion/kwt_shapes.ttl` + `backend/ingestion/sau_shapes.ttl`

### What Semantica Does

Semantica defines the canonical OWL ontology for all TFE entity types and auto-derives two country-specific SHACL shape profiles from it. Every raw telemetry packet arriving from TFE-ib (biophysical) or TFE-gdp (SCADA/industrial) simulators is evaluated against the shape profile matching its `jurisdiction` field before any data is written to the corresponding knowledge graph.

### OWL Ontology Entities Semantica Defines

- `tfe:BiophysicalNode` — a monitored ecological resource node (KWT-1, KWT-2, SAU-1, SAU-2)
- `tfe:IndustrialNode` — a monitored SCADA/logistics node (KWT-3, KWT-4, SAU-3, SAU-4)
- `tfe:TelemetryReading` — a timestamped sensor measurement with unit, source, and jurisdiction
- `tfe:ThresholdEvent` — a reading that meets or exceeds a defined critical threshold
- `tfe:MintDecision` — a sovereign minting or throttling event with full metadata, jurisdiction-tagged
- `tfe:CompressionEvent` — a 4:1 collateral squeeze trigger event, jurisdiction-scoped

### SHACL Gate Behaviour

- A packet that **passes** all shape constraints in its country's profile proceeds to that country's knowledge graph
- A packet that **fails** any constraint is immediately rejected with a plain-English validation report describing exactly which property violated which constraint
- The failed packet is logged to the rejection audit trail but **never written to either graph** and **never forwarded to STOKR**
- `kwt_shapes.ttl` and `sau_shapes.ttl` carry jurisdiction-specific sensor unit ranges, conductivity thresholds, and pressure bounds — they share the base ontology but are evaluated as independent shape graphs

### Acceptance Criteria

- 100% of intentionally corrupted test packets rejected, per country profile — zero false passes
- SHACL validation latency per packet: < 10ms
- Validation report human-readable in under 2 sentences per violation

---

## Layer 2 — LayoutLMv3 Forensic Clean Room

**File:** `backend/ingestion/cleanroom.py`

### What Semantica Does

Semantica containerises and orchestrates two parallel LayoutLMv3 document parsing pipelines (one Docker service per country). Each pipeline ingests 20–40 years of historical government and industrial records — PDFs, CSVs, scanned registers — and produces a country-specific **Genesis Matrix**: a clean, versioned Parquet dataset that serves as the immutable historical baseline for that country's knowledge graph.

### Input Documents Processed (by Node)

**Kuwait:**

- **KWT-1 — Kuwait Bay Intertidal Eco-Buffer:** 40yr daily water-temperature records, channel bathymetric surveys, historical bay water chemistry (Kuwait EPA, KISR, CMEMS)
- **KWT-2 — Dammam Aquifer Matrix:** 30yr daily pump registries, deep well pressure charts, geochemical metrics (Kuwait MEWA, FAO AQUASTAT)
- **KWT-3 — Mina Al-Ahmadi Refinery Complex:** 20yr SCADA log streams, transport customs weight records, refinery output declarations (KNPC, KPC, OPEC Statistics)
- **KWT-4 — Al-Zour Desalination Complex:** Plant flow meter histories, municipal output logs, inter-utility balance sheets (KAPP, IDA, Kuwait MEWA)

**Saudi Arabia:**

- **SAU-1 — Red Sea Coastal Eco-Shield:** 40yr bathymetric surveys, maritime salinity records, historical temperature logs (KAUST Red Sea Research Center, Saudi MEWA, CMEMS)
- **SAU-2 — Wajid/Minjur Aquifer Plenum:** 30yr daily pump registries, deep borehole logs, regional hydrogeologic archives (Saudi MEWA, Saudi Geological Survey)
- **SAU-3 — Jubail Industrial Complex:** 20yr SCADA log streams, customs weight records, refinery output declarations (Saudi Aramco, SABIC, Royal Commission for Jubail and Yanbu)
- **SAU-4 — Port of King Abdullah (Rabigh):** Shipping bills of lading, automated freight weight logs, customs tracking manifests (Mawani, UNCTAD, IMO GISIS)

### Clean Room Rules

- Any entry with a tampered or missing timestamp is flagged and excluded from the Genesis Matrix output
- Any entry where the recorded value falls outside the physically plausible range for that sensor type is quarantined and logged
- Any entry from a source that cannot be traced to an official government authority or DOI-registered dataset is excluded
- The two cleanrooms run as fully isolated containers — a malformed Kuwait document can never quarantine or corrupt the Saudi Arabia Genesis Matrix, and vice versa

### Output

Each Genesis Matrix is a versioned Parquet file with the schema:

```
jurisdiction | node_id | reading_type | valid_time | recorded_at | value | unit | source_doi | confidence
```

### Acceptance Criteria

- Both LayoutLMv3 cleanrooms produce a valid Parquet per country with no tampered entries passing through
- Every row in both Genesis Matrices has a `source_doi` or `source_authority` field populated

---

## Layer 3 — Bi-Temporal Knowledge Graph

**File:** `backend/graph/temporal_graph.py` + `backend/graph/context_graph.py`

### What Semantica Does

Semantica maintains two live 4-node sovereign hypergraphs — `ContextGraph(jurisdiction="KWT")` and `ContextGraph(jurisdiction="SAU")` — using `TemporalKnowledgeGraph` and `ContextGraph`. Every asserted fact, in either graph, is stored with **two independent timestamps** — these are never conflated and never overwritten, and never shared across jurisdictions.

### Dual-Timestamp Schema

- `valid_time` — when the fact was true in the real world (e.g. the date a reservoir level or piezometric head was measured)
- `recorded_at` — when Semantica ingested the fact (the ingestion timestamp)

This separation is the legal foundation of the entire system. A fact can be ingested today but have a `valid_time` decades in the past. An auditor can prove both dates independently, for either country.

### Key API Methods Semantica Must Expose

```python
kwt_graph.state_at("1994-01-01")
sau_graph.state_at("1990-01-01")
# Each returns the complete 4-node hypergraph for that country as it existed on that date.
# Uses valid_time to filter — not recorded_at.

kwt_graph.compute_delta(snapshot_a, snapshot_b)
sau_graph.compute_delta(snapshot_a, snapshot_b)
# Returns structural and value differences between two temporal snapshots, per graph.

graph.assert_fact(entity, property, value, valid_time, recorded_at, confidence)
# Writes a bi-temporal fact to the calling graph. Cannot overwrite an existing valid_time record.
```

### Allen Interval Algebra Anomaly Detection

Semantica applies the 13 Allen temporal relations to detect timing anomalies in historical SCADA logs and biophysical readings, independently in each country graph:

- `meets` / `met-by`
- `overlaps` / `overlapped-by`
- `during` / `contains`
- `starts` / `started-by`
- `finishes` / `finished-by`
- `equals`
- `before` / `after`

A detected anomaly (e.g. a downstream effect `before` its upstream cause) is flagged in the relevant graph as a `tfe:TemporalAnomaly` entity and surfaced in the dashboard with a KWT or SAU badge. No LLM is used to interpret the anomaly — the Allen algebra relation is deterministic.

### Acceptance Criteria

- `kwt_graph.state_at("1994-01-01")` and `sau_graph.state_at("1990-01-01")` each return a valid, non-empty graph distinct from that country's `state_at("2024-01-01")`
- `compute_delta()` returns a non-empty set of structural and value changes, for both graphs independently
- Allen Interval Algebra anomaly detection identifies at least one temporal inconsistency in each country's seeded SCADA test data

---

## Layer 4 — Betweenness Centrality Engine

**File:** `backend/graph/centrality.py`

### What Semantica Does

Semantica computes **Betweenness Centrality (C_B)** for each of the four nodes in each country hypergraph — 8 nodes total — using two independent `CentralityCalculator` instances. C_B quantifies how many shortest paths between all other node pairs pass through each given node — a direct measure of systemic criticality, computed separately per sovereign.

### C_B Interpretation

**Kuwait:**

- **KWT-1 (Kuwait Bay Intertidal Eco-Buffer)** — high ecological C_B; hypersalinity cascades to KWT-4 and degrades desalination intake quality
- **KWT-2 (Dammam Aquifer Matrix)** — moderate-high C_B; water-table drawdown propagates to refinery cooling loops at KWT-3
- **KWT-3 (Mina Al-Ahmadi Refinery Complex)** — high economic C_B; crude export clearance and SCADA custody transfer route through this node
- **KWT-4 (Al-Zour Desalination Complex)** — highest national utility C_B; municipal freshwater supply for all of Kuwait City

**Saudi Arabia:**

- **SAU-1 (Red Sea Coastal Eco-Shield)** — high ecological C_B; coral-mangrove buffer stabilises wave attenuation and draft depth at SAU-4
- **SAU-2 (Wajid/Minjur Aquifer Plenum)** — high resource C_B; primary industrial water tower for Eastern Province cooling loops at SAU-3
- **SAU-3 (Jubail Industrial Complex)** — highest economic C_B; world's largest single petrochemical export cluster
- **SAU-4 (Port of King Abdullah, Rabigh)** — high logistics C_B; primary Red Sea deep-water gateway for industrial export

### ΣE_D — Downstream Asset Exposure

For each of the 8 nodes, Semantica maintains a hardcoded set of `E_D` coefficients sourced from the relevant Genesis Matrix:

- **KWT-1 / SAU-1 E_D:** wave attenuation value (USD/event), intertidal/coastal buffer integrity index
- **KWT-2 / SAU-2 E_D:** aquifer recharge contribution rate (m³/yr), industrial cooling-loop dependency value
- **KWT-3 / SAU-3 E_D:** refinery/petrochemical export revenue (USD/yr), custody-transfer throughput volume
- **KWT-4 / SAU-4 E_D:** desalination output or port TEU throughput velocity, utility/logistics uptime coefficient

### SIU Valuation Formula — Live Computation

```
KWT_SIU_adjusted = f(kwt_C_B × kwt_sum_E_D) × (1 − kwt_omega)
SAU_SIU_adjusted = f(sau_C_B × sau_sum_E_D) × (1 − sau_omega)
```

Semantica owns all three variables, independently for each country:

- `C_B` — computed from that country's live graph state (sub-50ms)
- `ΣE_D` — summed across that country's 4 nodes using its Genesis Matrix coefficients
- `Ω_Threshold` — derived from that country's most recent SHACL-validated sensor readings; updated on every successful packet ingestion for that jurisdiction

The formula output is the floor price value that STOKR uses to determine each country's SIU reserve valuation. It is recomputed on every graph state change, per country — no caching of stale values, no cross-jurisdiction interpolation.

### Acceptance Criteria

- C_B computed for all 4 nodes in < 50ms on each graph state change, for both KWT and SAU graphs independently
- `KWT_SIU_adjusted` and `SAU_SIU_adjusted` each recompute automatically on every new validated telemetry packet for their jurisdiction
- C_B values are deterministic — same graph state always yields the same C_B, in either country

---

## Layer 5 — Rete Compliance Engine

**Files:** `backend/reasoning/rete_engine.py` + `backend/reasoning/rules/kwt_rules/` + `backend/reasoning/rules/sau_rules/`

### What Semantica Does

Semantica owns two deterministic compliance engines — `ReteEngine(jurisdiction="KWT")` and `ReteEngine(jurisdiction="SAU")`. All regulatory and ecological rules are pre-compiled into each Rete network at service startup — evaluated as pattern-matching over working memory, not as LLM prompts, not as vector similarity searches.

**The Rete network is the only component permitted to make a binary compliance decision. No other component in the system has this authority, in either jurisdiction.**

### The Rules Semantica Owns

**Kuwait ruleset (6 rules):**

| Rule | Trigger Condition | Action |
| --- | --- | --- |
| KWT-1 | Dammam Aquifer piezometric drawdown velocity exceeds recharge rate | Reject Node KWT-2; flag `tfe:AquiferBreachEvent`; block KWT minting |
| KWT-2 | Kuwait Bay electrical conductivity spike breaches hypersalinity threshold | Reject Node KWT-1; flag `tfe:HypersalinityEvent`; block KWT minting |
| KWT-3 | Mina Al-Ahmadi SCADA harmonics outside ±2σ of genesis baseline | Reject SCADA stream; flag `tfe:HarmonicAnomalyEvent`; suspend Node KWT-3 from C_B pending review |
| KWT-4 | Al-Zour pump thermodynamic signature variance exceeds bounds | Flag `tfe:PumpAnomalyEvent`; blocks minting only after 3 consecutive anomalies |
| KWT-5 | Kuwait Bay benthic sediment transport velocity above siltation threshold | Flag `tfe:SiltationEvent`; block desalination clearance at Node KWT-4 |
| KWT-C (Covenant) | SIU-T circulating supply exceeds 50% of SIU parent reserve | Reject mint call immediately; raise structured error; signal never reaches STOKR |

**Saudi Arabia ruleset (6 rules):**

| Rule | Trigger Condition | Action |
| --- | --- | --- |
| SAU-1 | Wajid/Minjur aquifer drawdown velocity exceeds recharge rate | Reject Node SAU-2; flag `tfe:AquiferBreachEvent`; block SAU minting |
| SAU-2 | Red Sea coastal thermal gradient or brine shift breaches threshold | Reject Node SAU-1; flag `tfe:BrineShiftEvent`; block SAU minting |
| SAU-3 | Jubail SCADA harmonics outside ±2σ of genesis baseline | Reject SCADA stream; flag `tfe:HarmonicAnomalyEvent`; suspend Node SAU-3 from C_B pending review |
| SAU-4 | King Abdullah Port PLC crane load vs. bill of lading divergence exceeds 3% | Flag `tfe:ManifestDiscrepancyEvent`; blocks minting only after 3 consecutive divergences |
| SAU-5 | Red Sea kinetic wave attenuation collapse below threshold | Flag `tfe:WaveAttenuationEvent`; block port clearance at Node SAU-4 |
| SAU-C (Covenant) | SIU-T circulating supply exceeds 50% of SIU parent reserve | Reject mint call immediately; raise structured error; signal never reaches STOKR |

### ReteEngine API Contract

```python
result = ReteEngine(jurisdiction="KWT").evaluate(telemetry_packet)
# Returns:
# {
#   "approved": bool,
#   "failing_rule": str | None,   # e.g. "KWT-1 — Aquifer Drawdown"
#   "flagged_events": list[str],  # zero or more tfe:EventType strings
#   "jurisdiction": "KWT",
#   "evaluation_id": str,         # UUID bound to this evaluation
# }
```

### Key Invariants

- Each ruleset is compiled **once** at service startup — never recompiled per evaluation call; KWT and SAU engines compile in parallel
- 1,000 evaluations on identical inputs must produce identical outputs (zero variance), for either ruleset independently
- No LLM API call may appear anywhere in either compliance evaluation path
- A failing evaluation must name the exact rule and jurisdiction that failed — generic "compliance failed" errors are not acceptable

### Acceptance Criteria

- All 6 KWT rules and all 6 SAU rules fire deterministically on every run
- 5 compliant test packets per country → all pass; 5 non-compliant packets per country → all fail naming the correct rule and jurisdiction
- Zero LLM calls confirmed by grep on both evaluation code paths

---

## Layer 6 — S-1 Mint Decision Tracker

**File:** `backend/reasoning/decision_tracker.py`

### What Semantica Does

Every minting decision and every throttle decision, in either jurisdiction, is a first-class object in the relevant Semantica graph — not a log line, not a database row. Semantica creates an immutable, jurisdiction-tagged causal object that binds the decision to its exact inputs, the Rete evaluation result, and the full backward-trace to originating sensor readings.

### Three API Methods Semantica Must Expose

**`graph.record_decision()`** — writes the decision object to the knowledge graph

```python
kwt_decision_id = kwt_graph.record_decision(
    category="s1_sovereign_mint",          # or "yield_compression", "mint_blocked"
    outcome="mint_siu_t",                  # or "squeeze_4_1", "blocked"
    jurisdiction="KWT",
    confidence=0.97,
    rationale="Kuwait Bay baseline stable. Dammam Aquifer within recharge bounds. All 4 KWT nodes green.",
    entities=["kwt_node1_bay", "kwt_node2_dammam", "kwt_node3_mina_ahmadi", "kwt_node4_alzour"],
)
```

**`graph.check_decision_rules()`** — runs the Rete evaluation and binds the result to the decision object

```python
kwt_compliance = kwt_graph.check_decision_rules(
    kwt_decision_id,
    ruleset="sir_v4_2_kwt_compliance",
)
# kwt_compliance.approved: bool
# kwt_compliance.failing_rule: str | None
# kwt_compliance.evaluation_id: str
```

**`graph.trace_decision_chain()`** — walks the causal graph backward to the originating sensor

```python
kwt_causal_chain = kwt_graph.trace_decision_chain(kwt_decision_id)
# Returns an ordered list of graph nodes from the decision object
# back through derived metrics, intermediate computations,
# and ultimately to the raw sensor reading with its:
#   - jurisdiction
#   - node_id
#   - sensor_type
#   - valid_time (exact timestamp of the original reading)
#   - recorded_at (ingestion timestamp)
#   - raw_value and unit
#   - source_doi or source_authority
```

The identical contract applies to `sau_graph`, with `jurisdiction="SAU"` and the `sir_v4_2_sau_compliance` ruleset.

### Blocked Mint Contract

If `check_decision_rules()` returns `approved=False`:

- The mint call raises a structured `MintBlockedError` immediately, naming the jurisdiction
- The error payload contains: `jurisdiction`, `decision_id`, `failing_rule`, and the partial `causal_chain` up to the point of failure
- No signal reaches the STOKR TaaS endpoint
- The blocked decision object remains in the relevant graph with `outcome="blocked"` — it is never silently discarded

### Acceptance Criteria

- `record_decision()`, `check_decision_rules()`, and `trace_decision_chain()` all functional and tested for both KWT and SAU
- `trace_decision_chain()` returns a chain reaching at least 3 hops back to a raw sensor value, in either jurisdiction
- Blocked decisions are visible in the Mint Feed dashboard panel with the correct jurisdiction badge and failing rule displayed

---

## Layer 7 — 4:1 Yield Compression Event Engine

**Files:** `backend/reasoning/rete_engine.py` + `backend/reasoning/decision_tracker.py`

### What Semantica Does

When `Ω_Threshold ≥ Ω_Crit` in either country graph, that country's Rete network fires the Yield Compression Event in under 100ms. No human confirmation. No LLM interpretation. No probabilistic delay. The event is strictly jurisdiction-scoped: a Kuwait breach never alters Saudi Arabia's collateral state, and vice versa.

### The Collateral Squeeze Rule

```
γ = { 2:1  if Ω_Threshold < Ω_Crit      ← normal baseline conditions
    { 4:1  if Ω_Threshold ≥ Ω_Crit      ← Yield Compression Event
```

Evaluated independently per country.

### The 6-Step Compression Sequence Semantica Owns (per jurisdiction)

1. **Breach detection** — an incoming SHACL-validated, country-tagged telemetry packet updates `Ω_Threshold` in that country's knowledge graph; that country's Rete network immediately evaluates the compression rule against the new value
2. **Rete fires** — the compression condition (`Ω_Threshold ≥ Ω_Crit`) matches in working memory; the Rete network triggers the Yield Compression Event with zero delay, scoped to that jurisdiction only
3. **Decision object created** — `record_decision(category="yield_compression", outcome="squeeze_4_1", jurisdiction="KWT"|"SAU")` writes an immutable causal object to the relevant graph, bound to the exact breach packet
4. **Causal chain attached** — `trace_decision_chain()` is invoked automatically and attached to the decision object before the STOKR signal is sent
5. **STOKR signal dispatched** — the decision object (including causal chain) is posted to the STOKR TaaS stub endpoint `/collateral-squeeze` with a jurisdiction header
6. **Collateral ratio updated** — the circulating SIU-T supply for that sovereign only is now constrained to 25% of its SIU parent reserve (4:1 lock), down from 50% (2:1 baseline); the other country's ratio is untouched

### SLA

- p99 latency from breach packet ingestion to 4:1 lock signal dispatched: **< 100ms**, for both KWT and SAU independently
- This SLA applies to the Semantica processing path only — network latency to STOKR is excluded

### Jurisdiction Isolation Guarantee

KWT and SAU Rete engines and graph instances are fully separate Python objects with no shared mutable state. `Ω_Threshold` variables are namespaced by country. A Kuwait breach can never trigger, throttle, or otherwise influence the Saudi Arabia compression engine, and is covered by `test_jurisdiction_isolation.py`.

### Acceptance Criteria

- Inject a simulated KWT-2 aquifer breach → KWT 4:1 lock signal received at STOKR stub in < 100ms → SAU collateral ratio remains 2:1
- Inject a simulated SAU-1 brine-shift breach → SAU 4:1 lock signal received at STOKR stub in < 100ms → KWT collateral ratio remains 2:1
- The causal chain on each compression decision object traces back to the exact breach sensor reading in the correct country graph
- Collateral ratio panel in the dashboard transitions from 2:1 to 4:1 with the Framer Motion animation firing on WebSocket push, badged to the correct jurisdiction

---

## Layer 8 — Provenance Manager

**File:** `backend/provenance/manager.py`

### What Semantica Does

Every asserted fact in either knowledge graph — every sensor reading, every derived metric, every Genesis Matrix row loaded into the graph — must have a provenance record binding it to its originating source. Semantica instantiates two independent provenance managers, `ProvenanceManager(jurisdiction="KWT")` and `ProvenanceManager(jurisdiction="SAU")`, each owning this binding from the moment of ingestion for its country.

### Provenance Record Schema

Every entity in either graph must have a provenance record containing:

- `jurisdiction` — `KWT` or `SAU`
- `source_document` — filename or URL of the originating document
- `source_doi` — the DOI of the originating academic or government publication (where available)
- `source_authority` — the government body or institution that produced the source
- `author` — the named author or publishing body
- `page` — the specific page or table within the document (for PDFs)
- `ingestion_timestamp` — when Semantica ingested this fact (`recorded_at`)
- `confidence` — a float between 0.0 and 1.0 representing parsing confidence
- `puf_fingerprint_flag` — boolean; true if the source was hardware-attested at the edge (post-PoC)
- `ml_kem_flag` — boolean; true if the source was encrypted with ML-KEM-768 in transit (post-PoC)

### Key API Methods

```python
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
# Returns the full ancestor chain:
# kwt_node2_dammam_piezometric
#   ← derived_from: dammam_aquifer_model_2024
#       ← derived_from: kuwait_mewa_pump_registry_1996_2024.csv
#           ← source: doi:10.xxxx/kwt.mewa.gw.2024.001 (page 18)

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
```

### Minimum Standard

- Every entity in either graph must have a provenance chain traceable to a DOI or named government authority
- The chain must be at least 3 hops deep for any SIU-influencing metric, in either country
- No SIU valuation component may be derived from a source with confidence < 0.80

### Acceptance Criteria

- `get_lineage()` returns a ≥ 3-hop chain for each of the 8 node entities (4 KWT + 4 SAU)
- Every row in both Genesis Matrices has a corresponding provenance record before graph loading begins

---

## Layer 9 — W3C PROV-O Turtle Export

**File:** `backend/provenance/exporter.py`

### What Semantica Does

Semantica converts each country's provenance graph into a compliance-grade W3C PROV-O Turtle (`.ttl`) file — one file per jurisdiction per event. These files are the primary artifacts delivered to international auditors, rating agencies, and the central banks (CBK and SAMA). Each must be machine-parseable, standards-compliant, and self-contained.

### Required PROV-O Triples in Every Export

Every exported Turtle file must contain:

- `prov:Entity` — one entry per tracked data entity in the decision's lineage, scoped to that jurisdiction
- `prov:wasDerivedFrom` — the full lineage chain linking derived entities to source entities
- `prov:wasAttributedTo` — the government body, institution, or sensor that produced the claim
- `prov:generatedAtTime` — the `recorded_at` ingestion timestamp (ISO 8601)
- `prov:wasAssociatedWith` — the parsing agent (LayoutLMv3 cleanroom) or sensor simulator that generated the claim
- `prov:used` — links each activity to the entities it consumed

### Export API

```python
RDFExporter().export(
    kwt_lineage,
    "kwt_sovereign_audit_trail_{decision_id}.ttl",
    format="turtle",
    jurisdiction="KWT",
)

RDFExporter().export(
    sau_lineage,
    "sau_sovereign_audit_trail_{decision_id}.ttl",
    format="turtle",
    jurisdiction="SAU",
)
```

### Validation Gate

Before any `.ttl` file is considered a valid PoC artifact:

1. `rdflib.Graph().parse(file, format="turtle")` must complete with zero errors
2. A SPARQL query for each required triple class must return at least one result
3. The file must be self-contained — no external URI dependencies that could resolve to 404

### Acceptance Criteria

- One-click export from the dashboard generates a valid `.ttl` file in < 2 seconds, for either jurisdiction
- Both files parse with zero errors in rdflib
- PROV-O triple validation passes for all 5 required triple types, in both exports
- Exports are generated for: all 8 node lineages (4 KWT + 4 SAU) + the most recent mint decision and compression event for each country

---

## Layer 10 — FastAPI + WebSocket Surface

**File:** `backend/api/main.py`

### What Semantica Does

Semantica exposes its internal graph, reasoning, and provenance state — for both KWT and SAU — through a single FastAPI application. This is the only interface the Next.js dashboard and the STOKR TaaS stub consume. All endpoints are jurisdiction-aware and read-consistent with the live graph state for the requested country.

### REST Endpoints (8)

**`POST /ingest?jurisdiction=KWT|SAU`**

- Accepts a raw telemetry packet (JSON); routes to the correct country's SHACL gate
- Returns `{accepted: bool, validation_report: str | None}`
- On acceptance: writes to that country's graph, triggers C_B recalculation, pushes updated `SIU_adjusted` to the matching WebSocket telemetry channel

**`GET /siu-value?jurisdiction=KWT|SAU`**

- Returns the current `SIU_adjusted` for the requested country with full breakdown: `C_B` per node, `ΣE_D` total, `Ω_Threshold` current value, and the raw formula evaluation

**`GET /compliance/{decision_id}`**

- Returns the Rete evaluation result and the full causal chain for a given decision ID; jurisdiction inferred from the decision ID

**`POST /mint?jurisdiction=KWT|SAU`**

- Records a mint decision for the specified sovereign, runs `check_decision_rules()`, returns `{jurisdiction, approved: bool, decision_id: str}` or `{jurisdiction, approved: false, failing_rule: str, decision_id: str}`

**`GET /audit/{entity_id}?jurisdiction=KWT|SAU`**

- Returns the full provenance lineage for a given graph entity; includes all PROV-O metadata fields

**`GET /graph/state?jurisdiction=KWT|SAU&date=YYYY-MM-DD`**

- Returns the requested country's bi-temporal graph snapshot as of the given date using `graph.state_at()`

**`POST /simulate/breach?jurisdiction=KWT|SAU&node={1|2|3|4}`**

- Injects a synthetic threshold breach for the specified node in the specified country; triggers the full 6-step compression sequence for that jurisdiction only

**`POST /simulate/restore?jurisdiction=KWT|SAU`**

- Restores all nodes in the specified country to baseline

### WebSocket Routes (4)

**`/ws/telemetry/kwt`** and **`/ws/telemetry/sau`**

- Each streams live `SIU_adjusted` updates, node health status, `Ω_Threshold` readings, and C_B values for that country on every graph state change
- Throttled to 10 events/sec maximum per channel to prevent Sigma.js render stalls

**`/ws/events/kwt`** and **`/ws/events/sau`**

- Each streams that country's compression events, mint decisions, and SHACL rejection alerts in real time as they are recorded in the graph
- Payload per event: `{jurisdiction, event_type, decision_id, outcome, failing_rule | null, timestamp}`

### STOKR TaaS Stub (`backend/api/stokr_stub.py`)

- Receives `POST /collateral-squeeze` from either compression engine, jurisdiction-tagged
- Logs: jurisdiction, decision_id, causal_chain summary, old ratio, new ratio, timestamp
- Receives `POST /mint-signal` from approved mint decisions in either jurisdiction
- Returns `200 OK` with a stub confirmation token in both cases

### Acceptance Criteria

- All 8 REST endpoints return structurally correct, jurisdiction-aware responses confirmed by automated tests covering both KWT and SAU
- All 4 WebSocket routes deliver an update within 200ms of a graph state change
- OpenAPI schema auto-generated and accessible at `/docs`
- STOKR stub correctly logs all compression and mint signals with jurisdiction and timestamps

---

## Layer 11 — Dashboard Data Feeds

**Directory:** `dashboard/`

Semantica's API feeds all 8 panels in the Next.js Sovereign Intelligence Dashboard, plus a global country selector. The panel-to-API mapping is:

### Global Header — Country Selector

- **Source:** Static UI state, persisted client-side; drives the `jurisdiction` query parameter on every panel's API calls
- **Behaviour:** Toggle between KWT-only, SAU-only, or side-by-side dual view; per-country WebSocket health indicator

### Panel 1 — Sovereign Hypergraph (Sigma.js + Graphology)

- **Source:** `GET /siu-value?jurisdiction=` (initial load) + `WS /ws/telemetry/kwt` and `/sau` (live updates)
- **Semantica data consumed:** C_B per node, health status per node, edge interdependency weights, Ω_Threshold per biophysical node — for the selected country or both
- **Behaviour:** Node color and size update on each WebSocket push; breach nodes pulse red via Framer Motion; two independent Graphology graph objects are mutated incrementally (never rebuilt), rendered side-by-side or toggled

### Panel 2 — SIU Valuation Card (Tremor + Recharts)

- **Source:** `WS /ws/telemetry/{kwt,sau}`
- **Semantica data consumed:** `KWT_SIU_adjusted` / `SAU_SIU_adjusted`, `C_B` breakdown per node, `ΣE_D` total, `Ω_Threshold` — one card per country
- **Behaviour:** Animated counter updates on each WebSocket push; Recharts donut reflects current C_B split; Ω radial gauge sweeps toward critical zone as Ω_Threshold rises, independently per country

### Panel 3 — Collateral Ratio Gauge (Framer Motion)

- **Source:** `WS /ws/events/{kwt,sau}`
- **Semantica data consumed:** Current collateral ratio (2:1 or 4:1) per country, SIU-T circulating supply, SIU parent reserve floor, seconds since last compression event
- **Behaviour:** Framer Motion spring animation transitions the relevant country's badge from green `2:1` to red `4:1` on compression event; the other country's badge is unaffected; Tremor progress bar shows SIU-T vs reserve floor per country

### Panel 4 — PROV-O Lineage Explorer (Sigma.js)

- **Source:** `GET /audit/{entity_id}?jurisdiction=` triggered on user selection
- **Semantica data consumed:** Full provenance lineage object including all entity IRIs, DOIs, authors, confidence scores, and `prov:` relationship types, scoped to the selected jurisdiction
- **Behaviour:** Sigma.js instance renders the DAG; click any node for tooltip with full metadata; export button calls `GET /audit/{entity_id}` and triggers the jurisdiction-prefixed `.ttl` download

### Panel 5 — Node Telemetry Timeline (Recharts)

- **Source:** `GET /graph/state?jurisdiction=&date=` for historical range + `WS /ws/telemetry/{kwt,sau}` for live append
- **Semantica data consumed:** Per-node key sensor metric time series, genesis baseline values, historical threshold breach timestamps, for the selected country's nodes
- **Behaviour:** Recharts multi-line chart with baseline overlay and vertical breach markers; date range selector re-calls `GET /graph/state` with the appropriate jurisdiction and date

### Panel 6 — Compression Event Feed

- **Source:** `WS /ws/events/kwt` and `/ws/events/sau` filtered for `event_type == "yield_compression"`
- **Semantica data consumed:** `jurisdiction`, `decision_id`, `outcome`, `timestamp`, expandable `causal_chain` from `GET /compliance/{decision_id}`
- **Behaviour:** Real-time push rows tagged with a KWT or SAU badge; click row to expand `trace_decision_chain()` output showing sensor → derived metric → Ω_Threshold → compression decision

### Panel 7 — Mint Decision Feed

- **Source:** `WS /ws/events/kwt` and `/ws/events/sau` filtered for `event_type == "s1_sovereign_mint"` or `"mint_blocked"`
- **Semantica data consumed:** `jurisdiction`, `decision_id`, `outcome`, `failing_rule | null`, `confidence`, `rationale`, node entity list
- **Behaviour:** Green `APPROVED` or red `BLOCKED — {failing_rule}` badge per row, tagged KWT or SAU; click decision ID opens Panel 4 (PROV-O Lineage Explorer) for that decision

### Panel 8 — Trigger Control Panel

- **Source:** Outbound to `POST /simulate/breach?jurisdiction=` and `POST /simulate/restore?jurisdiction=`
- **Semantica data consumed:** WebSocket connection status from `WS /ws/telemetry/kwt` and `/sau`
- **Behaviour:** Eight node breach buttons (4 KWT + 4 SAU) + one restore-baseline button per country; green/red WebSocket indicator per jurisdiction in the header; buttons disabled during that country's active squeeze (prevents double-trigger); the other country's buttons remain active

---

## Key Invariants — Things That Must Never Happen

These are hard boundaries. Violating any of these invalidates the PoC as a legally defensible artifact:

- **No LLM call in any compliance evaluation path** — grep on startup confirms zero OpenAI / Anthropic / Cohere API calls reachable from either `rete_engine.py` instance or `shacl_gates.py`
- **No unvalidated packet reaches either knowledge graph** — the country's SHACL gate is the only entry point; there is no bypass route
- **No mint signal reaches STOKR before `check_decision_rules()` returns `approved=True`** — the endpoint call is gated behind the Rete evaluation result, per jurisdiction
- **No decision object is silently discarded** — blocked decisions are written to the relevant graph with `outcome="blocked"` and remain permanently queryable
- **No `SIU_adjusted` value is cached beyond one graph state change** — each country's formula is recomputed on every validated telemetry ingestion for that jurisdiction
- **No `.ttl` file is considered valid before parsing with zero rdflib errors** — the export function must validate before returning success
- **No cross-sovereign bleed** — a KWT squeeze, breach, or rule failure must never alter SAU graph state, collateral ratio, or vice versa; `test_jurisdiction_isolation.py` enforces this as a binary gate

---

## Binary Acceptance Gates Summary

These 8 gates must all pass for the PoC to be considered complete:

| Gate | Test | Pass Condition |
| --- | --- | --- |
| G1 | Rete determinism | 1,000 evaluations on identical input → identical output, zero variance, for both KWT and SAU rulesets independently |
| G2 | Zero LLM in compliance path | grep / trace confirms no LLM API call reachable from either jurisdiction's compliance code |
| G3 | Squeeze < 100ms | p99 breach-to-4:1-lock latency < 100ms in benchmark, for both KWT and SAU |
| G4 | Jurisdiction isolation | A KWT squeeze event does NOT alter SAU collateral state and vice versa; confirmed by `test_jurisdiction_isolation.py` |
| G5 | Causal chain complete | `trace_decision_chain()` reaches the originating sensor with node ID, timestamp, and breach value, for both countries |
| G6 | PROV-O valid | Generated `.ttl` files for both KWT and SAU parse with zero rdflib errors; all 5 triple types present |
| G7 | Bi-temporal replay | `kwt_graph.state_at("1994-01-01")` and `sau_graph.state_at("1990-01-01")` each differ from their 2024 states; both non-empty and structurally correct |
| G8 | SHACL gate | 100% of corrupted test packets rejected before knowledge graph contact, for both KWT and SAU profiles |

---

*All responsibilities in this document are owned by Semantica Engineering and are deliverable within the 5-week PoC window (July 1 – August 1, 2026), inclusive of a Week 5 hardening and contingency buffer ahead of demo day. The dual-sovereign scope spans both the State of Kuwait (CBK) and the Kingdom of Saudi Arabia (SAMA), with every layer above instantiated independently per jurisdiction.*
