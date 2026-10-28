# Liam Carvajal

**OT Detection Engineer | Agentic AI for Security Automation**

I build OT detection that holds up in production and AI agents that SOC analysts can actually trust. My work sits at the intersection of detection engineering, industrial protocols and security automation: Sigma and Suricata content, protocol-aware telemetry, ATT&CK for ICS coverage, and agentic workflows with least privilege, tool allowlists, human approval and audit trails.

Currently **OT Detection Engineer @ Rockwell Automation**, working across OT detection, incident response and an internal AI-assisted SOC triage workflow.

Spain · EU citizen · open to EU remote, hybrid and B2B engagements

[LinkedIn](https://www.linkedin.com/in/liam-carvajal-perez/) · [Email](mailto:carvajalperezliam7@gmail.com) · [GitHub](https://github.com/LiamCarPer)

---

## What I focus on

- **OT detection engineering:** Sigma and native Suricata rules, protocol-aware deep packet inspection, MITRE ATT&CK for ICS coverage, detection quality metrics and adversary emulation.
- **OT/ICS security and response:** Purdue and IEC 62443 segmentation, Claroty and Nozomi monitoring, incident triage, threat hunting, vulnerability tracking and IR runbooks.
- **Agentic AI for security:** local-model SOC triage, RAG over playbooks, tool allowlists, read-only service accounts, human approval gates, audit logging and Splunk/Sentinel detection logic.

## Featured work

### [OT Detection Engineering](https://github.com/LiamCarPer/ot-detection-engineering)

Detection-as-code for OT: one Sigma source converted in CI into Splunk, Microsoft Sentinel, OpenSearch and Loki queries, plus native Suricata DPI for Modbus, DNP3 and OPC UA.

17 Sigma and 24 native Suricata rules, 177 tests, ATT&CK for ICS coverage of 15/97 techniques, 0.0 FPR on 50 authored benign events and 2.45 s mean MTTD.

`Sigma` `Suricata` `Rust` `Splunk` `Microsoft Sentinel` `OpenSearch` `Loki` `CI/CD`

### [ICS Agentic SOC Pipeline](https://github.com/LiamCarPer/ics-agentic-soc-pipeline)

RAG-based SOC triage that summarises alerts, retrieves playbook context and drafts NIST SP 800-61 reports with human review. Hardened prompt boundaries, tool access and audit logging.

AI threat model mapped to OWASP LLM Top 10, MITRE ATLAS and NIST AI RMF, with a 14-case AI red-team suite and poisoning/evasion experiments.

`Python` `LangChain` `ChromaDB` `FastAPI` `RAG` `Local models` `Docker`

### [OT-Security-Lab](https://github.com/LiamCarPer/OT-Security-Lab)

Five-zone water-treatment lab on the Purdue Model, with 3 OpenPLC PLCs, Scada-LTS, InfluxDB and every inter-zone conduit enforced through an iptables gateway.

Nine attack scenarios replayed through a 10-gate CI pipeline with detection evidence in Grafana/Loki. Includes IEC 62443 gap analysis, threat model, risk register and BIA, IR playbook and STIG-style hardening guides.

`OpenPLC` `Scada-LTS` `Modbus` `DNP3` `OPC UA` `iptables` `Grafana` `Loki`

### [Cloud Telemetry Lake](https://github.com/LiamCarPer/cloud-telemetry-lake)

Serverless AWS pipeline for OT and identity telemetry: S3, SQS, Lambda, DynamoDB and Parquet, with scoped IAM, KMS, Secrets Manager and TLS-only bucket policies.

Seven CloudTrail and GuardDuty identity rules covering root use, MFA-less console login, access-key creation, IAM changes and logging tampering. 78 tests across parsers and rules.

`AWS` `Terraform` `CloudTrail` `GuardDuty` `Lambda` `Parquet` `Python`

## Toolbox

**Detection:** Sigma, Suricata, Splunk, Microsoft Sentinel, Wazuh, OpenSearch, MITRE ATT&CK for ICS  
**OT/ICS:** IEC 62443, Purdue Model, Modbus, DNP3, OPC UA, S7comm, IEC 61850  
**Engineering:** Python, Rust, AWS, Terraform, Docker, Kubernetes, CI/CD

## Certifications

Claroty Implementation Engineer (IND) · Claroty Cybersecurity Analyst · Claroty Support Engineer · ISC2 CC · IEC 62443 IC32 in progress · GICSP planned

## Open to

OT detection, OT/ICS security and AI-security roles in the EU. Remote, hybrid or B2B. Based in Madrid, available to relocate for the right role.

[LinkedIn](https://www.linkedin.com/in/liam-carvajal-perez/) · [Email](mailto:carvajalperezliam7@gmail.com)
