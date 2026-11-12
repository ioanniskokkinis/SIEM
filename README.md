# Enterprise Security Simulation & SIEM Homelab

## Overview

This project is a hands-on, enterprise-grade security monitoring lab designed to simulate real-world attack scenarios and defensive operations. It focuses on building a centralized logging and detection infrastructure using a SIEM platform, enabling visibility across multiple endpoints and services.

The lab is aligned with core cybersecurity principles and maps directly to industry standards such as CompTIA Security+ domains, including threat detection, system architecture, and security operations.

---

## Objectives

* Design and deploy a centralized logging infrastructure
* Simulate real-world cyber attack scenarios
* Develop and test custom detection rules
* Gain hands-on experience with SIEM tools and log analysis
* Understand incident detection and response workflows
* Practice secure system architecture and network segmentation

---

## Architecture

The lab is hosted on a Hetzner VPS and designed with a modular architecture:

* Centralized SIEM server (Wazuh)
* Multiple Linux endpoints generating logs
* Dockerized services for isolation and scalability
* Segmented environment to simulate enterprise infrastructure

---

## Technologies Used

* Wazuh SIEM
* Docker & Docker Compose
* Ubuntu Server
* Nginx
* The Hive
* Bash scripting
* Webhooks (alerting & automation)
* Virtualization tools (VirtualBox / VMware)

---

## Environment Setup
I followed the wazuh instructions and i did perfectely.


## Network Design & Segmentation

## SIEM Configuration (Wazuh)
- **Docker conflicts**: Found two Docker daemons running at once (snap and apt) holding the same ports. Removed the snap install and standardized on one.
- **Port clashes**: Resolved conflicts on 443, 514/udp, 1514, 1515 and 55000, including remapping syslog to 5514 and clearing stale docker-proxy processes.
- Manager crash loop: Traced the restart loop through container exit codes, docker events and Wazuh’s own logs. The root cause was Filebeat failing because bind-mounted certificate files didn’t exist, so Docker had created directories in their place.
- **TLS certificates**: Regenerated the Wazuh certificates with the cert generator and fixed root-owned file permissions.
- **Indexer security**: Fixed a YAML syntax error in internal_users.yml. Learned that sed -i breaks single-file bind mounts because it replaces the inode, and that a container restart is needed to pick up the change. Initialized the OpenSearch security index manually with securityadmin.sh.
- **Admin credentials**: Rotated the indexer admin password by generating a bcrypt hash and updating the compose environment.
- **VM networking**: Diagnosed a VirtualBox VM that wouldn’t start by reading VBox.log. A serial port had been pointed at a network device name, which caused a power-up failure.

## Log Collection & Aggregation

We had an issue on that.Log were not showing up so i change the prefix

## Threat Simulation Scenarios

## Detection Rules & Alerting

## Incident Response Workflow

## Automation & Orchestration

## Monitoring & Visualization

## Security Considerations

## Challenges & Trade-offs

* Explaining and applying advanced technical concepts as a first-year student
* Balancing detection accuracy with false positives
* Managing limited resources in a virtualized environment

---

## Results & Key Findings

## Problems that i had
- Very complex project
- Not showing up everything it needs to be

## Future Improvements

## References

## License

This project is licensed under the MIT License.
