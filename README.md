# 🔍 Local Network Port Scanning - Task 1

## 📌 Objective

Learn to discover **open ports** on devices in the local network and understand possible **network exposures**.

## 🛠 Tools Used

* **Nmap** (for scanning)
* **Wireshark** (optional, for packet capture analysis)

---

## 🚀 Steps Followed by *Sri Hari*

### 1. Installed Nmap

Downloaded and installed **Nmap 7.98** on macOS.

```bash
nmap --version
```

Output:

```
Nmap version 7.98 ( https://nmap.org )
Platform: arm-apple-darwin24.4.0
```

---

### 2. Checked Local IP Address

Used `ifconfig` to find the local machine IP:

```
inet 192.168.0.115 netmask 0xffffff00 broadcast 192.168.0.255
```

👉 Local network range: `192.168.0.0/24`

---

### 3. Discovered Devices on Network

Used **Ping Scan**:

```bash
sudo nmap -sn 192.168.0.0/24
```

✅ Found **11 active hosts** including router, Apple devices, and unknown MAC vendors.

---

### 4. Performed SYN Stealth Scan

```bash
sudo nmap -sS 192.168.0.0/24 -oN ~/Desktop/scan_results.txt
```

📄 Results saved to `scan_results.txt` on Desktop.

---

### 5. Example Results

#### 📡 Router (192.168.0.1 - TP-Link)

```
22/tcp   open  ssh
53/tcp   open  domain
80/tcp   open  http
1900/tcp open  upnp
```

#### 💻 Local Machine (192.168.0.115 - Mac)

```
88/tcp    open  kerberos-sec
445/tcp   open  microsoft-ds
3306/tcp  open  mysql
5000/tcp  open  rtsp
5900/tcp  open  vnc (Apple Remote Desktop)
7000/tcp  open  rtsp
49152/tcp open  unknown
```

#### 📱 iPhone Devices (192.168.0.108 / 192.168.0.109)

```
49152/tcp open  unknown
62078/tcp open  iphone-sync
```

#### 📦 Device (192.168.0.121 - Cloud Network Tech)

```
3306/tcp open  mysql
```

---

### 6. Service Version Detection

```bash
nmap -sV 192.168.0.0/24
```

Sample output:

* Router (192.168.0.1):

  * `22/tcp OpenSSH 6.6.0`
  * `80/tcp TP-Link router http config`
* Mac (192.168.0.115):

  * `3306/tcp MySQL (unauthorized)`
  * `5900/tcp Apple remote desktop vnc`

---

## ⚠️ Security Risks Identified

* **Open MySQL (3306)**: Could allow unauthorized DB access if not secured.
* **VNC (5900)**: Remote desktop access → must be password protected.
* **UPnP (1900)**: Known for vulnerabilities in routers.
* **SSH (22)**: If weak credentials, attackers could gain shell access.

---

## 📂 Saved Scan Results

* `scan_results.txt` → Normal text format
* `scan_results.xml` (optional for import into tools)

---

Would you like me to also **format this README with a nice table** (IP → Open Ports → Services → Risks) so it looks cleaner for report submission?
