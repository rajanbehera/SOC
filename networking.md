# Computer Networking Quick Reference

> **Interview Study Guide** — All core networking concepts for SOC Analyst interviews: devices, protocols, OSI model, commands, and more.
>
> *Notes compiled by Rajan *

---

## Table of Contents

1. [Network Devices](#1-network-devices)
2. [Private IP Address Ranges](#2-private-ip-address-ranges)
3. [NAT and PAT](#3-nat-and-pat)
4. [Commonly Used Port Numbers](#4-commonly-used-port-numbers)
5. [Networking Basic Command Line Tools](#5-networking-basic-command-line-tools)
6. [TCP vs UDP](#6-tcp-vs-udp)
7. [TCP 3-Way Handshake](#7-tcp-3-way-handshake)
8. [TCP/IP Packet Structure](#8-tcpip-packet-structure)
9. [TCP Flags](#9-tcp-flags)
10. [OSI Reference Model](#10-osi-reference-model)
11. [DNS — Domain Name System](#11-dns--domain-name-system)
12. [DHCP — Dynamic Host Configuration Protocol](#12-dhcp--dynamic-host-configuration-protocol)
13. [ARP — Address Resolution Protocol](#13-arp--address-resolution-protocol)
14. [Proxy Servers](#14-proxy-servers)
15. [Firewall Related Questions](#15-firewall-related-questions)
16. [IPS / IDS Related Questions](#16-ips--ids-related-questions)
17. [Linux Commands Reference](#17-linux-commands-reference)

---

## 1. Network Devices

| Layer | Device | Description |
|-------|--------|-------------|
| Layer 1 | **Hub** | Connects multiple computers. Called a "dumb" device because it broadcasts all data to every port — no intelligence about destination. |
| Layer 2 | **Switch** | Connects two or more computers. Intelligently decides which computer the message is for and sends it directly — no broadcast needed. |
| Layer 3 | **Router** | Connects two or more networks. Calculates the best route for sending data from one point to another using routing protocols. |

---

## 2. Private IP Address Ranges

> **Key Fact:** Private IPs are also called **Non-Routable IP Addresses** — they cannot be routed over the public internet.

| Class | Range | CIDR Notation |
|-------|-------|---------------|
| Class A | 10.0.0.0 – 10.255.255.255 | `10.0.0.0/8` |
| Class B | 172.16.0.0 – 172.31.255.255 | `172.16.0.0/12` |
| Class C | 192.168.0.0 – 192.168.255.255 | `192.168.0.0/16` |

---

## 3. NAT and PAT

### NAT — Network Address Translation
The process of converting one IP address to another — typically a Private IP to a Public IP and vice versa.

### PAT — Port Address Translation
Allows multiple devices on a LAN to be mapped to a single public IP address. Goal: conserve public IP addresses.

**Examples:**
- Traffic to `100.20.30.40` on **Port 22** → NAT to `10.10.5.6` (Linux server)
- Traffic to `100.20.30.40` on **Port 443** → NAT to `10.10.5.7` (Web server)

---

## 4. Commonly Used Port Numbers

| Protocol | Service | Port | Protocol | Service | Port |
|----------|---------|------|----------|---------|------|
| FTP | File Transfer Protocol | `20, 21` | SNMP | Simple Network Management Protocol | `161, 162` |
| Telnet | Telnet | `23` | LDAP | Lightweight Directory Access Protocol | `389` |
| SSH | Secure Shell | `22` | HTTPS | Secure Hyper Text Transfer Protocol | `443` |
| SMTP | Simple Mail Transfer Protocol | `25` | MS SQL | Microsoft SQL | `1433` |
| DNS | Domain Name System | `53` | MySQL | mySQL Database | `3306` |
| DHCP | Dynamic Host Configuration Protocol | `67, 68` | RDP | Remote Desktop Protocol | `3389` |
| HTTP | Hyper Text Transfer Protocol | `80` | Syslog | Used to send logs to remote server | `514` |
| POP3 | Post Office Protocol | `110` | TLS Syslog | Secure Syslog | `6514` |
| NTP | Network Time Protocol | `123` | SFTP | Secure File Transfer Protocol | `22` |
| NetBIOS | NetBIOS Name Service | `135–139` | Secure SMTP | Secure Simple Mail Transfer Protocol | `587` |
| IMAP | Internet Message Access Protocol | `143` | | | |

---

## 5. Networking Basic Command Line Tools

### Windows — ipconfig

| Task | Command |
|------|---------|
| Find IP address | `ipconfig` |
| Find MAC address | `ipconfig /all` |
| Check DHCP enabled | `ipconfig /all` |
| Find Default Gateway | `ipconfig /all` |
| Find DNS servers | `ipconfig /all` |

> **Note:** MAC address is listed as **Physical Address** in Windows.

### Other Useful Commands

| Task | Command |
|------|---------|
| Check if host is reachable | `ping` |
| Check if port is open | `telnet <IP> <port>` |
| Get hostname of machine | `hostname` |
| Check open ports | `netstat -an` |

---

## 6. TCP vs UDP

### TCP — Transmission Control Protocol
- Connection Oriented
- Acknowledgement for each packet transmitted
- Failed packets are retransmitted
- Guaranteed delivery
- Reliable but slower
- Examples: HTTP, HTTPS, SMTP, SSH

### UDP — User Datagram Protocol
- Connection Less
- No Acknowledgement
- No re-transmission of lost packets
- Best effort delivery
- Unreliable but faster
- Examples: Streaming Videos, VoIP, Online Games

---

## 7. TCP 3-Way Handshake

A method used in TCP/IP to establish a connection between two hosts. Both client and server exchange SYN and ACK packets before actual data communication begins.

```
CLIENT  ──── SYN ────►  SERVER
CLIENT  ◄── SYN/ACK ──  SERVER
CLIENT  ──── ACK ────►  SERVER
```

1. Client sends a **SYN** packet — asking if the server is open for new connections
2. Server responds with **SYN/ACK** — acknowledges the request and signals willingness to communicate back
3. Client replies with an **ACK** — connection is now established; data communication can begin

---

## 8. TCP/IP Packet Structure

> A packet has 3 main sections: **IP Header**, **TCP Header**, and **Payload**.

### IP Header Fields
`Version` · `IHL` · `Type of Service` · `Total Length` · `Identification` · `Flags` · `Fragment Offset` · `Time to Live (TTL)` · `Protocol` · `Header Checksum` · `Source Address` · `Destination Address`

### Key Fields to Know
- **Source IP** — origin address
- **Destination IP** — target address
- **Source Port** — origin port
- **Destination Port** — target port
- **TCP Flags** — connection state indicators
- **Data / Payload** — actual content

---

## 9. TCP Flags

*(6 flags in TCP Header)*

| Flag | Full Name | Purpose |
|------|-----------|---------|
| `SYN` | Synchronization | Used in the first step of connection establishment (3-way handshake) |
| `ACK` | Acknowledgement | Acknowledges packets that have been successfully received by the host |
| `FIN` | Finish | Requests connection termination when there is no more data from the sender |
| `RST` | Reset | Terminates the connection if something is wrong with the TCP connection or it shouldn't exist |
| `PSH` | Push | Tells the receiver to process packets immediately as received, instead of buffering them |
| `URG` | Urgent | Data with URG=1 is forwarded to application layer immediately, even if more data is pending |

---

## 10. OSI Reference Model

| # | Layer | Function | Devices | Protocols | PDU |
|---|-------|----------|---------|-----------|-----|
| 7 | **Application** | Interface between user and computer; applications produce data to be transferred | — | HTTP, SMTP | Data |
| 6 | **Presentation** | Translation (ASCII↔HEX), Encoding/Decoding, Encryption/Decryption, Compression | — | JPEG, MPEG, TLS, SSL | Data |
| 5 | **Session** | Establishes/maintains sessions, authentication, security | — | NetBIOS, NFS, RPC | Data |
| 4 | **Transport** | Reliable delivery, ordering, no duplication, error control, flow control | — | TCP/UDP | Segments |
| 3 | **Network** | Routes data between hosts in different networks; selects shortest path | Routers, Firewall, IPS | RIP, OSPF | Packets |
| 2 | **Data Link** | Node-to-node delivery; framing, error/flow control. Sub-layers: LLC and MAC | Switch | ARP | Frames |
| 1 | **Physical** | Responsible for actual physical connection between devices | Hub, Bluetooth, WiFi | 802.11 | Bits |

> **OSI vs TCP/IP Model:** OSI is a reference model; TCP/IP is the practical model. In TCP/IP: Application+Presentation+Session merge into **Application**; Data Link+Physical merge into **Network Interface**. TCP/IP has 4 layers total.

### OSI Model Example — Sending an Email (Outlook)

1. Compose and send email in Outlook → **APPLICATION**
2. Email is encoded, encrypted (if enabled), compressed → **PRESENTATION**
3. Sending server initiates connection with receiving server → **SESSION**
4. Email flows error-free; receiver acknowledges → **TRANSPORT**
5. Each packet routed from sender to recipient email server → **NETWORK**
6. Node-to-node transmission using next hop MAC address → **DATA LINK**
7. Data transmitted as bits through cables/wireless → **PHYSICAL**

---

## 11. DNS — Domain Name System

DNS stands for **Domain Name System** — a service that translates domain names to IP addresses and vice versa.

### How DNS Works

1. Computer needs to reach facebook.com → sends request to **DNS Resolver**. If cached, returns IP immediately.
2. If not cached, Resolver reaches out to **Root Server** (13 root servers globally — hold index of TLDs)
3. **TLD Name Server** gives IP of the Authoritative Name Server for the requested domain
4. **Authoritative Name Server** returns the actual IP address
5. IP is returned to the client, which then makes the request and gets the response

### DNS — TCP or UDP?
- DNS uses **both** TCP and UDP
- **UDP** — for DNS Queries (faster)
- **TCP** — for Zone Transfers

### DNS Record Types

| Record | Purpose |
|--------|---------|
| `A` | Host address (IPv4) |
| `AAAA` | IPv6 host address |
| `CNAME` | Canonical name / alias |
| `MX` | Mail eXchange |
| `NS` | Name Server |
| `PTR` | Pointer (reverse lookup) |
| `SOA` | Start of Authority |
| `TXT` | Descriptive text |

---

## 12. DHCP — Dynamic Host Configuration Protocol

DHCP automatically assigns IP addresses and other network info to each host so they can communicate with other endpoints.

### DORA Process

| Step | Name | Description |
|------|------|-------------|
| **D** | Discover | Client broadcasts to all hosts. Source IP: `0.0.0.0` — Destination: `255.255.255.255` |
| **O** | Offer | Server unicasts an offer with: IP, Subnet, Default Gateway, DNS, Lease period |
| **R** | Request | Client officially requests the offered info by unicast to the server |
| **A** | Acknowledge | Server confirms the DHCP lease; client can now use the new IP settings |

### DHCP Follow-Up Q&A

**Q: What IP does the client use when sending DISCOVER?**
Source IP = `0.0.0.0` (no IP yet) | Destination IP = `255.255.255.255` (broadcast)

**Q: What if no DHCP server is available?**
Client gets an APIPA (Automatic Private IP Addressing) address in the range `169.254.0.0 – 169.254.255.255`

**Q: What if the DHCP server runs out of IP addresses?**
The subnet is "oversubscribed." DHCP refuses to assign new IPs until an existing device releases its address or a lease expires.

---

## 13. ARP — Address Resolution Protocol

ARP resolves an IP address to a physical MAC address. It operates at Layer 2 (Data Link).

### How ARP Works

1. Source device checks its ARP cache for the destination's MAC address. If found, uses it directly. If not, broadcasts an **ARP Request** to the local network.
2. All devices on the LAN receive the broadcast. The destination device replies with an **ARP Reply** (unicast) containing its MAC address.
3. Source machine updates its ARP cache with the new IP-to-MAC mapping for future use.

---

## 14. Proxy Servers

### What is a Proxy Server?
Processes requests on behalf of other machines. The IP address is converted via NAT. Proxy servers prevent external users from identifying internal IP addresses — making the network virtually invisible to outsiders.

### DNS Query: Client or Proxy?
- **IP Proxy:** Client does the DNS query, resolves the domain, then sends request to proxy
- **HTTP Proxy (Web Proxy):** Client sends request directly to proxy; proxy does the DNS resolution and forwards traffic

---

## 15. Firewall Related Questions

**Q: What is a Firewall?**
A network security system that monitors and controls incoming/outgoing traffic based on predetermined security rules (ACL — Access Control List). Traditional firewalls work at **Layer 3 and Layer 4**.

**Q: Why need a Firewall if routers have ACLs?**
A router's primary function is routing. Adding packet filtering slows the network. It is good practice to **separate filtering and routing functionality**.

**Q: What is DMZ?**
DeMilitarized Zone — a network segment hosting public-facing servers. It isolates them from internal servers so that if the DMZ is compromised, the attack doesn't spread internally.

**Q: What is Implicit Deny?**
If traffic is not explicitly allowed within an access list, it is **denied by default**.

**Q: Firewall Deny vs Drop?**
- **Deny:** Blocks connection and sends a Reset (RST) packet to the requester.
- **Drop:** Silently drops the request — no message sent to requester.
- *Best practice:* Deny outbound, Drop inbound (attacker won't know Firewall exists).

**Q: What is Stateful Inspection?**
A stateful firewall maintains a **State Table** of active allowed connections. Further packets in the same session are permitted through automatically.

**Q: What is VPN?**
A Virtual Private Network extends a private network across public networks, enabling secure data transmission.
- **Site-to-Site VPN:** Connects two office locations.
- **Remote VPN:** Users connect to corporate network from outside.

---

## 16. IPS / IDS Related Questions

**Q: What is IDS?**
Intrusion Detection System — detects malicious traffic based on network signatures and reports to admin. Compares current network activity to a known threat database.

**Q: IDS vs IPS?**
- **IDS:** Scans, detects, and *reports* malicious traffic.
- **IPS:** Scans, detects, and can also *block/prevent* malicious traffic.

**Q: IPS vs Firewall?**
- **Firewall:** Inspects TCP/IP header using ACLs.
- **IPS:** Does deep packet inspection (checks both header and payload using network signatures).

**Q: Where is IPS placed?**
IPS is placed **after the Firewall**. Firewall blocks unwanted traffic first; IPS does deep inspection on remaining allowed traffic. IPS needs more processing power — placing it first would waste resources.

### IDS Signature Example (Snort)

```snort
alert icmp any any -> $HOME_NET any
(msg:"ICMP test";
sid:1000001;
rev:1;
classtype:icmp-event;)

/* alert = rule action
   any any = source IP, source port
   $HOME_NET = destination IP
   sid = Snort rule ID */
```

---

## 17. Linux Commands Reference

| # | Task | Command |
|---|------|---------|
| 1 | Change directory | `cd` |
| 2 | Check running processes | `ps auxf` |
| 3 | Disk statistics | `df -h` |
| 4 | Find a file | `find / <name_of_file>` |
| 5 | Kill a process | `kill -9 <process_id>` |
| 6 | Get help on a command | `man top` / `top --help` |
| 7 | Create a new directory | `mkdir <new_directory_name>` |
| 8 | Change password | `passwd` |
| 9 | Present working directory | `pwd` |
| 10 | View last lines of file (live) | `tail -f <file_name>` |
| 11 | Display RAM and CPU info | `top` |
| 12 | Packet capture | `tcpdump -vvni eth0` |
| 13 | Find IP address on Linux | `ifconfig` |

---

### What happens when you type www.google.com and press Enter?

1. Browser checks its own cache for the IP. If not found, checks OS cache. If still not found, initiates a DNS request to the configured DNS server.
2. Once client has the IP, browser initiates a **TCP connection** with the server (3-way handshake)
3. Browser sends an **HTTP request** to the web server
4. Server handles the request and sends back a response
5. Browser displays the HTML content

---

### Quick Fire Questions

**Q: Can you connect 2 computers directly?**
Yes, with the help of **cross-over cables**.

**Q: ICMP works on which OSI layer?**
ICMP works on **Layer 3** (Network Layer).

**Q: What port does ping use?**
Ping uses **ICMP** (Internet Control Message Protocol) — it does *not* use TCP or UDP. ICMP type 8 = echo request; type 0 = echo reply. ICMP has no ports.
