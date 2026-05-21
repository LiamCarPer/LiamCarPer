# Liam Carvajal
**Security Engineer | OT/ICS & Cloud Detection Engineering**

I build end-to-end security architectures for critical infrastructure. My focus is on bridging the gap between legacy industrial protocols (Modbus, S7comm) and modern cloud-native detection pipelines.

[LinkedIn](https://www.linkedin.com/in/liam-carvajal-perez/) · [Email](mailto:carvajalperezliam7@gmail.com) · Based in Spain (Open to Remote Europe)

---

## 🏗️ Integrated OT/Cloud Security Ecosystem
I don't just build tools; I build entire environments to test how they fail. My work spans from the field device (Level 0) to the Cloud SIEM (Level 5).

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

## 🧰 Technical Arsenal
*   **OT Security:** Suricata (Custom Rules), Malcolm NDR, Zeek, Scapy, Modbus/TCP, S7comm, IEC 62443 mapping.
*   **Cloud (AWS):** Lambda (Serverless), S3 (Data Lake), DynamoDB, SNS/SQS, Athena, Glue.
*   **Engineering:** Python (Boto3, Pandas, Pytest), Terraform, Docker/Compose, LocalStack.
*   **Detection:** Syslog, Web, & Windows Event parsing, Stateful correlation, GeoIP/Threat-Intel enrichment.

---

## 📈 Professional Development
*   **Aligning with Industry Standards:** Actively hardening expertise via **GICSP** (Global Industrial Cyber Security Professional), **BTL1**, and **Security+**.
*   **Focus:** Advancing my knowledge in Cloud-Native SIEM (Sentinel/Chronicle) and ICS Adversary Emulation (TRITON/Industroyer).

---

## 🚀 Let's Secure Something
I am looking for **Detection Engineering** or **SOC Analyst** roles where I can apply my "Purdue-to-Cloud" mindset to protect critical infrastructure.
