# Liam Carvajal
**Security Engineer | OT/ICS & Cloud Detection Engineering**

I build end-to-end security architectures for critical infrastructure. My focus is on bridging the gap between legacy industrial protocols (Modbus, S7comm) and modern cloud-native detection pipelines.

[LinkedIn](https://www.linkedin.com/in/liam-carvajal-perez/) · [Email](mailto:carvajalperezliam7@gmail.com) · Based in Spain (Open to Remote Europe/USA)

---

## 🏗️ Integrated OT, Cloud & Analytics Ecosystem
I don't just build security tools; I engineer the data pipelines required to ingest, structure, and analyze high-volume industrial telemetry for advanced heuristics and ML modeling.

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

## 🛠️ Featured Projects

### [Cloud Telemetry Lake](https://github.com/LiamCarPer/cloud-telemetry-lake)
**The Problem:** Ingesting OT telemetry into AWS is often rigid and expensive.
**The Solution:** A serverless, event-driven pipeline that ingests, parses, and archives OT security events in real-time.
*   **Engineering Challenge:** Solved LocalStack Community constraints by implementing a **Fat-Zip dependency injection** at cold-start and a **dynamic gzip detection** layer for Fluent Bit payloads.
*   **Stack:** Terraform, AWS Lambda, DynamoDB, S3, Snappy/Parquet, Fluent Bit.

### [OT-NDR-Malcolm-Pipeline](https://github.com/LiamCarPer/OT-NDR-Malcolm-Pipeline)
**The Problem:** Commercial NDR (Nozomi/Claroty) is cost-prohibitive for many facilities.
**The Solution:** A production-grade NDR pipeline using CISA Malcolm, Arkime, and Suricata, enriched by a custom **Python SOAR layer**.
*   **Impact:** Implemented automated **DPI profiling** of Modbus function codes to identify unauthorized register manipulation before it hits the SIEM.
*   **Stack:** CISA Malcolm, Arkime, Suricata, Python (Scapy/Tshark).

### [OT-Security-Lab](https://github.com/LiamCarPer/OT-Security-Lab)
**The Problem:** You can't test attacks on live water treatment plants.
**The Solution:** A 5-zone Docker-based simulation of a water filtration facility mapped to the **Purdue Model** and **IEC 62443**.
*   **Engineering Judgment:** Isolated the Historian in Level 3 to enforce unidirectional data flow, fulfilling IEC 62443 requirements for zone-to-zone restricted access.
*   **Stack:** OpenPLC, Scada-LTS, Iptables (Zone Firewall), InfluxDB, Grafana.

### [Log Parser Toolkit](https://github.com/LiamCarPer/log-parser-toolkit)
**The Problem:** SIEM ingestion is only as good as its parser.
**The Solution:** A memory-efficient, stateful parsing engine for unstructured logs.
*   **Technical Nuance:** Uses the **Generator pattern** to process multi-gigabyte logs with near-zero RAM overhead. Features a stateful middleware for correlating SSH brute force and web scanning across time windows.

---

## 🛡️ Security Philosophy
*   **Availability is Paramount:** In OT, a False Positive that triggers a block can be more dangerous than the attack itself. I focus on high-fidelity, physics-aware detection.
*   **Threat-Informed Defense:** Every detection rule I write is mapped to **MITRE ATT&CK for ICS** (T0831, T0846, T0886) to ensure coverage of actual adversary TTPs.
*   **Evidence over Opinions:** I value raw PCAPs, verified attack logs, and NIST-aligned incident reports over "box-ticking" compliance.

---

## 🧠 Applied AI & Analytical Philosophy

*   **Data Quality is Paramount:** I focus heavily on the data engineering lifecycle. A predictive model in OT is useless without low-latency, highly structured telemetry.
*   **Physics-Aware Modeling:** False positives in ICS cost downtime. I emphasize high-fidelity feature engineering (e.g., mapping TTPs to MITRE ATT&CK for ICS) to ensure models understand actual industrial context, not just statistical noise.
*   **Research & Application:** Continuously researching the intersection of Deep Learning and Cybersecurity, including time-series anomaly detection and integrating LLMs (RAG) for automated incident response contextualization.

---

## 🧰 Technical Arsenal

**AI/ML & Data Engineering**
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white) ![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Pytest](https://img.shields.io/badge/Pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white) ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white) ![Parquet](https://img.shields.io/badge/Parquet-50ABF1?style=flat-square) ![LLM](https://img.shields.io/badge/LLM-FF6F00?style=flat-square) ![Time Series](https://img.shields.io/badge/Time%20Series-007396?style=flat-square)

**Cloud & Infrastructure**
![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat-square&logo=amazonaws&logoColor=white) ![Lambda](https://img.shields.io/badge/AWS%20Lambda-FF9900?style=flat-square&logo=awslambda&logoColor=white) ![S3](https://img.shields.io/badge/S3-569A31?style=flat-square&logo=amazons3&logoColor=white) ![DynamoDB](https://img.shields.io/badge/DynamoDB-4053D6?style=flat-square&logo=amazondynamodb&logoColor=white)
![Athena](https://img.shields.io/badge/Athena-FF9900?style=flat-square) ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![LocalStack](https://img.shields.io/badge/LocalStack-51BBFE?style=flat-square)

**OT Security**
![Malcolm NDR](https://img.shields.io/badge/Malcolm%20NDR-2F4F4F?style=flat-square) ![Zeek](https://img.shields.io/badge/Zeek-2D2D2D?style=flat-square) ![Scapy](https://img.shields.io/badge/Scapy-FF6B6B?style=flat-square) ![Modbus/TCP](https://img.shields.io/badge/Modbus%2FTCP-004466?style=flat-square)
![S7comm](https://img.shields.io/badge/S7comm-003366?style=flat-square) ![Syslog](https://img.shields.io/badge/Syslog-FFD700?style=flat-square)

---

## 📈 Professional Development
*   **Aligning with Industry Standards:** Actively hardening expertise via **GICSP** (Global Industrial Cyber Security Professional), **BTL1**, and **Security+**.
*   **Focus:** Advancing my knowledge in Cloud-Native SIEM (Sentinel/Chronicle) and ICS Adversary Emulation (TRITON/Industroyer).

---

## 🤝 Let's Collaborate

While my full-time focus is defending critical OT architectures, I spend my evenings and weekends immersed in the applied AI/ML community.

I am highly active in the broader engineering space and am always open to connecting regarding joint research initiatives, open-source collaborations, and technical advisory on data engineering and predictive modeling challenges. Whether it's architecting a robust data pipeline or exploring models for anomaly detection, feel free to reach out!
