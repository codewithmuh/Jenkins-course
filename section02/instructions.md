# 🛠 Jenkins Installation Guide

This section covers multiple ways to install Jenkins for various environments. We'll start with a Docker-based approach (fastest), then install it on AWS EC2 using APT, and finally show a local Mac installation using Homebrew (no Docker).

---

## 🚀 Option 1: Install Jenkins Using Docker (Recommended)

### ✅ Prerequisites
- Docker installed
- Optional: Docker Compose

### 🔹 Step-by-Step (Simple `docker run`)

```bash
docker volume create jenkins_home

docker run -d --name jenkins \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins/jenkins:lts
```

### 🔹 Access Jenkins
- Go to: `http://localhost:8080`
- Unlock Jenkins:
```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

### 🔹 Follow Setup Wizard
- Install Suggested Plugins
- Create admin user

---

## 💠 Option 2: Install Jenkins Using Docker Compose

```yaml
# docker-compose.yml
version: '3.8'

services:
  jenkins:
    image: jenkins/jenkins:lts
    container_name: jenkins
    ports:
      - "8080:8080"
      - "50000:50000"
    volumes:
      - jenkins_home:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
    restart: unless-stopped

volumes:
  jenkins_home:
```

Run Jenkins with Compose:
```bash
docker-compose up -d
```

Access Jenkins on `http://localhost:8080` and follow setup wizard.

---

## 🌟 Option 3: Install Jenkins on AWS EC2 (APT Method)

### 🔹 Step-by-Step

#### 1. Launch EC2
- Ubuntu Server 22.04 LTS
- Instance Type: `t2.micro`
- Open ports: 22 (SSH), 8080 (Jenkins)

#### 2. Connect via SSH
```bash
ssh -i your-key.pem ubuntu@<EC2-PUBLIC-IP>
```

#### 3. Install Java
```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```

#### 4. Install Jenkins
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y
```

#### 5. Start Jenkins
```bash
sudo systemctl start jenkins
sudo systemctl status jenkins
```

(Optional: Enable on boot)
```bash
sudo systemctl enable jenkins
```

#### 6. Access Jenkins
- Visit: `http://<EC2-PUBLIC-IP>:8080`
- Unlock Jenkins:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

## 🍏 Option 4: Install Jenkins Locally on macOS (No Docker)

### 🔹 Step-by-Step

#### 1. Install Java via Homebrew
```bash
brew install openjdk@17
```

#### 2. Install Jenkins
```bash
brew install jenkins-lts
```

#### 3. Start Jenkins
```bash
brew services start jenkins-lts
```

#### 4. Access Jenkins
- Visit: `http://localhost:8080`
- Unlock Jenkins:
```bash
cat /Users/$(whoami)/.jenkins/secrets/initialAdminPassword
```

---

## 📅 Summary Table

| Environment           | Method           | Command / Tool Used    |
|-----------------------|------------------|-------------------------|
| Local (Quick Start)   | Docker            | `docker run`           |
| Local (Reusable)      | Docker Compose    | `docker-compose up`    |
| Cloud (AWS EC2)       | APT Install       | `systemctl`             |
| Local macOS           | Homebrew Install  | `brew services start`  |

---

Continue to the next section to configure Jenkins and set up your first CI/CD pipeline!
