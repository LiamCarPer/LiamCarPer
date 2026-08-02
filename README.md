# Liam Carvajal

**MLOps & Industrial ML | Gated model promotion · Predictive maintenance · OT-domain systems**

I build production ML systems where a model only reaches production by passing an enforceable quality gate, every prediction carries its lineage back to code, data, and training run, and the metrics match the real cost of being wrong. My domain context comes from OT/ICS environments — I treat industrial signals (vibration, protocols, physics) as first-class features, not noise.

[LinkedIn](https://www.linkedin.com/in/liam-carvajal-perez/) · [Email](mailto:carvajalperezliam7@gmail.com) · Based in Spain (Open to Remote Europe/USA)

---

## The Loop

GatedOps is the operations layer: train → evaluate → gate → register → promote → serve, with lineage on every prediction. AetherPdM is the vertical that consumes the same contract for industrial predictive maintenance.

```mermaid
graph LR
    subgraph GatedOps["GatedOps - Model Operations"]
        T[Train<br/>config + data] --> E[Evaluate<br/>metrics vs champion]
        E --> G{Gate<br/>thresholds}
        G -- fail --> T
        G -- pass --> R[Register<br/>MLflow version + tag]
        R --> P[Promote<br/>staging -> prod]
        P --> S[Serve<br/>production alias only]
        S --> L[Lineage<br/>manifest: code + data + run]
    end
    A[AetherPdM<br/>Industrial PdM] -->|gated models + lineage| S
```

---

## Featured Projects

### [GatedOps](https://github.com/LiamCarPer/GatedOps)
**The Problem:** Most teams can train a model; few have a system where a bad model cannot be promoted and every prediction can be traced to its code, data, and training run.
**The Solution:** A reference MLOps platform — gated train/evaluate/promote/serve with full lineage. Models pass threshold gates vs. the champion before they can be registered (MLflow) and promoted (staging → production alias only); a CI workflow fails the pipeline with a `GateReport` when a model does not clear the bar.
*   **Engineering Challenge:** An MLflow-free gate engine with challenger/champion rules — generic over any `predict_proba` model, and identical locally, in CI, and against the production stack.
*   **Stack:** Python, MLflow, FastAPI, Docker Compose, uv, pytest, GitHub Actions.

### [AetherPdM](https://github.com/LiamCarPer/AetherPdM)
**The Problem:** Unplanned downtime in rotating equipment costs billions annually, and 40-60% of maintenance alerts are noise — rule-based thresholds don't adapt to load or operating conditions.
**The Solution:** End-to-end predictive maintenance: vibration waveforms → domain-aware signal features → anomaly score + fault classification → REST serving with model versioning, lineage, and operator-facing explanations.
*   **Engineering Challenge:** Anti-leakage train/test splits, and physics-informed features (envelope analysis, BPFO/BPFI/BSF, band power) that separate real bearing faults from statistical noise.
*   **Stack:** Python, scikit-learn, SciPy, FastAPI, MLflow, Parquet, Docker, uv, pytest, GitHub Actions.

### [OT-Security-Lab](https://github.com/LiamCarPer/OT-Security-Lab)
**The Problem:** You can't test attacks on live water treatment plants.
**The Solution:** A 5-zone Docker lab mapped to the Purdue Model and IEC 62443 — protocol-aware detection (Modbus DPI, DNP3), a physics-aware safety monitor that shadows PLC state, and a Grafana/Loki SIEM with SOAR-lite automation.
*   **Engineering Judgment:** The pipeline is machine-verified end to end: 10 CI gates plus a Compliance Gate that boots the lab, replays attack simulations, and **commits fresh detection evidence on every green run**; SBOMs are keyless-signed via Sigstore. This is where I learned that in OT, a false positive costs more than a miss — the same principle now drives my ML metric design.
*   **Stack:** Docker, OpenPLC, Scada-LTS, Scapy, DNP3, Grafana/Loki, OPA/conftest, GitHub Actions. [Live site](https://liamcarper.github.io/OT-Security-Lab/) · v1.0.1

---

## Also

- [Cloud Telemetry Lake](https://github.com/LiamCarPer/cloud-telemetry-lake) — serverless OT telemetry ingest (Terraform, Lambda, S3, DynamoDB, Fluent Bit)
- [OT-NDR-Malcolm-Pipeline](https://github.com/LiamCarPer/OT-NDR-Malcolm-Pipeline) — CISA Malcolm NDR with a custom Modbus DPI SOAR layer
- [ICS Agentic SOC Pipeline](https://github.com/LiamCarPer/ics-agentic-soc-pipeline) — agentic, NIST-aligned incident reporting (LangGraph, RAG, Isolation Forest)
- [Log Parser Toolkit](https://github.com/LiamCarPer/log-parser-toolkit) — generator-based log parsing with near-zero RAM overhead
- [rust-security-toolkit](https://github.com/LiamCarPer/rust-security-toolkit) & [solana-audit-toolkit](https://github.com/LiamCarPer/solana-audit-toolkit) — Rust/Solana program auditing tooling

---

## How I Build ML Systems

- **Gates before production:** a model that fails its quality bar cannot be promoted — the gate proves it, in CI, with artifact-hash integrity.
- **Domain metrics over vanity accuracy:** I design metrics to match the cost of being wrong (false-alarm rate, downtime) — the availability-first mindset I learned in OT.
- **Lineage and reproducibility:** every served prediction traces to its exact code, data, and training run; promote/serve is explicit and reversible.
- **OT literacy as context:** industrial protocols and physics-aware signals (envelope, BPFO, process state) inform how I structure features — not just what I train on.

---

## Stack

**MLOps & Data**
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white) ![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=flat-square&logo=scipy&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white) ![MLflow](https://img.shields.io/badge/MLflow-0194E2?style=flat-square&logo=mlflow&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white) ![uv](https://img.shields.io/badge/uv-0B0B0B?style=flat-square&logo=uv&logoColor=white) ![Parquet](https://img.shields.io/badge/Parquet-50ABF1?style=flat-square) ![Time Series](https://img.shields.io/badge/Time%20Series-007396?style=flat-square)

**Cloud & Infrastructure**
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat-square&logo=amazonaws&logoColor=white) ![Lambda](https://img.shields.io/badge/AWS%20Lambda-FF9900?style=flat-square&logo=awslambda&logoColor=white) ![S3](https://img.shields.io/badge/S3-569A31?style=flat-square&logo=amazons3&logoColor=white) ![DynamoDB](https://img.shields.io/badge/DynamoDB-4053D6?style=flat-square&logo=amazondynamodb&logoColor=white) ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white) ![LocalStack](https://img.shields.io/badge/LocalStack-51BBFE?style=flat-square)

**OT Domain**
![IEC 62443](https://img.shields.io/badge/IEC%2062443-005B96?style=flat-square) ![MITRE ATT&CK for ICS](https://img.shields.io/badge/MITRE%20ATT%26CK%20for%20ICS-C8102E?style=flat-square) ![Modbus/TCP](https://img.shields.io/badge/Modbus%2FTCP-004466?style=flat-square) ![DNP3](https://img.shields.io/badge/DNP3-0F4C81?style=flat-square) ![OpenPLC](https://img.shields.io/badge/OpenPLC-1B5E20?style=flat-square) ![Scapy](https://img.shields.io/badge/Scapy-FF6B6B?style=flat-square) ![Malcolm NDR](https://img.shields.io/badge/Malcolm%20NDR-2F4F4F?style=flat-square) ![Zeek](https://img.shields.io/badge/Zeek-2D2D2D?style=flat-square) ![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white) ![Loki](https://img.shields.io/badge/Loki-3A6EA5?style=flat-square)

---

## Professional Development

- **Now:** MLOps platform practice — gated promotion, model lineage, cloud ML deployment — and industrial ML on vibration/rotating-equipment signals.
- **Background:** OT/ICS security engineering — IEC 62443 zones and conduits, MITRE ATT&CK for ICS detection mapping, protocol-aware detection, DevSecOps pipelines.

---

## Open to

Building production ML systems — gating, lineage, industrial predictive maintenance — with a background in OT/ICS environments. Open to **MLOps / ML Platform / Industrial ML** roles, remote within Europe/USA. If you're building model infrastructure or industrial analytics, let's talk.
