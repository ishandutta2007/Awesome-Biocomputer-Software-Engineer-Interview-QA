# Topic 07: Data Management & Provenance

## Overview
Experimental data pipelines, metadata standards, and reproducibility requirements for biocomputing research — the data infrastructure enabling rigorous science and long-term substrate knowledge accumulation.

---

### Q1: What metadata must be captured alongside raw electrophysiology data to enable meaningful analysis and reproducibility, and why is this richer than metadata requirements for conventional computing hardware logs?

**A:**
**Core metadata categories uniquely demanding for biological substrates:**

1. **Biological substrate provenance and developmental history:** Unlike a conventional computing hardware log where the hardware's identity is fixed and unchanging, biological substrates have a continuous developmental/adaptation history that is essential context for interpreting any recorded data — metadata must capture: cell line/organoid batch origin, culture protocol details, days-in-vitro (DIV) at recording, biological substrate preparation and handling procedures, and any prior stimulation/experimental history the substrate has been exposed to (since prior experience shapes the biological network's current state through plasticity). A data file lacking this biological context is often uninterpretable in isolation.

2. **Recording session environmental conditions:** Temperature, CO₂/O₂ levels, media composition and batch, time since last media change — all physiologically relevant factors affecting biological substrate behavior that have no analogue in conventional hardware logging.

3. **Electrode array geometry, channel mapping, and impedance measurements:** Detailed spatial mapping of which physical electrode corresponds to which data channel, electrode impedance values (relevant to signal quality interpretation), and any channel exclusions/quality annotations — particularly important since electrode quality varies across a multi-electrode array and changes over time.

4. **Stimulation history during the recording session:** Complete log of all stimulation pulses delivered (timing, amplitude, duration, waveform, target electrodes) — essential for interpreting the biological substrate's activity during and after stimulation, and for reconstructing the full closed-loop input-output history when replaying or analyzing recorded sessions.

5. **Software/algorithm configuration versions and parameters:** All signal processing parameters used (filter cutoffs, spike detection thresholds, sorting parameters) — since changing these parameters can substantially affect derived data products (detected spikes, sorted units) in ways that make cross-session comparisons unreliable if parameter versions aren't tracked.

**Why richer than conventional computing metadata:** Conventional hardware log metadata is primarily about capturing system operational parameters that are stable and largely known in advance (hardware model, firmware version, sampling rate) — biological substrates add a biologically dynamic, continuously-evolving context (developmental history, network adaptation history, real-time physiological state) that must be comprehensively captured since it can substantially affect data interpretation and is genuinely unknowable in advance at system design time.

### Q2: Design a data management architecture for a longitudinal biocomputing experiment spanning several months, where the biological substrate undergoes continuous development and must be tracked across dozens of recording sessions.

**A:**
**Architecture approach:**
```
Experiment/substrate registration layer:
  - Unique substrate identifier created at substrate initialization
  - Linked to all downstream sessions, stimulation events, biological events
  ↓
Per-session data capture:
  - Raw electrophysiology data (NWB or equivalent standard format)
  - Full metadata bundle (Q1's categories) linked to substrate ID
  - Stimulation log linked to session ID
  - Signal quality annotations and channel health assessments
  ↓
Substrate state history database:
  - Longitudinal substrate state trajectory (unit activity profiles,
    network connectivity estimates, electrode impedance history)
  - Biological events log (media changes, microscopy observations,
    any biological anomalies observed)
  - Derived analysis results linked to specific raw data versions
    (enabling re-analysis with updated algorithms without losing
    the original analysis results)
  ↓
Cross-session analysis layer:
  - APIs supporting queries spanning multiple sessions for the same substrate
  - Substrate age/developmental state as a first-class query dimension
  - Change-detection and drift quantification across the longitudinal trajectory
```

**Key architectural principles:**
1. **Immutable raw data with versioned derived products:** Raw electrophysiology recordings should be stored immutably (never modified after capture), with derived analysis results (spike sorting outputs, decoded signals) stored separately as versioned products that can be regenerated from the immutable raw data using specified algorithm/parameter versions — enabling re-analysis with improved algorithms without overwriting or losing any original data or original analysis results.

2. **NWB (Neurodata Without Borders) or equivalent standardized data format adoption:** Adopting community-standard data formats (e.g., NWB, which has achieved substantial adoption in the neuroscience community specifically to address data portability and reproducibility challenges) enables data sharing with collaborators, long-term data accessibility as software tools evolve, and access to the broader analysis tool ecosystem built around these standard formats — rather than a proprietary format requiring custom reader tools that may not be maintained long-term.

3. **Substrate knowledge graph as a longitudinal semantic layer above raw session data:** For multi-month longitudinal experiments, a higher-level substrate "knowledge graph" representation — tracking learned knowledge about the specific biological substrate (which regions show specific functional properties, how specific network features have evolved over developmental time, what interventions have produced which effects in this specific substrate) as a continuously-updated semantic layer above raw session data — enables increasingly informed experimental design and interpretation as knowledge about the specific substrate accumulates, rather than treating each session's data as an isolated snapshot without explicit accumulation of substrate-specific knowledge over time.

### Q3–Q14: (Representative additional topics)
- NWB (Neurodata Without Borders) format specification and adoption practical guidance
- FAIR data principles (Findability, Accessibility, Interoperability, Reusability) applied to biocomputing research data
- Data compression strategies for high-channel-count, long-duration neural recordings
- Database technology choices for biocomputing data management (time-series databases, graph databases, document stores)
- Automated quality control and data validation at recording time versus post-hoc
- Secure data storage and access control for biocomputing research data involving human subjects or sensitive biological materials
- Long-term data preservation and archival strategy for multi-year biological computing research programs
- Integration with electronic laboratory notebook systems and experimental planning tools
- Data sharing and open science considerations for biocomputing research data
- Data management regulatory requirements for biocomputing research programs subject to institutional oversight

---

## Summary
Data management and provenance for biological computing substrates demands substantially richer, more biologically-contextualized metadata than conventional computing hardware logging — requiring longitudinal substrate developmental history tracking, standardized data format adoption, and immutable-raw-data-with-versioned-derived-products architecture to enable reproducible, interpretable multi-month experiments generating lasting substrate knowledge.
