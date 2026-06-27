# 🔐 SSH Log Analysis Using Splunk SIEM

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=Splunk&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Security](https://img.shields.io/badge/Security-SSH_SIEM-red?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

## 📖 Description

A comprehensive Splunk SIEM project for analyzing SSH (Secure Shell) log files
to detect security threats, monitor user behavior, identify brute force attacks,
and respond to unauthorized access attempts. This project provides production-ready
configurations, custom dashboards, and automated alert rules for SSH security monitoring.

---

## 🎯 What This Project Does

| Feature | Description |
|---------|-------------|
| 📊 SSH Activity Dashboard | Real-time overview of all SSH events |
| 🚨 Brute Force Detection | Detect IPs with multiple failed logins |
| 🌍 Geo-location Mapping | Map SSH connections by source location |
| 👤 User Behavior Analysis | Track user login patterns and anomalies |
| ⚠️ Automated Alerts | Email/Slack alerts for suspicious activity |
| 📈 Trend Analysis | Historical SSH activity trends |
| 🔍 Failed Login Analysis | Deep-dive into authentication failures |
| 🛡️ Threat Intelligence | Cross-reference IPs with threat feeds |

---

## 🚀 Quick Start

### Option 1: Docker (Recommended)
\`\`\`bash
git clone https://github.com/YOUR_USERNAME/ssh-splunk-analysis.git
cd ssh-splunk-analysis
python3 scripts/generate_ssh_logs.py
cd docker && docker-compose up -d
\`\`\`

### Option 2: Existing Splunk
\`\`\`bash
git clone https://github.com/YOUR_USERNAME/ssh-splunk-analysis.git
cd ssh-splunk-analysis
python3 scripts/generate_ssh_logs.py
python3 scripts/upload_to_splunk.py --host localhost --token YOUR_TOKEN
\`\`\`

---

## 📊 Dashboard Preview

- **SSH Overview** → Total events, failed/successful logins, top users
- **Threat Detection** → Brute force IPs, geo-map, anomaly timeline
- **User Behavior** → Session durations, off-hours logins, root access

---

## 📋 Prerequisites

- Splunk Enterprise 9.x (or Docker)
- Python 3.8+
- pip packages: `requests`, `faker`

---

## 📁 Project Structure

\`\`\`
ssh-splunk-analysis/
├── sample-logs/          # Sample SSH log files
├── scripts/              # Python automation scripts
├── splunk-configs/       # Splunk configuration files
├── dashboards/           # XML dashboard definitions
├── alerts/               # Alert configurations
├── searches/             # SPL query reference
└── docker/               # Docker deployment files
\`\`\`

---

## 🔍 Key SPL Searches

\`\`\`spl
# Brute Force Detection
index=ssh_logs sourcetype=linux_secure "Failed password"
| stats count by src_ip
| where count > 10
| sort -count

# Top Failed Users
index=ssh_logs sourcetype=linux_secure "Failed password"
| stats count by user
| sort -count | head 10

# Successful Logins Timeline
index=ssh_logs sourcetype=linux_secure "Accepted password"
| timechart span=1h count
\`\`\`

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first.

## 📄 License

MIT License - see [LICENSE](LICENSE) file.
