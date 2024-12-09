# 🌐 NFStream Installation and Configuration on Kali Linux with Wireshark

![NFStream](https://img.shields.io/badge/Tool-NFStream-blue?style=for-the-badge&logo=python&logoColor=white)  
![Wireshark](https://img.shields.io/badge/Tool-Wireshark-blueviolet?style=for-the-badge&logo=wireshark&logoColor=white)  
![Version](https://img.shields.io/badge/Version-1.0-orange?style=for-the-badge)  
![Author](https://img.shields.io/badge/Author-Trung%20Huynh-lightblue?style=for-the-badge&logo=linkedin&logoColor=white)  
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)  
![Contributions](https://img.shields.io/badge/Contributions-Welcome-yellow?style=for-the-badge&logo=github&logoColor=white)

---

## 🚀 Introduction

NFStream is a flexible and efficient network traffic analysis framework. This guide will walk you through the steps to set up NFStream on Kali Linux and integrate it with Wireshark for monitoring network traffic on the `eth0` interface.

---

## 🔧 **Prerequisites**

### 1. 🛠️ Update System Packages
Ensure your system is up-to-date:
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. 🐍 Install Python and Pip
Ensure Python3 and pip3 are installed:
```bash
sudo apt install python3-pip -y
python3 --version
pip3 --version
```

### 3. 🌐 Install Python Virtual Environment
Set up a virtual environment to manage Python packages:
```bash
sudo apt install python3-venv -y
```

---

## **Step 1: Install NFStream**

### 1.1. 📦 Install Dependencies
Install required libraries and tools:
```bash
sudo apt install python3-dev autoconf automake libtool pkg-config flex bison gettext libjson-c-dev -y
sudo apt install libusb-1.0-0-dev libdbus-glib-1-dev libbluetooth-dev libnl-genl-3-dev -y
```

### 1.2. 🖥️ Create and Activate Virtual Environment
Create a Python virtual environment to isolate dependencies:
```bash
python3 -m venv nfstream_env
source nfstream_env/bin/activate
```

### 1.3. ⚙️ Install NFStream
Install NFStream via PyPi for the latest version:
```bash
pip install --upgrade pip
pip install nfstream
```
Alternatively, install from source:
```bash
git clone --recurse-submodules https://github.com/nfstream/nfstream.git
cd nfstream
python3 -m pip install --upgrade pip
python3 -m pip install -r dev_requirements.txt
python3 -m pip install .
```

---

## **Step 2: Integrate NFStream with Wireshark**

### 2.1. 🌐 Verify Network Interface
Check if the `eth0` network interface is active:
```bash
ifconfig eth0
```
You should see information about the `eth0` interface (e.g., IP and MAC address).

### 2.2. 🔍 Enable Promiscuous Mode
Activate promiscuous mode for `eth0` to capture all network packets:
```bash
sudo ifconfig eth0 promisc
```
Verify that `PROMISC` is active:
```bash
ifconfig eth0
```

### 2.3. 🧩 Install libpcap-dev
Ensure `libpcap-dev` is installed to allow packet capturing:
```bash
sudo apt install libpcap-dev -y
```

---

## **Step 3: Capture and Analyze Traffic with NFStream**

### 3.1. 📄 Capture Traffic to a PCAP File
Use `tcpdump` to capture network traffic:
```bash
sudo tcpdump -i eth0 -w test.pcap
```
You can generate traffic using a simple ping command:
```bash
ping 8.8.8.8
```

### 3.2. 🖥️ Analyze PCAP with NFStream
Create a Python script to read and analyze the captured traffic:

#### Create a Python Script:
```bash
nano nfstream_capture.py
```

#### Add the Following Code:
```python
from nfstream import NFStreamer

# Analyze traffic from PCAP file
streamer = NFStreamer(source="test.pcap")

for flow in streamer:
    print(flow)
```

#### Run the Script:
```bash
python3 nfstream_capture.py
```

---

## ✅ **Final Checks**

Ensure the `eth0` interface is active and receiving traffic. Use `tcpdump` to verify:
```bash
sudo tcpdump -i eth0
```
If no traffic is observed, generate network activity using tools like `ping` or browsing the web.

---

## 📜 **License**
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)  
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## 🤝 **Contributions**
![Contributions](https://img.shields.io/badge/Contributions-Welcome-yellow?style=flat-square)  
Contributions are always welcome! Feel free to fork the repository and submit pull requests.

