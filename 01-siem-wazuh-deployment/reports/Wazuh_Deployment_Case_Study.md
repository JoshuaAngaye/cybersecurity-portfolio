# Technical Case Study: Enterprise SIEM Deployment and Log Telemetry Pipeline (Wazuh)

## 1. Executive Summary
This project details the end-to-end deployment, configuration, and operational validation of an enterprise-grade **Wazuh Security Information and Event Management (SIEM)** stack. Deployed in an isolated Ubuntu 24.04 LTS virtualized environment, the architecture integrates the Wazuh Indexer, Manager, and Dashboard components into a unified All-in-One topology. This laboratory reproduction directly mirrors the enterprise log monitoring, alert observation, and triage workflows experienced during my cybersecurity internship at UNICCON Group of Companies in Abuja.

## 2. Objective
* Deploy and configure a functional All-in-One Wazuh SIEM server on Ubuntu 24.04 LTS.
* Establish secure administrative access and resolve environmental constraints (package dependencies, resource allocation).
* Validate component health, API connectivity, and index pattern synchronization.
* Establish a foundational architecture for subsequent endpoint telemetry ingestion and threat detection workflows.

## 3. Environment & Architecture
* **Host Operating System:** Windows 11 Pro (Hosting VMware Workstation).
* **Virtualization Platform:** VMware Workstation Pro.
* **Guest Operating System:** Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-137-generic x86_64).
* **Server IP Address:** `192.168.239.128` (Assigned via network interface `ens33`).
* **SIEM Stack:** Wazuh Version 4.14.7 (Indexer, Manager, Filebeat, Dashboard).
* **Access Protocols:** SSH (Port 22) for backend management; HTTPS (Port 443) for web UI access.

## 4. Implementation Methodology
1. **Host Preparation & Hardening:** Verified system resource availability, performed package updates, and cleared legacy installation fragments to ensure a pristine deployment base.
2. **Automated Deployment:** Executed the official Wazuh installation assistant script via root privileges (`wazuh-install.sh -a`) to provision the distributed cluster components locally.
3. **Credential Management:** Captured and secured auto-generated administrative credentials.
4. **Service Initialization & Health Verification:** Monitored systemd service startup states (`wazuh-indexer`, `wazuh-manager`, `filebeat`, `wazuh-dashboard`) and validated web application initialization through API health checks.

## 5. Troubleshooting & Challenges
* **Resource Bottlenecks:** Initial host performance degradation was identified due to concurrent high memory utilization and heavy virtual disk I/O. Remediation involved resource throttling and process management.
* **Console Latency:** Transitioned from the sluggish VMware graphical console to a direct, responsive SSH session (`joshua@192.168.239.128`), vastly accelerating command execution speed and log inspection.

## 6. Security Purpose & Operational Relevance
In a professional Security Operations Center environment (such as those observed during my internship at UNICCON), centralized log aggregation is vital for detecting adversarial behavior. This lab mirrors standard operating procedures by establishing a single pane of glass for security monitoring, bridging the gap between raw endpoint telemetry and actionable intelligence.

## 7. Limitations
* **Single-Node Topology:** Configured as an All-in-One instance; high availability, load balancing, and multi-node cluster scaling were out of scope for this localized test environment.
* **Network Isolation:** Tested within a localized virtual network rather than a live corporate perimeter.

## 8. Lessons Learned
* Automated installation scripts significantly reduce deployment friction, but understanding underlying configuration files (`/var/ossec/etc/ossec.conf`) and service dependencies is essential for troubleshooting startup stalls.
* Securing transport layer security (TLS) certificates and managing internal user databases are critical initial steps post-deployment.
* high speed internet is recommended for smooth operations.
