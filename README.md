<p align="center">
  <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Focus-DVWA%20Setup-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Beginner--Friendly-orange?style=for-the-badge"/>
</p>

# 🧱 DVWA Setup Lab (Linux Web Security Environment)

## ⭐ Project Summary

This repository documents the complete installation and configuration of Damn Vulnerable Web Application (DVWA) on a Linux system.

The focus of this project is environment preparation only.

No penetration testing or exploitation is performed in this phase.

This lab establishes a clean, reproducible, and controlled environment suitable for future web security testing.

## 🎯 Project Goals

- Build a functional DVWA lab environment
- Configure Apache, PHP, and MariaDB correctly
- Ensure DVWA is fully operational
- Provide terminal-ready documentation for reproducibility

## 🛠️ Technology Stack

| Component | Technology |
|-----------|-----------|
| Operating System | Parrot OS (Debian-based Linux) |
| Web Server | Apache2 |
| Backend Language | PHP |
| Database | MariaDB |
| Application | Damn Vulnerable Web Application (DVWA) |

## 🧪 Lab Architecture

```
Browser
   │
Apache Web Server
   │
DVWA (PHP Application)
   │
MariaDB Database
```

## 📁 Repository Structure

```
dvwa-setup-lab/
│
├── setup/
│   └── dvwa-setup-report.md   # Step-by-step terminal commands
│
├── screenshots/          
│
└── README.md
```

## 🚀 Quick Start

⚠️ Recommended: Use an isolated VM or local lab environment

```bash
git clone https://github.com/your-username/dvwa-setup-lab.git
cd dvwa-setup-lab
```

📄 Follow the complete setup guide here:

➡️ setup/dvwa-setup-report.md

## ✅ Validation Checklist

- [ ] Apache service running without errors
- [ ] MariaDB database created and accessible
- [ ] DVWA configuration file updated
- [ ] DVWA database initialized successfully
- [ ] DVWA dashboard accessible via browser

## 🔐 Security Notes

DVWA is intentionally vulnerable

Must never be exposed to the public internet

Use NAT / Host-only networking

Intended strictly for educational purposes

## 📌 Learning Outcomes

- Linux web stack setup
- PHP application deployment
- Database configuration
- Vulnerable lab environment creation
- Professional technical documentation

## 🛣️ Roadmap

- Phase 2: Vulnerability exploitation (SQLi, XSS, Auth)
- Phase 3: Detection and monitoring
- Phase 4: Reporting and mitigation
