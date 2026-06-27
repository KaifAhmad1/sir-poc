# Semantica — Full Responsibility Specification

**Document ID:** SEM-RESP-2026-V1.0
**Date:** June 27, 2026
**Classification:** RESTRICTED — CO-DEVELOPMENT BRIEF
**Project:** SIR V.4.2 Proof of Concept · Sri Lanka Case Study
**Author:** Semantica Engineering

---

## Overview

Semantica is the **sole veracity and accountability middleware layer** in the SIR V.4.2 stack. It sits between TFE's physical edge hardware and STOKR's settlement ledger, and is the only component that produces the legally defensible, auditor-readable, machine-verifiable signal that authorises every Sovereign Integrity Unit (SIU) minted and every 4:1 collateral lock triggered.

**Nothing in the compliance, valuation, or provenance path is delegated outside Semantica.** No LLM. No probabilistic reasoner. No off-chain oracle.

---

## Ownership Boundary

### What Semantica Owns — Full Responsibility

- Every data validation decision from the moment a telemetry packet arrives
- Every knowledge graph write and every graph-state query
- Every compliance rule evaluation
- Every minting and squeeze decision object, from creation to causal trace
- Every provenance record and every W3C PROV-O export
- The full data contract powering all 8 dashboard panels

### What Semantica Does NOT Own

- **TFE** owns the physical hardware: Sentinel Hub V.4 edge enclaves (biophysical), Socket-7 Consolidated Gateways (SCADA/industrial), SRAM PUF silicon fingerprinting, and ML-KEM-768 post-quantum encryption
- **STOKR** owns the settlement ledger: Liquid Network token issuance, Blockstream AMP, ORO Fund SPV, CSSF licensing, and the TaaS API endpoint
- **Hugging Face** supplies the LayoutLMv3 model weights — Semantica containerises and orchestrates it but does not own the model
- **Legal and regulatory filings** (CSSF, CBSL, international rating agency submissions) are post-PoC deliverables owned by TFE/STOKR

---

## Full Pipeline

```
TFE EDGE HARDWARE
(Sentinel Hub V.4 + Socket-7, SRAM PUF, ML-KEM-768)
        │
        │  Post-Quantum Encrypted Stream
        ▼
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        SEMANTICA OWNS EVERYTHING BELOW THIS LINE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        │
        ▼
Layer 1 · SHACL Ingestion Gate          (packet → accept / reject)
        │
        ▼
Layer 2 · LayoutLMv3 Forensic Clean Room (documents → Genesis Matrix)
        │
        ▼
Layer 3 · Bi-Temporal Knowledge Graph   (facts → timestamped graph)
        │
        ▼
Layer 4 · Betweenness Centrality Engine (graph → C_B → SIU_adjusted)
        │
        ▼
Layer 5 · Rete Compliance Engine        (facts → approved / blocked)
        │
        ▼
Layer 6 · S-1 Mint Decision Tracker     (decision → causal object)
        │
        ▼
Layer 7 · Yield Compression Event Engine (breach → 4:1 lock < 100ms)
        │
        ▼
Layer 8 · Provenance Manager            (entity → DOI chain)
        │
        ▼
Layer 9 · W3C PROV-O Turtle Export      (lineage → .ttl audit file)
        │
        ▼
Layer 10 · FastAPI + WebSocket Surface  (data → REST + WS endpoints)
        │
        ▼
Layer 11 · Dashboard Data Feeds         (endpoints → 8 UI panels)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        │
        │  Verified Oracle Handshake
        ▼
STOKR INFRASTRUCTURE
(Liquid Network, Blockstream AMP, ORO Fund SPV)
```

---

## Layer 1 — SHACL Ingestion Gate

**File:** `backend/ingestion/shacl_gates.py` + `backend/ingestion/ontology.ttl`

### What Semantica Does

Semantica defines the canonical OWL ontology for all TFE entity types and auto-derives SHACL shape constraints from it. Every raw telemetry packet arriving from TFE-ib (biophysical) or TFE-gdp (SCADA/industrial) simulators is evaluated against these shapes before any data is written to the knowledge graph.

### OWL Ontology Entities Semantica Defines

- `tfe:BiophysicalNode` — a monitored ecological resource node (Nodes 1 and 2)
- `tfe:IndustrialNode` — a monitored SCADA/logistics node (Nodes 3 and 4)
- `tfe:TelemetryReading` — a timestamped sensor measurement with unit and source
- `tfe:ThresholdEvent` — a reading that meets or exceeds a defined critical threshold
- `tfe:MintDecision` — a sovereign minting or throttling event with full metadata
- `tfe:CompressionEvent` — a 4:1 collateral squeeze trigger event

### SHACL Gate Behaviour

- A packet that **passes** all shape constraints proceeds to the knowledge graph
- A packet that **fails** any constraint is immediately rejected with a plain-English validation report describing exactly which property violated which constraint
- The failed packet is logged to the rejection audit trail but **never written to the graph** and **never forwarded to STOKR**

### Acceptance Criteria

- 100% of intentionally corrupted test packets rejected — zero false passes
- SHACL validation latency per packet: < 10ms
- Validation report human-readable in under 2 sentences per violation

---

## Layer 2 — LayoutLMv3 Forensic Clean Room

**File:** `backend/ingestion/cleanroom.py`

### What Semantica Does

Semantica containerises and orchestrates the LayoutLMv3 document parsing pipeline (Docker service). The pipeline ingests 20–40 years of historical Sri Lanka government records — PDFs, CSVs, scanned registers — and produces the **Genesis Matrix**: a clean, versioned Parquet dataset that serves as the immutable historical baseline for the knowledge graph.

### Input Documents Processed (by Node)

- **Node 1 — Highland Hydrology:** 40yr daily rainfall registries (Department of Meteorology), reservoir depth sonar charts (Water Resources Board), NOAA GHCNd gap-fill CSVs
- **Node 2 — Coastal Blue Carbon:** 30yr deltaic bathymetric charts, mangrove baseline maps (JAXA Global Mangrove Watch), storm-surge manifests (Coast Conservation Dept.)
- **Node 3 — Eppawala Mining:** 20yr SCADA log streams, automated weigh-bridge manifests, refinery mass-balance registers (GSMB Sri Lanka)
- **Node 4 — Port of Colombo:** Shipping bills of lading, port flow meter histories, customs documentation (SLPA, Sri Lanka Customs)

### Clean Room Rules

- Any entry with a tampered or missing timestamp is flagged and excluded from the Genesis Matrix output
- Any entry where the recorded value falls outside the physically plausible range for that sensor type is quarantined and logged
- Any entry from a source that cannot be traced to an official government authority or DOI-registered dataset is excluded

### Output

The Genesis Matrix is a versioned Parquet file with the schema:

```
node_id | reading_type | valid_time | recorded_at | value | unit | source_doi | confidence
```

### Acceptance Criteria

- LayoutLMv3 cleanroom produces a valid Parquet with no tampered entries passing through
- Every row in the Genesis Matrix has a `source_doi` or `source_authority` field populated

---

## Layer 3 — Bi-Temporal Knowledge Graph

**File:** `backend/graph/temporal_graph.py` + `backend/graph/context_graph.py`

### What Semantica Does

Semantica maintains the live 4-node Sri Lanka sovereign hypergraph using `TemporalKnowledgeGraph` and `ContextGraph`. Every asserted fact is stored with **two independent timestamps** — these are never conflated and never overwritten.

### Dual-Timestamp Schema

- `valid_time` — when the fact was true in the real world (e.g. the date a reservoir level was measured)
- `recorded_at` — when Semantica ingested the fact (the ingestion timestamp)

This separation is the legal foundation of the entire system. A fact can be ingested today but have a `valid_time` of 1994. An auditor can prove both dates independently.

### Key API Methods Semantica Must Expose

```python
graph.state_at("1990-01-01")
# Returns the complete 4-node hypergraph as it existed on that date.
# Uses valid_time to filter — not recorded_at.

graph.compute_delta(snapshot_a, snapshot_b)
# Returns structural and value differences between two temporal snapshots.

graph.assert_fact(entity, property, value, valid_time, recorded_at, confidence)
# Writes a bi-temporal fact. Cannot overwrite an existing valid_time record.
```

### Allen Interval Algebra Anomaly Detection

Semantica applies the 13 Allen temporal relations to detect timing anomalies in historical SCADA logs and biophysical readings:

- `meets` / `met-by`
- `overlaps` / `overlapped-by`
- `during` / `contains`
- `starts` / `started-by`
- `finishes` / `finished-by`
- `equals`
- `before` / `after`

A detected anomaly (e.g. a downstream effect `before` its upstream cause) is flagged in the graph as a `tfe:TemporalAnomaly` entity and surfaced in the dashboard. No LLM is used to interpret the anomaly — the Allen algebra relation is deterministic.

### Acceptance Criteria

- `graph.state_at("1990-01-01")` returns a valid, non-empty graph distinct from `graph.state_at("2024-01-01")`
- `compute_delta(1990, 2024)` returns a non-empty set of structural and value changes
- Allen Interval Algebra anomaly detection identifies at least one temporal inconsistency in the seeded SCADA test data

---

## Layer 4 — Betweenness Centrality Engine

**File:** `backend/graph/centrality.py`

### What Semantica Does

Semantica computes **Betweenness Centrality (C_B)** for each of the 4 Sri Lanka nodes within the sovereign hypergraph. C_B quantifies how many shortest paths between all other node pairs pass through each given node — a direct measure of systemic criticality.

### C_B Interpretation for Sri Lanka

- **Node 1 (Highland Hydrology)** — high ecological C_B because it feeds freshwater to Nodes 2 (coastal mangroves) and indirectly constrains agricultural output linked to Node 4 trade flows
- **Node 2 (Coastal Blue Carbon)** — moderate C_B; shields Node 4 from storm-surge disruption
- **Node 3 (Eppawala Mining)** — low-to-moderate C_B; direct commodity export path to Node 4 but limited ecological interdependency
- **Node 4 (Port of Colombo)** — highest economic C_B; all sovereign trade flows route through this node

### ΣE_D — Downstream Asset Exposure

For each node, Semantica maintains a hardcoded set of `E_D` coefficients sourced from the Genesis Matrix:

- **Node 1 E_D:** catchment recharge contribution rate (m³/yr), flood attenuation value (USD/event)
- **Node 2 E_D:** storm-surge attenuation value (USD/event), blue-carbon sequestration rate (tCO₂/yr)
- **Node 3 E_D:** phosphate export revenue (USD/yr), estimated resource lifespan (years)
- **Node 4 E_D:** container TEU throughput velocity (TEU/yr), port uptime coefficient

### SIU Valuation Formula — Live Computation

```
SIU_adjusted = f(C_B × ΣE_D) × (1 − Ω_Threshold)
```

Semantica owns all three variables:

- `C_B` — computed from the live graph state (sub-50ms)
- `ΣE_D` — summed across all 4 nodes using Genesis Matrix coefficients
- `Ω_Threshold` — derived from the most recent SHACL-validated sensor readings; updated on every successful packet ingestion

The formula output is the floor price value that STOKR uses to determine the SIU reserve valuation. It is recomputed on every graph state change — no caching of stale values.

### Acceptance Criteria

- C_B computed for all 4 nodes in < 50ms on each graph state change
- `SIU_adjusted` recomputes automatically on every new validated telemetry packet
- C_B values are deterministic — same graph state always yields the same C_B

---

## Layer 5 — Rete Compliance Engine

**Files:** `backend/reasoning/rete_engine.py` + `backend/reasoning/rules/bad_neighbor.py` + `backend/reasoning/rules/covenants.py`

### What Semantica Does

Semantica owns the deterministic compliance engine. All regulatory and ecological rules are pre-compiled into a Rete network at service startup — evaluated as pattern-matching over working memory, not as LLM prompts, not as vector similarity searches.

**The Rete network is the only component permitted to make a binary compliance decision. No other component in the system has this authority.**

### The 6 Rules Semantica Owns

**Rule 1 — Highland Aquifer Drawdown (Node 1)**
- Condition: aquifer drawdown velocity > recharge rate for the current season
- Action: reject the affected node; flag `tfe:AquiferBreachEvent`; block SIU-T minting for Node 1

**Rule 2 — Mangrove Invasive Species (Node 2)**
- Condition: invasive species density index > threshold in the coastal perimeter monitoring zone
- Action: reject the affected node; flag `tfe:InvasiveSpeciesEvent`; block SIU-T minting for Node 2

**Rule 3 — SCADA Thermodynamic Harmonic Deviation (Node 3)**
- Condition: extraction mill thermodynamic harmonics fall outside ±2σ of the genesis baseline
- Action: reject the SCADA stream; flag `tfe:HarmonicAnomalyEvent`; suspend Node 3 from the C_B calculation pending manual review

**Rule 4 — Port Manifest Weight Divergence (Node 4)**
- Condition: PLC crane load weight vs. bill of lading declared weight diverges by > 3%
- Action: flag `tfe:ManifestDiscrepancyEvent`; escalate to compliance log; does not block minting unless divergence persists across 3 consecutive manifests

**Rule 5 — Wildfire Fuel Continuity Index (Nodes 1 & 2)**
- Condition: wildfire fuel continuity index for a biophysical node breaches the critical threshold
- Action: reject the affected node; flag `tfe:FireRiskEvent`; block SIU-T minting for that node

**Covenant Rule — 2:1 Over-Collateralisation Lock**
- Condition: proposed SIU-T mint would cause circulating SIU-T supply to exceed 50% of the current SIU parent reserve
- Action: reject the mint call immediately; raise a structured error; never permit the STOKR endpoint to receive the mint signal

### ReteEngine API Contract

```python
result = ReteEngine.evaluate(telemetry_packet)
# Returns:
# {
#   "approved": bool,
#   "failing_rule": str | None,   # e.g. "Rule 1 — Aquifer Drawdown"
#   "flagged_events": list[str],  # zero or more tfe:EventType strings
#   "evaluation_id": str,         # UUID bound to this evaluation
# }
```

### Key Invariants

- The Rete ruleset is compiled **once** at service startup — never recompiled per evaluation call
- 1,000 evaluations on identical inputs must produce identical outputs (zero variance)
- No LLM API call may appear anywhere in the compliance evaluation path
- A failing evaluation must name the exact rule that failed — generic "compliance failed" errors are not acceptable

### Acceptance Criteria

- All 6 rules fire deterministically on every run
- 5 compliant test packets → all pass; 5 non-compliant packets → all fail naming the correct rule
- Zero LLM calls confirmed by grep on the evaluation code path

---

## Layer 6 — S-1 Mint Decision Tracker

**File:** `backend/reasoning/decision_tracker.py`

### What Semantica Does

Every minting decision and every throttle decision is a first-class object in the Semantica graph — not a log line, not a database row. Semantica creates an immutable causal object that binds the decision to its exact inputs, the Rete evaluation result, and the full backward-trace to originating sensor readings.

### Three API Methods Semantica Must Expose

**`graph.record_decision()`** — writes the decision object to the knowledge graph

```python
decision_id = graph.record_decision(
    category="s1_sovereign_mint",          # or "yield_compression", "mint_blocked"
    outcome="mint_siu_t",                  # or "squeeze_4_1", "blocked"
    confidence=0.98,
    rationale="Baseline biophysical conditions satisfied. All 4 nodes stable.",
    entities=["node1_highland", "node2_coastal", "node3_mining", "node4_port"],
)
```

**`graph.check_decision_rules()`** — runs the Rete evaluation and binds the result to the decision object

```python
compliance = graph.check_decision_rules(
    decision_id,
    ruleset="sir_v4_2_compliance"
)
# compliance.approved: bool
# compliance.failing_rule: str | None
# compliance.evaluation_id: str
```

**`graph.trace_decision_chain()`** — walks the causal graph backward to the originating sensor

```python
causal_chain = graph.trace_decision_chain(decision_id)
# Returns an ordered list of graph nodes from the decision object
# back through derived metrics, intermediate computations,
# and ultimately to the raw sensor reading with its:
#   - node_id
#   - sensor_type
#   - valid_time (exact timestamp of the original reading)
#   - recorded_at (ingestion timestamp)
#   - raw_value and unit
#   - source_doi or source_authority
```

### Blocked Mint Contract

If `check_decision_rules()` returns `approved=False`:

- The mint call raises a structured `MintBlockedError` immediately
- The error payload contains: `decision_id`, `failing_rule`, and the partial `causal_chain` up to the point of failure
- No signal reaches the STOKR TaaS endpoint
- The blocked decision object remains in the graph with `outcome="blocked"` — it is never silently discarded

### Acceptance Criteria

- `record_decision()`, `check_decision_rules()`, and `trace_decision_chain()` all functional and tested
- `trace_decision_chain()` returns a chain reaching at least 3 hops back to a raw sensor value
- Blocked decisions are visible in the Mint Feed dashboard panel with the correct failing rule displayed

---

## Layer 7 — 4:1 Yield Compression Event Engine

**Files:** `backend/reasoning/rete_engine.py` + `backend/reasoning/decision_tracker.py`

### What Semantica Does

When `Ω_Threshold ≥ Ω_Crit`, Semantica's Rete network fires the Yield Compression Event in under 100ms. No human confirmation. No LLM interpretation. No probabilistic delay.

### The Collateral Squeeze Rule

```
γ = { 2:1  if Ω_Threshold < Ω_Crit      ← normal baseline conditions
    { 4:1  if Ω_Threshold ≥ Ω_Crit      ← Yield Compression Event
```

### The 6-Step Compression Sequence Semantica Owns

1. **Breach detection** — an incoming SHACL-validated telemetry packet updates `Ω_Threshold` in the knowledge graph; Rete immediately evaluates the compression rule against the new value
2. **Rete fires** — the compression condition (`Ω_Threshold ≥ Ω_Crit`) matches in working memory; the Rete network triggers the Yield Compression Event with zero delay
3. **Decision object created** — `record_decision(category="yield_compression", outcome="squeeze_4_1")` writes an immutable causal object to the graph, bound to the exact breach packet
4. **Causal chain attached** — `trace_decision_chain()` is invoked automatically and attached to the decision object before the STOKR signal is sent
5. **STOKR signal dispatched** — the decision object (including causal chain) is posted to the STOKR TaaS stub endpoint `/collateral-squeeze`
6. **Collateral ratio updated** — the circulating SIU-T supply is now constrained to 25% of the SIU parent reserve (4:1 lock), down from 50% (2:1 baseline)

### SLA

- p99 latency from breach packet ingestion to 4:1 lock signal dispatched: **< 100ms**
- This SLA applies to the Semantica processing path only — network latency to STOKR is excluded

### Acceptance Criteria

- Inject a simulated Node 1 aquifer breach → 4:1 lock signal received at STOKR stub in < 100ms
- The causal chain on the compression decision object traces back to the exact breach sensor reading
- Collateral ratio panel in the dashboard transitions from 2:1 to 4:1 with the Framer Motion animation firing on WebSocket push

---

## Layer 8 — Provenance Manager

**File:** `backend/provenance/manager.py`

### What Semantica Does

Every asserted fact in the knowledge graph — every sensor reading, every derived metric, every Genesis Matrix row loaded into the graph — must have a provenance record binding it to its originating source. Semantica's `ProvenanceManager` owns this binding from the moment of ingestion.

### Provenance Record Schema

Every entity in the graph must have a provenance record containing:

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
# Returns the full ancestor chain:
# node1_highland_recharge
#   ← derived_from: highland_aquifer_model_2024
#       ← derived_from: dept_of_meteorology_rainfall_1984_2024.csv
#           ← source: doi:10.xxxx/slhydro.2024.001 (page 42)
```

### Minimum Standard

- Every entity in the graph must have a provenance chain traceable to a DOI or named government authority
- The chain must be at least 3 hops deep for any SIU-influencing metric
- No SIU valuation component may be derived from a source with confidence < 0.80

### Acceptance Criteria

- `prov.get_lineage()` returns a ≥ 3-hop chain for each of the 4 node entities
- Every row in the Genesis Matrix has a corresponding provenance record before graph loading begins

---

## Layer 9 — W3C PROV-O Turtle Export

**File:** `backend/provenance/exporter.py`

### What Semantica Does

Semantica converts the provenance graph into a compliance-grade W3C PROV-O Turtle (`.ttl`) file. This file is the primary artifact delivered to international auditors, rating agencies, and central bank regulators. It must be machine-parseable, standards-compliant, and self-contained.

### Required PROV-O Triples in Every Export

Every exported Turtle file must contain:

- `prov:Entity` — one entry per tracked data entity in the decision's lineage
- `prov:wasDerivedFrom` — the full lineage chain linking derived entities to source entities
- `prov:wasAttributedTo` — the government body, institution, or sensor that produced the claim
- `prov:generatedAtTime` — the `recorded_at` ingestion timestamp (ISO 8601)
- `prov:wasAssociatedWith` — the parsing agent (LayoutLMv3 cleanroom) or sensor simulator that generated the claim
- `prov:used` — links each activity to the entities it consumed

### Export API

```python
RDFExporter().export(
    lineage,
    "sir_sovereign_audit_trail.ttl",
    format="turtle"
)
```

### Validation Gate

Before any `.ttl` file is considered a valid PoC artifact:

1. `rdflib.Graph().parse("sir_sovereign_audit_trail.ttl", format="turtle")` must complete with zero errors
2. A SPARQL query for each required triple class must return at least one result
3. The file must be self-contained — no external URI dependencies that could resolve to 404

### Acceptance Criteria

- One-click export from the dashboard generates a valid `.ttl` file in < 2 seconds
- The file parses with zero errors in rdflib
- PROV-O triple validation passes for all 5 required triple types
- Exports are generated for: all 4 node lineages + the most recent mint decision + the most recent compression event

---

## Layer 10 — FastAPI + WebSocket Surface

**File:** `backend/api/main.py`

### What Semantica Does

Semantica exposes its internal graph, reasoning, and provenance state through a FastAPI application. This is the only interface the Next.js dashboard and the STOKR TaaS stub consume. All endpoints are read-consistent with the live graph state.

### REST Endpoints (7)

**`POST /ingest`**
- Accepts a raw telemetry packet (JSON)
- Runs SHACL validation; returns `{accepted: bool, validation_report: str | None}`
- On acceptance: writes to graph, triggers C_B recalculation, pushes updated `SIU_adjusted` to WebSocket `/ws/telemetry`

**`GET /siu-value`**
- Returns the current `SIU_adjusted` with full breakdown: `C_B` per node, `ΣE_D` total, `Ω_Threshold` current value, and the raw formula evaluation

**`GET /compliance/{decision_id}`**
- Returns the Rete evaluation result and the full causal chain for a given decision ID

**`POST /mint`**
- Records a mint decision, runs `check_decision_rules()`, returns `{approved: bool, decision_id: str}` or `{approved: false, failing_rule: str, decision_id: str}`

**`GET /audit/{entity_id}`**
- Returns the full provenance lineage for a given graph entity; includes all PROV-O metadata fields

**`GET /graph/state`**
- Query parameter: `?date=YYYY-MM-DD`
- Returns the bi-temporal graph snapshot as of the given date using `graph.state_at()`

**`POST /simulate/breach`**
- Query parameter: `?node={1|2|3|4}`
- Injects a synthetic threshold breach for the specified node; triggers the full 6-step compression sequence

### WebSocket Routes (2)

**`/ws/telemetry`**
- Streams live `SIU_adjusted` updates, node health status, `Ω_Threshold` readings, and C_B values on every graph state change
- Throttled to 10 events/sec maximum to prevent Sigma.js render stalls

**`/ws/events`**
- Streams all compression events and mint decisions in real time as they are recorded in the graph
- Payload per event: `{event_type, decision_id, outcome, failing_rule | null, timestamp}`

### STOKR TaaS Stub (`backend/api/stokr_stub.py`)

- Receives `POST /collateral-squeeze` from the compression engine
- Logs: decision_id, causal_chain summary, old ratio, new ratio, timestamp
- Receives `POST /mint-signal` from approved mint decisions
- Returns `200 OK` with a stub confirmation token in both cases

### Acceptance Criteria

- All 7 REST endpoints return structurally correct responses confirmed by automated tests
- WebSocket `/ws/telemetry` delivers an update within 200ms of a graph state change
- OpenAPI schema auto-generated and accessible at `/docs`
- STOKR stub correctly logs all compression and mint signals with timestamps

---

## Layer 11 — Dashboard Data Feeds

**Directory:** `dashboard/`

Semantica's API feeds all 8 panels in the Next.js Sovereign Intelligence Dashboard. The panel-to-API mapping is:

### Panel 1 — Sovereign Hypergraph (Sigma.js + Graphology)

- **Source:** `GET /siu-value` (initial load) + `WS /ws/telemetry` (live updates)
- **Semantica data consumed:** C_B per node, health status per node, edge interdependency weights, Ω_Threshold per biophysical node
- **Behaviour:** Node color and size update on each WebSocket push; breach nodes pulse red via Framer Motion; Graphology graph object is mutated incrementally (never rebuilt)

### Panel 2 — SIU Valuation Card (Tremor + Recharts)

- **Source:** `WS /ws/telemetry`
- **Semantica data consumed:** `SIU_adjusted`, `C_B` breakdown per node, `ΣE_D` total, `Ω_Threshold`
- **Behaviour:** Animated counter updates on each WebSocket push; Recharts donut reflects current C_B split; Ω radial gauge sweeps toward critical zone as Ω_Threshold rises

### Panel 3 — Collateral Ratio Gauge (Framer Motion)

- **Source:** `WS /ws/events`
- **Semantica data consumed:** Current collateral ratio (2:1 or 4:1), SIU-T circulating supply, SIU parent reserve floor, seconds since last compression event
- **Behaviour:** Framer Motion spring animation transitions badge from green `2:1` to red `4:1` on compression event; Tremor progress bar shows SIU-T vs reserve floor

### Panel 4 — PROV-O Lineage Explorer (Sigma.js)

- **Source:** `GET /audit/{entity_id}` triggered on user selection
- **Semantica data consumed:** Full provenance lineage object including all entity IRIs, DOIs, authors, confidence scores, and `prov:` relationship types
- **Behaviour:** Second Sigma.js instance renders the DAG; click any node for tooltip with full metadata; export button calls `GET /audit/{entity_id}` and triggers `.ttl` download

### Panel 5 — Node Telemetry Timeline (Recharts)

- **Source:** `GET /graph/state?date=` for historical range + `WS /ws/telemetry` for live append
- **Semantica data consumed:** Per-node key sensor metric time series, genesis baseline values, historical threshold breach timestamps
- **Behaviour:** Recharts multi-line chart with baseline overlay and vertical breach markers; date range selector re-calls `GET /graph/state` with the appropriate date

### Panel 6 — Compression Event Feed

- **Source:** `WS /ws/events` filtered for `event_type == "yield_compression"`
- **Semantica data consumed:** `decision_id`, `outcome`, `timestamp`, expandable `causal_chain` from `GET /compliance/{decision_id}`
- **Behaviour:** Real-time push rows; click row to expand `trace_decision_chain()` output showing sensor → derived metric → Ω_Threshold → compression decision

### Panel 7 — Mint Decision Feed

- **Source:** `WS /ws/events` filtered for `event_type == "s1_sovereign_mint"` or `"mint_blocked"`
- **Semantica data consumed:** `decision_id`, `outcome`, `failing_rule | null`, `confidence`, `rationale`, node entity list
- **Behaviour:** Green `APPROVED` or red `BLOCKED — {failing_rule}` badge per row; click decision ID opens Panel 4 (PROV-O Lineage Explorer) for that decision

### Panel 8 — Trigger Control Panel

- **Source:** Outbound to `POST /simulate/breach` and `POST /simulate/restore`
- **Semantica data consumed:** WebSocket connection status from `WS /ws/telemetry`
- **Behaviour:** Four node breach buttons + one restore baseline button; green/red WebSocket indicator in the header; button disabled during an active squeeze (prevents double-trigger)

---

## Key Invariants — Things That Must Never Happen

These are hard boundaries. Violating any of these invalidates the PoC as a legally defensible artifact:

- **No LLM call in any compliance evaluation path** — grep on startup confirms zero OpenAI / Anthropic / Cohere API calls reachable from `rete_engine.py` or `shacl_gates.py`
- **No unvalidated packet reaches the knowledge graph** — the SHACL gate is the only entry point; there is no bypass route
- **No mint signal reaches STOKR before `check_decision_rules()` returns `approved=True`** — the endpoint call is gated behind the Rete evaluation result
- **No decision object is silently discarded** — blocked decisions are written to the graph with `outcome="blocked"` and remain permanently queryable
- **No `SIU_adjusted` value is cached beyond one graph state change** — the formula is recomputed on every validated telemetry ingestion
- **No `.ttl` file is considered valid before parsing with zero rdflib errors** — the export function must validate before returning success

---

## Binary Acceptance Gates Summary

These 7 gates must all pass for the PoC to be considered complete:

| Gate | Test | Pass Condition |
| --- | --- | --- |
| G1 | Rete determinism | 1,000 evaluations on identical input → identical output, zero variance |
| G2 | Zero LLM in compliance path | grep / trace confirms no LLM API call reachable from compliance code |
| G3 | Squeeze < 100ms | p99 breach-to-4:1-lock latency < 100ms in benchmark |
| G4 | Causal chain complete | `trace_decision_chain()` reaches originating sensor with node ID, timestamp, and breach value |
| G5 | PROV-O valid | Generated `.ttl` parses with zero rdflib errors; all 5 triple types present |
| G6 | Bi-temporal replay | `graph.state_at("1990-01-01")` ≠ `graph.state_at("2024-01-01")`; both non-empty and structurally correct |
| G7 | SHACL gate | 100% of corrupted test packets rejected before knowledge graph contact |

---

*All responsibilities in this document are owned by Semantica Engineering and are deliverable within the 4-week PoC window (July 1–25, 2026).*
