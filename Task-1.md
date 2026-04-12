## Scan Your Local Network for Open Ports
**Objective** :- Learn to discover open ports on devices in your local network to understand network exposure.
**Tools** :- Nmap, Wireshark

- Here in this task i will be practicing on tools called as nmap and wireshark
- so whenever we need to find the target first we need to scan the network 
- and we can easily do that with subnet 
- for now we will explore the local machines network 
- by that we come to understand how and where device or application will be running 
- As i am working on kali machine it had already pre-installed tools in it
- so we will be jumping directly to scan the network

#### Finding IP Range
- so to find IP addresses you need to scan your own IP subnet.
- and we will be finding these all things by the help of nmap.
##### why nmap ?
-  it quickly shows you every live device on your network and what ports/services they are running.
- and also shows what devices were connected like PCs, Phones, IoT,servers.
- by that you can spot potential security risks or misconfigurations.

## Practical
#### Finding Network interface IP addresses
**command** : ifconfig
![[Screenshot 2026-04-09 171110.png]]
- whenever you have to find any devices either it maybe under you IP address or any target
- first know what is your or target IP address
- as for now i am working on my machine,  i need to find network interface's that were under mine IP address
- to find or look what mine IP address is **ifconfig** 
- ifconfig, to view or configure network interface IP addresses and settings in one command.
- 

##### These are PRIVATE IP addresses
- 10.0.2.15     → Private range (Class A private)
- 172.18.0.1    → Private range (Class B private)
- 127.0.0.1     → Localhost (every computer has this)

#### Now let us look at 1 IP address  deeply
###### we need to explore the particular IP
- here i will be focusing on mine own machine let us see what we will find in it
- Real scan begins now
- so to find network interfaces like devices, application or any kind of scan we will be using the nmap tool
- by this tool we can scan by both Ip address or domain name
- but to find network interfaces we need to do scan under subnet
- because as this all kind of network interfaces were connected to or under mine Ip address network
- mine IP address is :- **10.0.2.15**
- 

- by this we will come to know which IP were alive and 
- also shows open ports and sometimes it will show us closed or filtered 
- as we found 3 IP  addresses we need to explore even deeper each of them
- by the help of nmap we can even enumerate all of these IP addresses
- to get to steal even more information that we will come to know is this secure or any unpatch service that this IP were running on 

###### let us try the stealth scan 
**command** :- nmap -sS ip addr
![[Pasted image 20260409182100.png]]

**Critical observation:** This appears to be a *Windows machine running MySQL* (unusual - MySQL is more common on Linux). Could be:
- Windows server with MySQL installed
- Developer machine with local MySQL
- Misconfigured IoT device running Windows
- by this we will come to know that we can even go deeper in scanning to find maybe  surprising unpatched services
- this is how stealth scan help find scan 


##### To go even more deeper we need 
- to go even deeper we need to scan the port 
- by this we can find easily on what service does this the device running on 
- in case any of the service is unpatched it can be easily attacked by attacker 
- you can see below the pic that i got all information about the device 
- **command** : nmap -sV -sC ip
- ![[Pasted image 20260409190655.png]]

> NEXT WE WILL BE EXPLORING THE WIRESHARK

## WIRESHARK
Wireshark is a **network protocol analyzer** used to capture and inspect packets traveling across a network in real time. It helps security analysts understand traffic behavior, detect anomalies, and investigate attacks.
##### why do we use wireshark
- Capture live network traffic
- Analyze packets in detail
- Troubleshoot network issues
- Detect suspicious activity
- Investigate attacks (MITM, scanning, malware)
- Understand protocols (HTTP, TCP, DNS, etc.)

##### Key Features (Important Ones)
- **Live Packet Capture** — Captures network traffic in real time from selected network interface.
- **Deep Packet Inspection** — Allows detailed analysis of packet contents across multiple protocol layers.
- **Display Filters** — Filters captured packets to quickly find specific traffic (e.g., HTTP, TCP, IP).
- **Follow TCP Streams** — Reconstructs full communication between client and server in readable format.

## Practical
- here we will be analysing the our one of ip address which is under machine network interface 
- first we need to open the wireshark 
- then when we go under wireshark, we need to select the eth0 
- **`eth0`** is the **first Ethernet network interface** on a Linux system used for wired network communication.
- ![[Pasted image 20260409184057.png]]
- as you can see the image 
- we can analyze each communcation that two ip addresses were communication
- as we can that source and destination
<<<<<<< HEAD
- also they workin' on and also syn and ack to confirm to continue the communication



## Interview based Question and Answer 
---
## 1. What is an Open Port?
A port is a **logical communication endpoint** on a system. An open port means a service or application is **actively listening** on that port, ready to accept connections.

> Think of it like a building — the IP address is the building, and ports are the doors. An open port is an **unlocked, open door** where someone is waiting inside.

- Ports range from **0 to 65535**
- Well-known ports: **80 (HTTP), 443 (HTTPS), 22 (SSH), 21 (FTP)**

---

## 2. How Does Nmap Perform a TCP SYN Scan?

TCP SYN scan is Nmap's **default and most popular scan** — also called a **Half-Open Scan** or **Stealth Scan.**

**How it works:**

```
Nmap → sends SYN packet to target port

If port is OPEN:
Target replies SYN-ACK
Nmap sends RST (reset) — never completes handshake

If port is CLOSED:
Target replies RST immediately

If port is FILTERED:
No response (firewall dropped the packet)
```

**Why it's stealthy:**

- Full TCP connection is **never completed**
- Many older systems and basic firewalls **don't log incomplete connections**
- Faster than full connect scan

**Command:**

bash

```bash
nmap -sS 192.168.1.1
```

---

## 3. What Risks Are Associated with Open Ports?

|Risk|Explanation|
|---|---|
|**Attack Surface**|Every open port is a potential entry point|
|**Service Exploitation**|Vulnerable service on that port can be exploited|
|**Information Disclosure**|Port + banner reveals OS, software, version|
|**Brute Force**|SSH (22), RDP (3389) open = brute force target|
|**Unauthorized Access**|Misconfigured services allow direct access|
|**Lateral Movement**|Attacker uses internal open ports to move across network|

> **Simple truth:** Every unnecessary open port is an **unnecessary risk.**

---

## 4. Difference Between TCP and UDP Scanning

|Factor|TCP Scanning|UDP Scanning|
|---|---|---|
|**Connection**|Connection-oriented — has handshake|Connectionless — no handshake|
|**Reliability**|Response always comes back|No response = open OR filtered (ambiguous)|
|**Speed**|Faster — clear open/closed response|Slow — relies on timeouts|
|**Detection**|Easier to detect|Harder to detect|
|**How open is identified**|SYN-ACK reply = open|No response = likely open|
|**How closed is identified**|RST reply = closed|ICMP Port Unreachable = closed|
|**Common ports**|80, 443, 22, 3306|53 (DNS), 161 (SNMP), 67 (DHCP)|

**Nmap commands:**

bash

```bash
nmap -sS 192.168.1.1    ← TCP SYN scan
nmap -sU 192.168.1.1    ← UDP scan
```

> **Key insight:** UDP scanning is harder because **silence doesn't always mean closed** — it could be open and just not responding.

---

## 5. How Can Open Ports Be Secured?

1. **Close unnecessary ports** — if no service needs it, shut it down
2. **Firewall rules** — whitelist only required ports per source IP
3. **Use non-default ports** — move SSH from 22 to a custom port (security by obscurity, not a fix alone)
4. **Keep services patched** — vulnerable services on open ports are prime targets
5. **Disable banner grabbing** — don't let services reveal version info
6. **Use VPN for sensitive services** — RDP, SSH should not be publicly open
7. **Network segmentation** — internal services should never be exposed externally
8. **IDS/IPS monitoring** — alert on unusual port activity or scanning behavior

---

## 6. What is a Firewall's Role Regarding Ports?

A firewall acts as a **gatekeeper** between the network and the outside world. Its job regarding ports:

- **Allow** traffic only on permitted ports
- **Block/Drop** traffic on all other ports
- **Filter by direction** — inbound vs outbound rules
- **Filter by source** — only allow specific IPs to reach specific ports
- **Stateful inspection** — track active connections, block unsolicited packets

```
Internet → Firewall → Only port 443 allowed → Web Server
                    → Port 22 blocked       → SSH (protected)
                    → Port 3306 blocked     → Database (never exposed)
```

> **Firewall doesn't close ports — it controls WHO can reach them and from WHERE.**

---

## 7. What is a Port Scan and Why Do Attackers Perform It?

A **port scan** is the process of systematically probing a target's ports to discover which ones are **open, closed, or filtered** — and what services are running on them.

**Why attackers do it:**

|Reason|Purpose|
|---|---|
|**Reconnaissance**|Map the attack surface before launching an attack|
|**Service discovery**|Find what software is running and its version|
|**Vulnerability identification**|Match open services to known CVEs|
|**Finding weak points**|Old FTP, Telnet, unpatched SSH = easy entry|
|**Network mapping**|Understand the internal structure of the target|

**Attacker's thought process:**

```
Port 22 open (SSH) → Try brute force or exploit known CVE
Port 21 open (FTP) → Try anonymous login
Port 8080 open (HTTP) → Check for admin panel, default creds
Port 27017 open (MongoDB) → Try connecting without authentication
```

> **Port scanning is not an attack itself — it's the attacker's intelligence gathering phase.**

---

## 8. How Does Wireshark Complement Port Scanning?

Nmap tells you **what is open.** Wireshark tells you **what is happening.**

| Nmap                  | Wireshark                              |
| --------------------- | -------------------------------------- |
| Discovers open ports  | Captures actual packets on those ports |
| Identifies services   | Reveals what data is being transmitted |
| Active — sends probes | Passive — just listens and captures    |
| High-level results    | Packet-level deep inspection           |
| Used for scanning     | Used for traffic analysis              |


thank you
=======
- also they workin' on and also syn and ack to confirm to continue the communication
>>>>>>> f186967d648b10ef67c992411d5d3251c6953019
