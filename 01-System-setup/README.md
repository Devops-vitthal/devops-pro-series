# 🚀 DevOps Lab Setup Guide – `devops-pro-series`

Welcome to the DevOps Pro Series Lab! This guide helps you set up a local development environment using **VirtualBox**, **Ubuntu**, and essential DevOps tools like **GitHub**, **Jenkins**, and **Minikube**.

---

## 🧰 Prerequisites

- System with **8GB RAM**, **100GB free disk space**
- **VT-x/AMD-V** enabled in BIOS (required for virtualization)
- Internet connection
- Admin rights on your system

---

## 🪟 Step 1: Install VirtualBox

### 🔗 Download & Install

1. Visit 👉 [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
2. Download VirtualBox for your OS (Windows/Linux/Mac)
3. Run the installer and complete the installation

---

## 🐧 Step 2: Create Ubuntu VM with Fullscreen Support

### 🔗 Download Ubuntu ISO

Download Ubuntu Server ISO from:  
👉 [https://releases.ubuntu.com/](https://releases.ubuntu.com/)

Recommended version: `Ubuntu Server 22.04 LTS`

---

### ⚙️ Create a New Virtual Machine in VirtualBox

- Open VirtualBox > Click **New**
- Name: `Ubuntu-DevOps`
- Type: `Linux`
- Version: `Ubuntu (64-bit)`
- Memory: `4096 MB` or more
- Disk: `Create a virtual hard disk now` → `VDI` → `Dynamically allocated` → `40 GB`+

---

### 💾 Install Ubuntu on the VM

- Mount the ISO and start the VM
- Proceed with Ubuntu installation (choose minimal install or full)
- Create a username/password (e.g., `devops` / `devops@123`)
- Enable **OpenSSH** if prompted

---

### 🖥️ Enable Fullscreen Resolution (Install Guest Additions)

To enable full screen and auto-resize:

#### Step 1: Update System and Install Build Tools

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install build-essential dkms linux-headers-$(uname -r) -y
````

#### Step 2: Insert Guest Additions CD

In VirtualBox window menu → **Devices > Insert Guest Additions CD image...**

#### Step 3: Mount & Install Guest Additions

```bash
cd /media/$USER/VBox_GAs_*
sudo ./VBoxLinuxAdditions.run
```

#### Step 4: Reboot VM

```bash
sudo reboot
```

#### Step 5: Enable Fullscreen

* Go to **View > Fullscreen Mode** in VirtualBox (or press `Host + F`)
* If needed, adjust resolution in Ubuntu: **Settings > Display**

---

## 🐙 Step 3: Install Git & Configure GitHub

### 🧩 Install Snap (if not already installed)

```bash
sudo apt update && sudo apt install snapd -y
sudo systemctl enable --now snapd.socket
```

Reboot your VM or log out and back in.

---

### ✅ Install Git via Snap

```bash
sudo snap install git --classic
```

---

### 🔗 Set Up Git Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

## 🔧 Step 4: Install Jenkins

### 🛠️ Install curl (if not already installed)

```bash
sudo apt update
sudo apt install curl -y
```

---

### 🌐 Install Chromium Browser (to access Jenkins GUI inside VM)

```bash
sudo snap install chromium
```

After installation, launch it via:

```bash
chromium-browser
```

---

### ☕ Install Java via Snap (required for Jenkins)

```bash
sudo snap install openjdk
```

---

### 🔧 Install Jenkins via Snap

```bash
sudo snap install jenkins --classic
```

Start Jenkins (if not auto-started):

```bash
sudo systemctl start snap.jenkins.daemon
sudo systemctl enable snap.jenkins.daemon
```

---

### 🔑 Access Jenkins

* Open Chromium browser: `http://localhost:8080`
* Get admin password:

```bash
sudo cat /var/snap/jenkins/common/secrets/initialAdminPassword
```

> 📌 **Note:** Jenkins via Snap runs in a confined environment. For Docker integrations, consider using the `apt` version if needed.

---

## ☸️ Step 5: Install Minikube (Kubernetes Cluster)

### 🧰 Install Required Tools

```bash
sudo apt install curl wget apt-transport-https -y
```

---

### 🐳 Install Docker (for Minikube driver)

```bash
sudo apt install docker.io -y
sudo usermod -aG docker $USER
newgrp docker
```

---

### 🧪 Install kubectl

```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | \
  sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update
sudo apt install -y kubectl
```

---

### 📦 Install Minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

---

### 🚀 Start Minikube

```bash
minikube start --driver=docker
```

---

### ✅ Verify Kubernetes Node

```bash
kubectl get nodes
```

---

## ✅ Final Checklist

| Task                                       | Status |
| ------------------------------------------ | ------ |
| VirtualBox Installed                       | ✅      |
| Ubuntu VM Created                          | ✅      |
| Fullscreen Enabled                         | ✅      |
| Git Installed & GitHub Connected           | ✅      |
| Jenkins Running on `http://localhost:8080` | ✅      |
| Minikube Cluster Running                   | ✅      |

---

## 🙋 Need Help?

Raise an issue here 👉 [https://github.com/TechGuru-DrVitthalKale/devops-pro-series/issues](https://github.com/TechGuru-DrVitthalKale/devops-pro-series/issues)

---

Happy Learning!
**\~ Dr. Vitthal Kale (TechGuru)**
📺 YouTube: [https://www.youtube.com/@TechGuru\_Dr.VitthalKale](https://www.youtube.com/@TechGuru_Dr.VitthalKale)
