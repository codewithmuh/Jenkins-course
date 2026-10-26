# 🚀 Jenkins CI/CD Mastery Course & Hands-On Guide

<p align="center">
  <a href="https://github.com/codewithmuh/Jenkins-course/releases"><img src="https://img.shields.io/github/v/release/codewithmuh/Jenkins-course?color=blue&label=version&style=flat-square" alt="GitHub Release"></a>
  <a href="https://github.com/codewithmuh/Jenkins-course/stargazers"><img src="https://img.shields.io/github/stars/codewithmuh/Jenkins-course?style=flat-square" alt="Stars"></a>
  <a href="https://github.com/codewithmuh/Jenkins-course/network/members"><img src="https://img.shields.io/github/forks/codewithmuh/Jenkins-course?style=flat-square" alt="Forks"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green.svg?style=flat-square" alt="License: MIT"></a>
  <a href="https://youtube.com/@codewithmuh"><img src="https://img.shields.io/badge/YouTube-%40codewithmuh-FF0000?style=flat-square&logo=youtube&logoColor=white" alt="YouTube"></a>
  <br>
  <img src="https://img.shields.io/badge/CI%2FCD-Jenkins%20LTS-D24939?style=flat-square&logo=jenkins&logoColor=white" alt="Jenkins LTS">
  <img src="https://img.shields.io/badge/Deployment-Docker%20%7C%20EC2-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/OS-Ubuntu%20Linux-E95420?style=flat-square&logo=ubuntu&logoColor=white" alt="Ubuntu">
  <img src="https://img.shields.io/badge/Cloud-AWS-FF9900?style=flat-square&logo=amazon-aws&logoColor=white" alt="AWS">
</p>

## Overview

Welcome to the **Complete Jenkins CI/CD Course & Hands-On Automation Guide**! This repository is designed to take developers, DevOps engineers, and system administrators from zero to building production-ready automated deployment pipelines using Jenkins.

Whether deploying Jenkins on a single laptop using Docker or setting up distributed Jenkins agents on AWS EC2, this course covers all real-world scenarios.

---

## 🗺️ Course Curriculum & Roadmap

```mermaid
flowchart LR
    M1["1. CI/CD & Jenkins Architecture"] --> M2["2. Installation<br/>(Docker & Linux EC2)"]
    M2 --> M3["3. Declarative Pipelines<br/>(Jenkinsfile Syntax)"]
    M3 --> M4["4. Distributed Agents<br/>(Master-Worker Nodes)"]
    M4 --> M5["5. Security & Credentials<br/>(Secrets, RBAC, Webhooks)"]
    M5 --> M6["6. End-to-End Projects<br/>(Docker, ECR, K8s)"]
```

---

## 📚 Course Modules

| Section | Focus | Description |
|---|---|---|
| **01 — Introduction** | Fundamentals | Understanding Continuous Integration & Continuous Delivery, Jenkins vs GitHub Actions. |
| **02 — Installation** | Deployment | Docker-based run, Docker Compose orchestration, and native Ubuntu/AWS EC2 installation. |
| **03 — Declarative Pipelines** | Pipelines | `Jenkinsfile` syntax, stages, steps, post-actions, environment variables, and parameters. |
| **04 — Node & Agent Setup** | Scaling | Master-to-agent architecture, SSH build agents, and dynamic cloud agents. |
| **05 — Security & Plugins** | Governance | Credentials management, GitHub webhooks, role-based access control (RBAC), and SSL. |
| **06 — Production Projects** | Real-World | Building Docker containers, running security scans (Trivy), and automated cloud rollouts. |

---

## 🛠️ Quick Installation (Docker)

To spin up a local Jenkins instance with persistent storage:

```bash
docker volume create jenkins_home

docker run -d --name jenkins \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins/jenkins:lts
```

Retrieve your initial administrative unlock key:
```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```
Open **[http://localhost:8080](http://localhost:8080)** in your browser and complete the initial setup wizard.

For complete Docker Compose and native EC2 instructions, see [`section02-installing-jenkins/instructions.md`](section02-installing-jenkins/instructions.md).

---

## 📄 License
This project is open-source under the [MIT License](LICENSE).
