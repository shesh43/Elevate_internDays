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
- whenever you have to find any devices either it maybe under you IP address or any target
- first know what is your or target IP address
- as for now i am working on my machine,  i need to find network interface's that were under mine IP address
- to find or look what mine IP address is **ifconfig** 
- ifconfig, to view or configure network interface IP addresses and settings in one command.
- ![[Pasted image 20260409171414.png]]

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
- ![[Pasted image 20260409171115.png]]

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
- also they workin' on and also syn and ack to confirm to continue the communication