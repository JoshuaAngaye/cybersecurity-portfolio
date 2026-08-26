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
5. **Advanced Configuration:** Enabling Archive Logging (`logall` / `logall_json`) **Filebeat:** A secure log shipper that transports processed events and raw logs from the manager to the Elasticsearch/OpenSearch indexer.**Wazuh Indexer & Dashboard:** The storage database and web user interface used for data visualization, threat hunting, and index management.
6. **Administrative Credential Hardening & User Management**
To eliminate default credential vulnerabilities and secure access to the SIEM cluster, the initial auto-generated administrative password was updated to a hardened, custom passphrase.

* **Service Propagation:** Verified that internal API authentication, indexer security settings, and dashboard login sessions successfully accepted the new credentials to maintain uninterrupted management access.

### Problem Statement
By default, the Wazuh analysis engine focuses purely on high-priority security alerts (Level 3 and above) and discards routine operational data like successful logons, standard session creations, and allowed network connections to prevent storage bloat. However, comprehensive threat hunting and forensic investigations often require visibility into baseline user behaviors that standard alerts miss.

### Configuration Adjustment
To capture all raw incoming logs—including successful authentication events—archive logging was explicitly enabled within the global configuration file (`/var/ossec/etc/ossec.conf`):

<global>
  <logall>yes</logall>
  <logall_json>yes</logall_json>
</global>

## 5. Troubleshooting & Challenges
* **Resource Bottlenecks:** Initial host performance degradation was identified due to concurrent high memory utilization and heavy indexing loads.
* **Console Latency:** Transitioned from the sluggish VMware graphical console to a direct, responsive SSH session (`192.168.239.128`) for streamlined management.

## 6. Security Purpose & Operational Relevance
In a professional Security Operations Center environment (such as those observed during my internship at UNICCON), centralized log retention ensures forensic visibility across diverse infrastructures.

## 7. Limitations
* **Single-Node Topology:** Configured as an All-in-One instance; high availability, load balancing, and multi-node cluster scaling are omitted.
* **Network Isolation:** Tested within a localized virtual network rather than a live corporate perimeter.

## 8. Lessons Learned
* Automated installation scripts significantly reduce deployment friction, but understanding underlying configuration files (`/var/ossec/etc/ossec.conf`) is vital for log tuning.
* Securing transport layer security (TLS) certificates and managing internal user databases are critical initial steps post-deployment.
* High-speed internet is recommended for smooth operations.
