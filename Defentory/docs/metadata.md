# Enterprise Detection Coverage Metadata Dictionary
### For MITRE ATT&CK Mapping & Visibility Across Host, Cloud, and Hybrid Environments

---

### 1. Data Source Metadata (Core for Coverage Mapping)
| Field                  | Why It Matters                                      | Example Values                                      |
|------------------------|-----------------------------------------------------|-----------------------------------------------------|
| Data Source Name       | Human-readable identifier                           | Microsoft Defender for Endpoint, CrowdStrike Falcon, AWS CloudTrail |
| Data Source Type       | Categorizes the telemetry type                      | EDR, NDR, Cloud Logs, IAM Logs, Firewall, SIEM     |
| Platform / Environment | Indicates where the data lives                      | AWS, Azure, GCP, Windows, Linux, macOS, Kubernetes, SaaS (O365, Okta) |
| Vendor / Product       | Tracks vendor-specific gaps and capabilities        | Microsoft, Crowdstrike, Palo Alto Cortex, Splunk, SentinelOne |
| Log Type / Event Type  | Granular source of the telemetry                    | Process Creation, DNS Query, CloudTrail Management Event, Okta SystemLog |

---

### 2. MITRE ATT&CK Mapping Metadata
| Field                   | Why It Matters                                                                 |
|-------------------------|--------------------------------------------------------------------------------|
| ATT&CK Technique ID(s)  | Primary key for mapping (e.g., T1078.004, T1566.001)                            |
| ATT&CK Tactic(s)        | Enables tactic-level heatmaps and reporting                                    |
| Sub-Technique Support   | Indicates coverage of sub-techniques (Yes / No / Partial)                      |
| Detection Confidence    | Overall reliability (High / Medium / Low) based on FP rate, visibility, etc.  |
| Detection Type          | Rule methodology                                                               | Analytic, Behavioral, Anomaly, Threat Intel Match, ML-based |
| Visibility Level        | How directly the behavior is observed                                          | Direct (command line), Indirect (image load + network), None |

---

### 3. Visibility & Coverage Metadata
| Field                   | Why It Matters                                              |
|-------------------------|-------------------------------------------------------------|
| Covered Assets %        | % of endpoints/servers/cloud accounts with this source     |
| Deployment Status       | Current rollout state                                       | Deployed, Partial, Planned, Not Feasible |
| Geographic Scope        | Data residency & collection boundaries                      | Global, US-only, EU-only |
| Environment Scope       | Which environments are included                             | Prod only, Prod + Dev, All |
| Collection Frequency    | Latency of detection capability                             | Real-time, Hourly, Daily |
| Data Retention          | How long raw events are available                           | 30 days, 90 days, 1 year |

---

### 4. Host / Endpoint-Specific Metadata
| Field                        | Example Values                              |
|------------------------------|---------------------------------------------|
| OS Type & Version            | Windows 10 22H2, Ubuntu 20.04, macOS Ventura |
| Sensor/Agent Version         | CrowdStrike 6.44, Defender 10.8230          |
| Process Command Line Logging | Enabled / Disabled                          |
| Script Block Logging / AMSI  | Enabled / Disabled                          |
| EDR Coverage Tier            | Full, Basic, None                           |

---

### 5. Cloud & Hybrid-Specific Metadata
| Field                     | Example Values                                           |
|---------------------------|----------------------------------------------------------|
| Cloud Provider            | AWS, Azure, GCP, Multi-cloud                             |
| Cloud Service Coverage    | EC2, Lambda, S3, Azure VMs, AKS, GuardDuty, Defender for Cloud |
| Control Plane Logging     | CloudTrail, Azure Activity Log, GCP Admin Activity      |
| Data Plane Logging        | VPC Flow Logs, S3 Access Logs, GuardDuty Findings       |
| SaaS Applications         | Office 365, Okta, Salesforce, GitHub                    |
| Identity Provider Coverage| Azure AD, Okta, Ping, On-prem AD                        |

---

### 6. Detection Content Metadata
| Field                    | Purpose                                                  |
|--------------------------|----------------------------------------------------------|
| Rule / Analytic ID       | Unique identifier across the enterprise                  |
| Rule Name                | Human-readable name                                      |
| Rule Maturity            | Production, Beta, Deprecated                             |
| False Positive Rate      | Low / Medium / High (or numeric)                         |
| Mean Time to Detect (MTTD)| Measured or estimated detection latency                  |
| Last Tested Date         | Validates rule is still effective                        |
| Detection Logic Summary  | Short description (e.g., “Detects PowerShell downloading from pastebin”) |

---

### 7. Gaps & Recommendations Metadata
| Field                   | Use                                                         |
|-------------------------|-------------------------------------------------------------|
| Coverage Gap Reason     | Why visibility/detection is missing                         | No sensor, No logging, Cost, Technical limitation |
| Recommended Data Source | Actionable next step                                        | “Enable OSQuery fleet”, “Turn on CloudTrail data events” |
| Priority                | Business impact of the gap                                  | P0 (Critical), P1, P2, P3 |
| Effort to Implement     | Resource requirement to close the gap                       | Low / Medium / High |

---
