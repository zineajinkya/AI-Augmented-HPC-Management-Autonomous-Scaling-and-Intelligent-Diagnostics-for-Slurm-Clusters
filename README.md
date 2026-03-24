# AI-Augmented HPC Management System

<div align="center">

**Autonomous Scaling and Intelligent Diagnostics for Slurm Clusters**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Slurm](https://img.shields.io/badge/Slurm-Workload%20Manager-green.svg)](https://slurm.schedmd.com/)
[![AWS](https://img.shields.io/badge/AWS-Cloud%20Integration-orange.svg)](https://aws.amazon.com/)
[![Ansible](https://img.shields.io/badge/Ansible-Automation-red.svg)](https://www.ansible.com/)

*A C-DAC ACTS Project*

</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [System Components](#system-components)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Team](#team)
- [Future Scope](#future-scope)
- [License](#license)

---

##  Overview

This project introduces a **self-governing HPC management framework** that combines AI-driven diagnostics with automated cloud scalability. By integrating the **Gemini API** with **Slurm Workload Manager**, we've developed an intelligent system that autonomously:

- 🔍 Perceives cluster states in real-time
- 🧠 Diagnoses root causes of failures using AI
- ⚡ Executes remedial actions automatically
- ☁️ Scales resources dynamically with AWS cloud bursting

### Problem Statement

Traditional HPC clusters suffer from:
- Static resource allocation
- Manual troubleshooting overhead
- Long job queue wait times
- Reactive infrastructure scaling

### Solution

An intelligent, multi-agent AI system that transforms HPC administration from **reactive** to **proactive** and **autonomous**.

---

##  Key Features

### 🤖 AI-Powered Diagnostics
- Real-time root cause analysis using **Gemini 2.0 Flash**
- Converts cryptic error messages into plain English
- Provides actionable remediation steps
- Learns from historical failure patterns

###  Autonomous Cloud Bursting
- Dynamic provisioning of AWS EC2 instances
- Seamless integration with existing Slurm cluster
- Zero-touch automation via Ansible
- Cost-optimized scaling with automatic cleanup

###  Multi-Agent Architecture
Four specialized agents work in concert:
1. **Agent 1 (Detector)**: High-frequency job queue monitoring
2. **Agent 2 (Scaling)**: Cloud resource provisioning
3. **Agent 3 (Diagnostic)**: AI-powered log analysis
4. **Agent 4 (Monitor)**: Resource cleanup and optimization

###  Enterprise-Grade Infrastructure
- **LDAP** centralized authentication
- **NFS** shared filesystems with LVM elastic management
- **Munge** authentication for secure node communication
- **Tailscale** zero-config VPN mesh networking
- **DNS & NTP** for stable cluster operations

---

## 🏛️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Users & Jobs                         │
└───────────────────┬─────────────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────────────┐
│              SLURM Scheduler (Master)                   │
│  ┌─────────────────────────────────────────────────┐    │
│  │         AI Management Layer                     │    │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐         │    │
│  │  │ Agent 1  │ │ Agent 2  │ │ Agent 3  │         │    │
│  │  │ Detector │ │ Scaling  │ │Diagnostic│         │    │
│  │  └──────────┘ └──────────┘ └──────────┘         │    │
│  │  ┌──────────┐                                   │    │
│  │  │ Agent 4  │      Gemini API Integration       │    │
│  │  │ Monitor  │                                   │    │
│  │  └──────────┘                                   │    │
│  └─────────────────────────────────────────────────┘    │
└───────────┬─────────────────────┬───────────────────────┘
            │                     │
┌───────────▼─────────┐  ┌────────▼──────────────────────┐
│  On-Premise Nodes   │  │   AWS Cloud Nodes             │
│  ┌────────────────┐ │  │  ┌─────────────────────────┐  │
│  │ Compute 1, 2, 3│ │  │  │  Auto-Provisioned       │  │
│  │                │ │  │  │  via Ansible            │  │
│  │ LDAP • NFS     │ │  │  │                         │  │
│  │ Munge • Slurmd │ │  │  │  Tailscale VPN          │  │
│  └────────────────┘ │  │  └─────────────────────────┘  │
└─────────────────────┘  └───────────────────────────────┘
```

---

##  System Components

### Agent 1: Job Detector
- Monitors Slurm queue every 5 seconds
- Detects job failures (FAILED, TIMEOUT, NODE_FAIL, etc.)
- Identifies resource constraints
- Triggers cloud burst when needed
- **User authorization required** for AWS provisioning

### Agent 2: AWS Scaling Manager
- Launches EC2 instances (t3.micro by default)
- Configures Tailscale VPN for secure connectivity
- Runs Ansible playbooks for node provisioning
- Registers nodes with Slurm cluster
- Manages up to 2 concurrent cloud nodes

### Agent 3: Diagnostic Engine
- AI-powered log analysis using Gemini API
- Provides structured diagnostics: **ERROR → WHY → FIX**
- Handles hardware limit violations
- Processes held jobs and configuration errors
- Batch processes multiple failures

### Agent 4: Resource Monitor
- Tracks active job count
- Implements idle detection (4 polling cycles)
- Triggers scale-down when cluster is idle
- Prevents unnecessary AWS costs

---

##  Prerequisites

### Hardware Requirements
- **Login Node**: 8+ cores, 16-32GB RAM, SSD
- **Master Node**: 4-8 cores, 8-16GB RAM
- **Compute Nodes**: 8+ cores, 16GB+ RAM per node
- **Storage Node**: High-capacity disks with RAID support
- **Network**: 1Gbps+ managed switch

### Software Requirements
```
Operating System: Ubuntu 24.04 LTS
Cluster Management: Slurm Workload Manager
Authentication: LDAP, Munge
Storage: NFS, LVM
Automation: Ansible, Boto3
AI/Monitoring: Python 3.x, Gemini API
Cloud: AWS CLI, IAM roles
Networking: Tailscale VPN
```

---

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/zineajinkya/AI-Augmented-HPC-Management-Autonomous-Scaling-and-Intelligent-Diagnostics-for-Slurm-Clusters.git
cd AI-Augmented-HPC-Management-Autonomous-Scaling-and-Intelligent-Diagnostics-for-Slurm-Clusters
```

### 2. Set Up Virtual Environment
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 3. Configure Base Infrastructure
```bash
# Install and configure DNS, NTP, LDAP, NFS, Munge
# See documentation in docs/infrastructure-setup.md
```

### 4. Install Slurm
```bash
sudo apt install slurm-wlm slurmd slurmctld
# Copy slurm.conf to /etc/slurm/
```

### 5. Set Up Tailscale
```bash
curl -fsSL https://tailscale.com/install.sh | sh
tailscale up --authkey=<your-auth-key>
```

---

##  Configuration

### 1. Environment Variables
Create a `.env` file:
```bash
GEMINI_API_KEY=your_gemini_api_key
TS_AUTH_KEY=your_tailscale_auth_key
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
```

### 2. Cluster Configuration
Edit `cluster_config.py`:
```python
SYSTEM_SETTINGS = {
    "STATE_FILE": "/path/to/cluster_state.json",
    "GEMINI_API_KEY": os.getenv("GEMINI_API_KEY")
}

LOCAL_NODE_SPECS = {
    "CPU_PER_NODE": 16,
    "MEM_PER_NODE_GB": 40,
    "MAX_LOCAL_NODES": 3
}

CLOUD_PROVISIONING = {
    "REGION": "us-east-1",
    "AMI_ID": "ami-0e2c8caa4b6378d8c",
    "INSTANCE_TYPE": "t3.micro"
}
```

### 3. AWS Configuration
```bash
aws configure
# Enter your AWS credentials
```

### 4. Ansible Setup
Update `provision_aws_slurm_worker.yml` with your:
- Master node IP
- NFS server IP
- Munge key path
- Slurm configuration

---

##  Usage

### Starting the System
```bash
cd /path/to/mas-hpc
./start_system.sh
```

This launches all four agents in the background and starts the admin dashboard.

### Submitting Jobs
```bash
# Submit a job to the local partition
sbatch job_script.sh

# Submit a job that may trigger cloud bursting
sbatch --partition=cloud cloud_job.sh
```

### Monitoring
```bash
# Check job queue
squeue

# View cluster state
cat cluster_state.json

# Monitor agent logs
tail -f logs/*.log
```

### Manual Cloud Burst Testing
```bash
# Test AWS connectivity
python test_aws.py

# Manually trigger cloud deployment
sbatch cloud_burst.sh
```



##  Team

**Centre for Development of Advanced Computing (C-DAC)**  
**ACTS, Pune**

**Project Guide:** Mr. Ashutosh Das

**Team Members:**
- Ajinkya Zine    (PRN: 250840127002)
- Anjali Hongekar (PRN: 250840127003)
- Harshada Rathor (PRN: 250840127008)
- Mohit Pawaskar  (PRN: 250840127012)
- Soham Bhamare   (PRN: 250840127021)

---

##  Future Scope

- [ ] Integration of advanced AI/ML models for predictive failure detection
- [ ] Multi-cloud support (Azure, GCP)
- [ ] Fully self-healing automation
- [ ] Container support (Singularity, Docker, Kubernetes)
- [ ] Cost-aware and energy-efficient scheduling
- [ ] Enhanced security with AI-driven anomaly detection
- [ ] Scalability for enterprise and national-level HPC deployments

---

##  License

This project was developed as part of the Post Graduate Diploma in High Performance Computing System Administration at C-DAC ACTS, Pune.

---

##  Acknowledgments

We express our gratitude to:
- **Mr. Ashutosh Das** for his guidance and support
- **Mr. Gaur Sunder**, HOD ACTS
- **Mrs. Risha P.R.**, Program Head
- **Ms. Divya Patel**, Course Coordinator
- **C-DAC ACTS, Pune** for providing infrastructure and resources

---

<div align="center">

*Transforming HPC Administration from Reactive to Autonomous*

</div>
