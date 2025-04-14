# SOC Lab: Wazuh + TheHive + Shuffle (Beginner Friendly)

This project is a hands-on, beginner-friendly lab designed to simulate a mini Security Operations Center (SOC). It integrates **Wazuh**, **TheHive**, and **Shuffle** for real-time alerting, automation, enrichment, and incident tracking.

---

## Lab Stack

| Component | Description |
|----------|-------------|
| **Wazuh** | Open-source SIEM used to monitor and analyze system logs |
| **TheHive** | Case management system for incident response |
| **Elasticsearch** | Backend log storage and search engine for Wazuh/TheHive |
| **Shuffle** | SOAR (Security Orchestration Automation and Response) platform to automate tasks |
| **Windows 10 VM** | Simulates attacks for testing (keyloggers, ransomware, etc.) |

---

## Architecture Diagram
```
+------------------+         +-------------------+
| Windows 10 (test)| -----> | Wazuh (collects)  |
+------------------+         +-------------------+
                                     |
                                     v
                            +-------------------+
                            | TheHive (tracks)  |
                            +-------------------+
                                     |
                                     v
                            +-------------------+
                            | Shuffle (alerts)  |
                            +-------------------+
                                     |
                                     v
                            +-------------------+
                            | Discord (SOC alert)|
                            +-------------------+
```

---

## Features

- [x] Wazuh agent on Windows 10 VM
- [x] Alerts sent via webhook to Shuffle
- [x] Shuffle workflows:
  - Triggered by Wazuh alerts
  - Enrich alert with VirusTotal and AbuseIPDB
  - Create a case in TheHive
  - Notify analysts via Discord
  - Add logs and debugging output
- [x] TheHive integrated with Cortex for analysis
- [x] Working dashboard access for all components
- [x] Dockerized deployment for all services

---

## What I Got Working

- Wazuh monitoring Windows 10 and simulating attacks
- Alerts flowing to Shuffle, enriched with VirusTotal and AbuseIPDB
- Cases auto-created in TheHive
- Discord messages sent for each high-priority alert
- TheHive linked with Cortex for fast analysis
- Shuffle workflows with logging and error tracking

---

## Common Problems I Solved

| Problem                            | Cause                                  | Fix                                      |
|------------------------------------|-----------------------------------------|-------------------------------------------|
| Wazuh dashboard not loading        | Port conflict, container restarting     | Checked logs, freed up ports              |
| Shuffle webhook not triggering     | `isStartNode` not checked               | Enabled `isStartNode` manually            |
| TheHive failing to start           | Missing directories, SSL config errors  | Recreated folders, used HTTP fallback     |
| Discord webhook errors             | Bad JSON formatting                     | Updated payload syntax                    |
| VirusTotal/AbuseIPDB API errors    | Missing or invalid keys                 | Added proper API keys                     |
| Bridged mode needed for traffic    | NAT blocked inter-VM communication      | Switched to bridged adapter               |

---

## What’s Next

- [x] Automatically check IPs on VirusTotal and AbuseIPDB
- [x] Add firewall rules for auto-mitigation (based on IP score)
- [x] Create a unified dashboard for visibility
- [x] Package everything into Docker containers
- [x] Automate case creation in TheHive
- [x] Connect TheHive to Cortex
- [x] Add logging and error tracing in Shuffle
- [ ] Integrate with Jira for automatic incident ticketing

---

## Network Setup

| Mode     | Purpose                                | Notes                        |
|----------|----------------------------------------|------------------------------|
| **NAT**  | Used for installing packages securely  | More secure (hidden VM)      |
| **Bridged** | Used for inter-VM communication     | Required for Wazuh/Shuffle communication |

---

## References
- [SOC-Automation-Lab by uruc](https://github.com/uruc/SOC-Automation-Lab)
- [SOAR-Flow by malwarekid](https://github.com/malwarekid/SOAR-Flow)

---

## Author
**Gabriel Reis**

Feel free to fork and improve this lab. Contributions are welcome!
