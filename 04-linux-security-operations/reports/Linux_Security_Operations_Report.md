# Technical Report: Linux Security Operations, Monitoring, and Storage Management

## 1. Executive Summary
This project outlines essential Linux system administration, process monitoring, active network connection triage, and Logical Volume Manager (LVM) storage configuration. Designed around practical command-line operations, this report demonstrates the ability to inspect system health, track, monitor and kill anomalous processes, analyze active listening sockets, and manage flexible storage partitions securely.

## 2. Objective
* Monitor live system resource allocation and track process behavior using command-line utilities.
* Inspect active network connections and listening ports to verify service posture and detect unauthorized binding.
* Administer and expand storage environments safely using Logical Volume Management (LVM).
* Apply hardening practices across Linux administrative interfaces.

## 3. Toolset & Methodologies
* **Process & Performance Monitoring:** `top`, `htop` for tracking CPU, memory utilization, and active process IDs.
* **Network Socket Triage:** `ss`, `netstat` for auditing open ports, established connections, and associated service daemons.
* **Storage Administration:** LVM (Logical Volume Manager) physical volumes, volume groups, and logical volume sizing.

## 4. Execution & Operational Analysis
1. **Resource Auditing:** Utilized interactive process viewers to inspect memory footprints and CPU loads, identifying resource-heavy background tasks during system operations.
2. **Socket & Port Inspection:** Audited network listeners using socket statistics (`ss`) to verify that only authorized administrative and application ports were exposed to the network perimeter.
3. **Storage Scaling & Management:** Configured and evaluated LVM configurations to ensure storage pools can be dynamically resized and managed without disrupting active filesystems.

## 5. Security Relevance & Risk Analysis
Unmonitored background processes and unverified open ports represent significant blind spots in Linux environments. Attackers frequently leverage rogue background execution or unauthorized listening services for persistence and data exfiltration. Routine command-line inspection ensures administrators maintain full host visibility.

## 6. Lessons Learned
* Proficiency with native command-line utilities (`ss`, `htop`) allows for rapid triage during incident response without relying on heavy graphical interfaces.
* Flexible volume management (LVM) provides crucial scalability for log storage partitions in high-volume logging environments like SIEM servers.

---
*Prepared as part of practical Linux security operations and administration.*
