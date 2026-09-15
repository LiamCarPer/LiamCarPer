# Liam Carvajal

**OT Detection Engineer | Detection-as-Code · OT NDR · MITRE ATT&CK for ICS**

I build OT detection that holds up in a real plant. That means content written once and generated everywhere, rules that understand what a Modbus function code or a DNP3 operate actually does, and coverage measured against adversary emulation instead of guessed at. Architecture is part of that job too — zones and conduits, IT/OT segmentation and DMZ design, secure remote access — because a detection is only ever as good as the telemetry the network lets through. I work across legacy industrial protocols (Modbus, PROFINET, DNP3, OPC UA, IEC 61850) and the brownfield reality of adding monitoring to a running facility.

Currently **OT Security Analyst (Incident Response & Threat Hunting) @ Rockwell Automation** — industrial detection, threat hunting and incident response in production OT environments.

[LinkedIn](https://www.linkedin.com/in/liam-carvajal-perez/) · [Email](mailto:carvajalperezliam7@gmail.com) · Spain · **Open to EU remote & B2B / contract engagements**

---

## 🔍 How detection reaches the plant

The rule source is the center of gravity. Everything downstream — edge sensors, SIEM queries, coverage metrics — is generated from it, so nothing drifts and no rule is deployed by hand.

```mermaid
graph TD
    subgraph "Detection as Code"
        DE[OT Detection Engineering<br/>Sigma rules · protocol decoders · native Suricata]
    end

    subgraph "Plant / Edge (OT-Security-Lab)"
        PLC[PLCs · HMIs] -->|Modbus · DNP3 · S7comm · OPC UA| GW[Edge DPI / OT Gateway]
        GW -->|Suricata · Zeek| ML[Malcolm NDR Pipeline]
    end

    DE -.->|Sigma to Suricata| GW
    DE -.->|Sigma to Loki / OpenSearch| ML
    ML -->|Fluent Bit| S3[S3 Raw Telemetry]
    S3 -->|SQS · Lambda| LP[Log Parser Toolkit]
    LP -->|Detections| DDB[(DynamoDB)]
    DDB -->|Streams| IR[Automated NIST Reports]

    style DE fill:#cfe2ff,stroke:#333
    style GW fill:#f96,stroke:#333
    style LP fill:#ff9,stroke:#333
    style IR fill:#dfd,stroke:#333
```

---

## 🛡️ Detection Engineering at a Glance

*   **Rules as software** — pySigma-based validation over a parsed rule model, positive/negative fixtures, and structural governance for native Suricata rules.
*   **Protocol-aware content** — application-layer detections for Modbus, DNP3, S7comm and OPC UA, backed by Rust decoders rather than fragile byte offsets.
*   **Coverage you can prove** — ATT&CK for ICS coverage and MTTD / false-positive metrics derived from the rules themselves, never hand-maintained.
*   **Proven, not assumed** — content exercised against adversary emulation and a live lab run before it is trusted.
*   **One rule, many consumers** — Splunk, Microsoft Sentinel, OpenSearch and Grafana Loki queries all generated from a single source of truth.

---

## 🎯 Featured Work

### [OT Detection Engineering](https://github.com/LiamCarPer/ot-detection-engineering)
**The Problem:** OT detection content is written once, deployed by hand, duplicated across the SIEM and the NDR, and never measured — so nobody can say which ATT&CK for ICS techniques are covered, how fast detections fire, or whether a rule change broke one.
**The Solution:** A detection-as-code pipeline that treats detections as software: OT Sigma rules and native protocol DPI (Modbus, DNP3, S7comm, OPC UA), with Rust DNP3, S7comm and OPC UA decoders for application-layer events, validated and converted in CI from a single source of truth, proven against adversary emulation and deployed into a Malcolm NDR pipeline and the OT-Security-Lab Loki stack.
*   **Detection Engineering:** Built a pySigma-based validation matcher over the parsed rule model, labeled positive/negative fixtures, and structural governance for native Suricata rules. ATT&CK for ICS coverage and MTTD/false-positive metrics are generated, never hand-maintained.
*   **Impact:** Verified against a live run of OT-Security-Lab — 4/4 emulation expectations detected at a **2.45 s mean MTTD**, with Loki, OpenSearch, Splunk and Microsoft Sentinel queries generated from one rule source.
*   **Stack:** pySigma/sigma-cli, Sigma, Suricata, Rust, Grafana Loki, OpenSearch, Splunk, Microsoft Sentinel, JSON Schema, Python, GitHub Actions.

### [OT-NDR-Malcolm-Pipeline](https://github.com/LiamCarPer/OT-NDR-Malcolm-Pipeline)
**The Problem:** Commercial NDR (Nozomi/Claroty) is cost-prohibitive for many facilities.
**The Solution:** A production-grade NDR pipeline using CISA Malcolm, Arkime, and Suricata, enriched by a custom **Python SOAR layer**.
*   **Impact:** Implemented automated **DPI profiling** of Modbus function codes to identify unauthorized register manipulation before it hits the SIEM.
*   **Stack:** CISA Malcolm, Arkime, Suricata, Python (Scapy/Tshark).

### [ICS Agentic SOC Pipeline](https://github.com/LiamCarPer/ics-agentic-soc-pipeline)
**The Problem:** SOC analysts in OT environments drown in high-noise alerts. Generating NIST-aligned incident reports and Suricata rules manually is slow, inconsistent, and doesn't scale.
**The Solution:** An agentic AI pipeline that detects anomalies via Isolation Forest, enriches them with RAG-augmented OT knowledge (IEC 62443, asset inventories, past incidents), and produces NIST SP 800-61 reports with custom Suricata rules — all without human intervention.
*   **Engineering Challenge:** Built a deterministic classification layer that routes alerts to the correct analysis path before LLM invocation, eliminating token waste. Made the agent **LLM-agnostic** — swap between GPT-4o-mini and local Ollama models by changing two env vars.
*   **Stack:** Python, LangChain/LangGraph, ChromaDB, FastAPI, scikit-learn, OpenAI/OpenRouter, Pytest. 25 deterministic tests pass in CI without API keys.

### [OT-Security-Lab](https://github.com/LiamCarPer/OT-Security-Lab) — *the environment my detections are validated against*
**The Problem:** You can't test attacks on live water treatment plants.
**The Solution:** A 5-zone Docker-based simulation of a water filtration facility mapped to the **Purdue Model** and **IEC 62443**, with every inter-zone conduit enforced through a dedicated iptables gateway.
*   **Architecture Judgment:** Isolated the Historian in Level 3 to enforce unidirectional data flow, fulfilling IEC 62443 requirements for zone-to-zone restricted access.
*   **GRC Depth:** Full IEC 62443 gap analysis, threat model mapped to MITRE ATT&CK for ICS (T0800–T0890), asset inventory, risk register & BIA (12 scenarios), IR playbook, and STIG-style hardening guides.
*   **Stack:** OpenPLC, Scada-LTS, Iptables (Zone Firewall), InfluxDB, Grafana, Docker Compose.

### [Cloud Telemetry Lake](https://github.com/LiamCarPer/cloud-telemetry-lake)
**The Problem:** Ingesting OT telemetry into AWS is often rigid and expensive while respecting segmentation boundaries.
**The Solution:** A serverless, event-driven pipeline that ingests, parses, and archives OT security events in real-time.
*   **Engineering Challenge:** Solved LocalStack Community constraints by implementing a **Fat-Zip dependency injection** at cold-start and a **dynamic gzip detection** layer for Fluent Bit payloads.
*   **Stack:** Terraform, AWS Lambda, DynamoDB, S3, Snappy/Parquet, Fluent Bit.

### [Log Parser Toolkit](https://github.com/LiamCarPer/log-parser-toolkit)
**The Problem:** SIEM ingestion is only as good as its parser.
**The Solution:** A memory-efficient, stateful parsing engine for unstructured logs.
*   **Technical Nuance:** Uses the **Generator pattern** to process multi-gigabyte logs with near-zero RAM overhead. Features a stateful middleware for correlating SSH brute force and web scanning across time windows.

---

## 🧰 Systems, Coding & Applied AI

The detection work only holds if the tooling underneath it does. Alongside the OT projects I write memory-safe parsers, analyzers and ML tooling.

*   **[Rust Security Toolkit](https://github.com/LiamCarPer/rust-security-toolkit)** — Rust CLI for Solana transaction forensics, IDL-aligned account validation and instruction simulation. 56 integration tests.
*   **[Solana Audit Toolkit](https://github.com/LiamCarPer/solana-audit-toolkit)** — syn-based static analyzer for missing signer checks, missing owner constraints, discriminator collisions and CPI privilege escalation, plus a ProgramTest fuzzer. 40 tests, 3 shipped audit findings.
*   **[AetherPdM](https://github.com/LiamCarPer/AetherPdM)** — Predictive maintenance for rotating equipment: vibration DSP (FFT, envelope), PyTorch autoencoder anomaly detection that beat the sklearn baseline on real CWRU validation, MQTT streaming ingestion, and ONNX edge deployment.
*   **[GatedOps](https://github.com/LiamCarPer/GatedOps)** — Reference MLOps platform: gated train/evaluate/promote/serve with byte-exact lineage and serving-quality gates.
*   **Open source:** [CISA Malcolm](https://github.com/cisagov/Malcolm) (OT/ICS protocol visibility for Modbus TCP in the DPI pipeline), [socketioxide](https://github.com/Totodore/socketioxide) (volatile events, remote-adapter core refactor), [sqlx](https://github.com/transact-rs/sqlx) (SQLite datetime builder off a deprecated API).

---

## 🧠 Technical Arsenal

**Detection, Network & Response**
![Sigma](https://img.shields.io/badge/Sigma-2F4F4F?style=flat-square) ![pySigma](https://img.shields.io/badge/pySigma-2F4F4F?style=flat-square) ![Suricata](https://img.shields.io/badge/Suricata-FF6B6B?style=flat-square) ![Zeek](https://img.shields.io/badge/Zeek-2D2D2D?style=flat-square) ![Malcolm NDR](https://img.shields.io/badge/Malcolm%20NDR-2F4F4F?style=flat-square) ![Arkime](https://img.shields.io/badge/Arkime-008C95?style=flat-square) ![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=flat-square) ![Scapy](https://img.shields.io/badge/Scapy-FF6B6B?style=flat-square) ![Splunk](https://img.shields.io/badge/Splunk-000000?style=flat-square&logo=splunk&logoColor=white) ![Microsoft Sentinel](https://img.shields.io/badge/Microsoft%20Sentinel-0078D4?style=flat-square) ![OpenSearch](https://img.shields.io/badge/OpenSearch-005EB8?style=flat-square&logo=opensearch&logoColor=white) ![Grafana Loki](https://img.shields.io/badge/Grafana%20Loki-F46800?style=flat-square&logo=grafana&logoColor=white) ![MITRE ATT&CK for ICS](https://img.shields.io/badge/MITRE%20ATT%26CK%20for%20ICS-CC0000?style=flat-square)

**OT / ICS Security**
![IEC 62443](https://img.shields.io/badge/IEC%2062443-2F4F4F?style=flat-square) ![Purdue Model](https://img.shields.io/badge/Purdue%20Model-004466?style=flat-square) ![NIS2](https://img.shields.io/badge/NIS2-003366?style=flat-square) ![BDEW](https://img.shields.io/badge/BDEW%20White%20Paper-004466?style=flat-square)
![Modbus/TCP](https://img.shields.io/badge/Modbus%2FTCP-004466?style=flat-square) ![PROFINET](https://img.shields.io/badge/PROFINET-003366?style=flat-square) ![DNP3](https://img.shields.io/badge/DNP3-2F4F4F?style=flat-square) ![OPC UA](https://img.shields.io/badge/OPC%20UA-004466?style=flat-square) ![IEC 61850](https://img.shields.io/badge/IEC%2061850-003366?style=flat-square) ![S7comm](https://img.shields.io/badge/S7comm-003366?style=flat-square)

**Cloud & Infrastructure**
![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat-square&logo=amazonaws&logoColor=white) ![Lambda](https://img.shields.io/badge/AWS%20Lambda-FF9900?style=flat-square&logo=awslambda&logoColor=white) ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)

**Rust, Python & Systems**
![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white) ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) ![iptables](https://img.shields.io/badge/iptables-000000?style=flat-square) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square)

**Applied ML & Data**
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white) ![MLflow](https://img.shields.io/badge/MLflow-0194E2?style=flat-square&logo=mlflow&logoColor=white) ![Parquet](https://img.shields.io/badge/Parquet-50ABF1?style=flat-square) ![MQTT](https://img.shields.io/badge/MQTT-660066?style=flat-square&logo=mqtt&logoColor=white)

---

## 📈 Professional Development
*   **Certification path:** ISA/IEC 62443 Cybersecurity Fundamentals Specialist (IC32) → GICSP.
*   **Focus:** detection engineering at scale, ATT&CK for ICS coverage and adversary emulation (TRITON/Industroyer), OT network segmentation and secure remote access, and NIS2 / CRA compliance.

---

## 🤝 Let's Collaborate

My full-time focus is defending OT/ICS environments; on the side I keep building open tooling at the intersection of OT detection and applied AI. I'm open to connecting on detection research, joint adversary-emulation work, open-source collaboration and technical advisory for industrial detection challenges — as well as EU-remote and B2B / contract engagements.

[LinkedIn](https://www.linkedin.com/in/liam-carvajal-perez/) · [Email](mailto:carvajalperezliam7@gmail.com)
