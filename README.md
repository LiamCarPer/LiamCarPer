# Liam Carvajal

**OT/ICS Cybersecurity Engineer | Network Segmentation · IEC 62443 · Detection Engineering**

I design and defend security architectures for live industrial environments. My focus is the layer most security people skip: OT network architecture — zones and conduits, IT/OT segmentation and DMZ design, secure remote access, and detection that survives real plant constraints. I work across legacy industrial protocols (Modbus, PROFINET, DNP3, OPC UA, IEC 61850), OT NDR/SOC pipelines, and the brownfield reality of changing architecture in a running plant.

Currently **OT SOC Analyst @ Rockwell Automation** — industrial detection and incident response in production OT environments.

[LinkedIn](https://www.linkedin.com/in/liam-carvajal-perez/) · [Email](mailto:carvajalperezliam7@gmail.com) · Spain · **Open to EU remote & B2B / contract engagements**

---

## 🏗️ How an OT security architecture actually holds together

I don't stop at the standard or the slide deck. I build the pipelines that prove the design works — from edge protocol inspection to the SIEM, and from the cloud telemetry lake to the incident report.

```mermaid
graph TD
    subgraph "On-Prem / Edge (OT-Security-Lab)"
        PLC[PLCs / HMI] -->|Modbus/TCP| GW[OT Gateway / NDR]
        GW -->|Suricata/Zeek| ML[Malcolm NDR Pipeline]
    end

    subgraph "Cloud Telemetry Lake (AWS/LocalStack)"
        ML -->|Fluent Bit| S3[S3 Raw Storage]
        S3 -->|SQS/Lambda| LP[Log Parser Toolkit]
        LP -->|Detections| DDB[(DynamoDB)]
        DDB -->|Streams| IR[Automated NIST Reports]
    end

    style GW fill:#f96,stroke:#333
    style LP fill:#ff9,stroke:#333
    style IR fill:#dfd,stroke:#333
```

---

## 🛡️ OT / ICS Security Architecture — Featured Work

### [OT-Security-Lab](https://github.com/LiamCarPer/OT-Security-Lab)
**The Problem:** You can't test attacks on live water treatment plants.
**The Solution:** A 5-zone Docker-based simulation of a water filtration facility mapped to the **Purdue Model** and **IEC 62443**, with every inter-zone conduit enforced through a dedicated iptables gateway.
*   **Architecture Judgment:** Isolated the Historian in Level 3 to enforce unidirectional data flow, fulfilling IEC 62443 requirements for zone-to-zone restricted access.
*   **GRC Depth:** Full IEC 62443 gap analysis, threat model mapped to MITRE ATT&CK for ICS (T0800–T0890), asset inventory, risk register & BIA (12 scenarios), IR playbook, and STIG-style hardening guides.
*   **Stack:** OpenPLC, Scada-LTS, Iptables (Zone Firewall), InfluxDB, Grafana, Docker Compose.

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

## 🦀 Rust & Systems Security Engineering

Where the OT work needs to go below the abstraction level, I build the tooling — memory-safe parsers and analyzers for industrial and on-chain environments.

### [Rust Security Toolkit](https://github.com/LiamCarPer/rust-security-toolkit)
A Rust CLI for Solana transaction forensics, IDL-aligned account validation, and instruction simulation — enabling rapid triage of suspicious on-chain activity.
*   **Stack:** Rust, Solana SDK, Anchor, Clap, Tokio. 56 integration tests.

### [Solana Audit Toolkit](https://github.com/LiamCarPer/solana-audit-toolkit)
A Rust-based static analyzer (syn) that detects missing signer checks, missing owner constraints, discriminator collisions, and CPI privilege escalation — plus a ProgramTest fuzzer with auto-generated invariants.
*   **Stack:** Rust, syn, Anchor, SPL Token, ProgramTest, Bankrun, SARIF. 40 tests, 3 shipped audit findings.

### Open Source Contributions
*   **[CISA Malcolm](https://github.com/cisagov/Malcolm)** — OT/ICS protocol visibility improvements for Modbus TCP within the DPI pipeline.
*   **[socketioxide](https://github.com/Totodore/socketioxide)** — volatile events support and remote-adapter core refactoring (merged PRs).
*   **[sqlx](https://github.com/transact-rs/sqlx)** — SQLite datetime format builder migrated off a deprecated API.

---

## 🧠 Applied AI for OT (Differentiator)

I use machine learning where it earns its place in OT — high-fidelity, physics-aware, and never at the cost of availability.

*   **[AetherPdM](https://github.com/LiamCarPer/AetherPdM)** — Predictive maintenance for rotating equipment: vibration DSP (FFT, envelope), PyTorch autoencoder anomaly detection that beat the sklearn baseline on real CWRU validation, MQTT streaming ingestion, and ONNX edge deployment.
*   **[GatedOps](https://github.com/LiamCarPer/GatedOps)** — Reference MLOps platform: gated train/evaluate/promote/serve with byte-exact lineage and serving-quality gates.

---

## 🧰 Technical Arsenal

**OT / ICS Security**
![IEC 62443](https://img.shields.io/badge/IEC%2062443-2F4F4F?style=flat-square) ![Purdue Model](https://img.shields.io/badge/Purdue%20Model-004466?style=flat-square) ![NIS2](https://img.shields.io/badge/NIS2-003366?style=flat-square) ![BDEW](https://img.shields.io/badge/BDEW%20White%20Paper-004466?style=flat-square)
![Modbus/TCP](https://img.shields.io/badge/Modbus%2FTCP-004466?style=flat-square) ![PROFINET](https://img.shields.io/badge/PROFINET-003366?style=flat-square) ![DNP3](https://img.shields.io/badge/DNP3-2F4F4F?style=flat-square) ![OPC UA](https://img.shields.io/badge/OPC%20UA-004466?style=flat-square) ![IEC 61850](https://img.shields.io/badge/IEC%2061850-003366?style=flat-square) ![S7comm](https://img.shields.io/badge/S7comm-003366?style=flat-square)

**Detection, Network & Response**
![Malcolm NDR](https://img.shields.io/badge/Malcolm%20NDR-2F4F4F?style=flat-square) ![Zeek](https://img.shields.io/badge/Zeek-2D2D2D?style=flat-square) ![Suricata](https://img.shields.io/badge/Suricata-FF6B6B?style=flat-square) ![Scapy](https://img.shields.io/badge/Scapy-FF6B6B?style=flat-square) ![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=flat-square) ![MITRE ATT&CK ICS](https://img.shields.io/badge/MITRE%20ATT%26CK%20for%20ICS-CC0000?style=flat-square)

**Cloud & Infrastructure**
![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat-square&logo=amazonaws&logoColor=white) ![Lambda](https://img.shields.io/badge/AWS%20Lambda-FF9900?style=flat-square&logo=awslambda&logoColor=white) ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)

**Rust, Python & Systems**
![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white) ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) ![iptables](https://img.shields.io/badge/iptables-000000?style=flat-square) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square)

**Applied ML & Data**
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white) ![MLflow](https://img.shields.io/badge/MLflow-0194E2?style=flat-square&logo=mlflow&logoColor=white) ![Parquet](https://img.shields.io/badge/Parquet-50ABF1?style=flat-square) ![MQTT](https://img.shields.io/badge/MQTT-660066?style=flat-square&logo=mqtt&logoColor=white)

---

## 📈 Professional Development
*   **Certification path:** ISA/IEC 62443 Cybersecurity Fundamentals Specialist (IC32) → GICSP.
*   **Focus:** OT network architecture and segmentation at scale, secure remote access and identity in OT (AD/PAM), NIS2 / CRA compliance, and ICS adversary emulation (TRITON/Industroyer).

---

## 🤝 Let's Collaborate

My full-time focus is defending OT/ICS architectures; on the side I keep building open tooling at the intersection of OT security and applied AI. I'm open to connecting on joint research, open-source collaboration, and technical advisory for industrial security, segmentation, and detection challenges — as well as EU-remote and B2B / contract engagements.

[LinkedIn](https://www.linkedin.com/in/liam-carvajal-perez/) · [Email](mailto:carvajalperezliam7@gmail.com)
