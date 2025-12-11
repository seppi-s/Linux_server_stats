# Server Performance Stats (Go)
A lightweight, dependency-free system monitoring CLI written in Go that runs on any Linux server.

---

## 📌 Overview
**Server Performance Stats** is a fast and portable Go application designed to display essential server metrics, including:

- CPU usage  
- Memory usage  
- Disk usage  
- Top processes by CPU and memory  
- OS information  
- Uptime & load average  
- Logged-in users  
- Failed login attempts  

The tool reads data directly from Linux system files (`/proc`) and uses standard system commands.  
This makes it extremely efficient and perfect for DevOps engineers, sysadmins, and SRE teams.

---

# 📥 Installing Go (Required Before Building)

Before compiling or running `server_stats.go`, Go must be installed.  
Use the correct package manager for your Linux distribution.

### **Ubuntu / Debian**
```bash
sudo apt update
sudo apt install -y golang
go version
````

### **Red Hat / CentOS / AlmaLinux / Rocky Linux**

```bash
sudo dnf install -y golang
# Or for older versions:
sudo yum install -y golang
go version
```

### **Fedora**

```bash
sudo dnf install -y golang
go version
```

### **Arch / Manjaro**

```bash
sudo pacman -S go
go version
```

### **openSUSE**

```bash
sudo zypper install go
go version
```

---

## 🔧 Install Latest Go (Recommended – Official tar.gz)

If you want the newest Go version:

```bash
wget https://go.dev/dl/go1.23.4.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.23.4.linux-amd64.tar.gz
```

Add Go to PATH:

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
go version
```

---

# ⚙️ Building & Running the Application

### **Build the binary**

```bash
go build -o server_stats server_stats.go
```

### **Run the app**

```bash
./server_stats
```

### **Run without building**

```bash
go run server_stats.go
```

---

# ✨ Features

## **1. System Information**

* OS version
* Hostname
* Kernel & architecture
* System uptime
* Load average (1m, 5m, 15m)

## **2. CPU Usage**

Accurate CPU usage is calculated by reading `/proc/stat` twice over a 1-second interval.

## **3. Memory Usage**

Reads `/proc/meminfo`:

* Total memory
* Available memory
* Used memory
* Memory utilization (%)

## **4. Disk Usage**

Uses `syscall.Statfs`:

* Total disk
* Used space
* Free space
* Disk utilization (%)
* Human-readable output (GiB)

## **5. Process Monitoring**

Using `ps` to display:

* Top 5 processes by CPU
* Top 5 processes by memory

## **6. Logged-in Users**

```
who
```

## **7. Failed Login Attempts**

```
lastb -n 10
```

(May require root.)

---

# 📊 Example Output

```
--------------------------------------------------------------------------------
BASIC SERVER INFO
--------------------------------------------------------------------------------
OS           : Ubuntu 22.04.3 LTS
Hostname     : gpu-server-1
Kernel       : linux amd64
Uptime       : 3d 12h 55m
Load Average : 0.32 0.45 0.50

--------------------------------------------------------------------------------
CPU USAGE
--------------------------------------------------------------------------------
Total CPU Usage: 12.45%

--------------------------------------------------------------------------------
MEMORY USAGE
--------------------------------------------------------------------------------
Total Memory: 15936 MB
Used Memory : 2450 MB
Free/Avail  : 13200 MB
Usage       : 15.38%

--------------------------------------------------------------------------------
DISK USAGE (ROOT FILESYSTEM)
--------------------------------------------------------------------------------
Total : 120.0 GiB
Used  : 53.2 GiB
Free  : 66.8 GiB
Usage : 44.30%

--------------------------------------------------------------------------------
TOP 5 PROCESSES BY CPU USAGE
--------------------------------------------------------------------------------
PID      COMMAND              %CPU     %MEM
1123     python               32.4     1.8

--------------------------------------------------------------------------------
TOP 5 PROCESSES BY MEMORY USAGE
--------------------------------------------------------------------------------
PID      COMMAND              %MEM     %CPU
987      java                 42.1     5.3

--------------------------------------------------------------------------------
LOGGED IN USERS
--------------------------------------------------------------------------------
root pts/0  2025-12-10 10:11 (:0)

--------------------------------------------------------------------------------
RECENT FAILED LOGIN ATTEMPTS (if available)
--------------------------------------------------------------------------------
btmp log entries…
```

---

# 🧱 Internal Architecture

| Component        | Purpose                 |
| ---------------- | ----------------------- |
| `/proc/stat`     | CPU usage               |
| `/proc/meminfo`  | Memory details          |
| `/proc/loadavg`  | Load averages           |
| `/proc/uptime`   | System uptime           |
| `syscall.Statfs` | Disk usage              |
| `ps`             | Process CPU & RAM usage |
| `who`, `lastb`   | Login & security info   |

---
