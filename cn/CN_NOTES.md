# 4 U By U &bull; Complete Computer Networks (CN) Masterclass & Placement Blueprint

> **Primary Video Sources:**  
> 1. Kunal Kushwaha: *Computer Networking Full Course - OSI Model Deep Dive with Real Life Examples* ([Watch Video](https://www.youtube.com/watch?v=IPvYjXCsTg8)) &bull; Video ID: `IPvYjXCsTg8`  
> 2. Gate Smashers: *Complete CN Interview Questions in One Shot | Placement Revision* ([Watch Video](https://www.youtube.com/watch?v=skvCwFPZ7zM)) &bull; Video ID: `skvCwFPZ7zM`  
> 3. Gate Smashers: *Placement Interview Questions Series* (Playlist: `PLUDPUBNI7KL4`)  
> **Target Audience:** Engineering Students, System Architects & Placement Candidates  
> **Status:** 100% Verified Comprehensive Masterclass Notes with Deep Timestamps  

---

## Master Table of Contents
1. [Module 1: Computer Networking Fundamentals & Topologies](#module-1-computer-networking-fundamentals--topologies)
2. [Module 2: Network Architectures: OSI 7-Layer vs TCP/IP 5-Layer Models](#module-2-network-architectures-osi-7-layer-vs-tcpip-5-layer-models)
3. [Module 3: Physical & Data Link Layers (Framing, MAC, Error Control)](#module-3-physical--data-link-layers-framing-mac-error-control)
4. [Module 4: Network Layer (IPv4, IPv6, Subnetting, NAT & Routing)](#module-4-network-layer-ipv4-ipv6-subnetting-nat--routing)
5. [Module 5: Transport Layer (TCP, UDP, Handshakes & Congestion Control)](#module-5-transport-layer-tcp-udp-handshakes--congestion-control)
6. [Module 6: Application Layer Protocols (DNS, HTTP/1-3, HTTPS, DHCP, Email)](#module-6-application-layer-protocols-dns-http1-3-https-dhcp-email)
7. [Module 7: The Master Placement Interview Question: "URL to Page Render"](#module-7-the-master-placement-interview-question-url-to-page-render)
8. [Module 8: Top 30 High-Yield CN Placement Interview Questions & Answers](#module-8-top-30-high-yield-cn-placement-interview-questions--answers)

---

## Module 1: Computer Networking Fundamentals & Topologies
*Video Timestamps:* `IPvYjXCsTg8` &bull; 0:00 (Intro), 4:50 (Origins), 48:00 (LAN/MAN/WAN), 55:47 (Topologies)

### 1.1 What is a Computer Network?
- An interconnection of autonomous computing devices (nodes/hosts) connected via transmission media (guided cables or wireless RF) and communicating using a common set of protocols.
- **Key Metrics:**
  - **Bandwidth:** Maximum theoretical data transfer rate across a link (measured in bps, Mbps, Gbps).
  - **Throughput:** Actual operational volume of successful data delivered per unit time.
  - **Latency / Delay:** Total round-trip or one-way transit time ($T_{\text{total}} = T_{\text{propagation}} + T_{\text{transmission}} + T_{\text{queuing}} + T_{\text{processing}}$).
  - **Jitter:** Variation in packet arrival latency (critical in VoIP and real-time streaming).

### 1.2 Network Classifications by Geographic Scale
1. **PAN (Personal Area Network):** Range $\approx 10$ meters (Bluetooth, Zigbee, USB tethering).
2. **LAN (Local Area Network):** Single office, building, or campus. High bandwidth (100 Mbps to 10 Gbps), low latency, privately owned (Ethernet 802.3, Wi-Fi 802.11).
3. **MAN (Metropolitan Area Network):** Spans a city/metro region (Cable TV networks, city-wide municipal fiber).
4. **WAN (Wide Area Network):** Spans countries or continents. Interconnects heterogeneous LANs via telecom carriers, routers, and submarine optical fiber cables. The Internet is the premier public WAN.

### 1.3 Physical & Logical Topologies
- **Bus Topology:** Single central backbone cable (coaxial/bus) with terminators at both ends.
  - *Pros:* Minimal cabling, inexpensive.
  - *Cons:* Single point of failure (backbone break halts entire network), high collision probability under load.
- **Star Topology:** Every node connects independently to a central hub/switch via point-to-point links.
  - *Pros:* Failure of one host cable does not impact others; easy troubleshooting and scaling.
  - *Cons:* Failure of the central switch disables the entire network. Standard topology for modern enterprise Ethernet.
- **Ring Topology:** Nodes connected in a circular loop; tokens circulate unidirectionally (e.g., Token Ring 802.5, FDDI).
  - *Pros:* Deterministic transmission, zero packet collisions.
  - *Cons:* Break in the ring drops the network unless dual counter-rotating rings are deployed.
- **Mesh Topology (Full Mesh vs Partial Mesh):**
  - In Full Mesh with $N$ nodes, each node connects directly to every other node via dedicated point-to-point links.
  - **Link Formula:** Number of physical duplex links = $\frac{N(N-1)}{2}$.
  - Number of I/O ports per device = $N - 1$.
  - *Pros:* Ultimate redundancy, zero bottlenecking, instant fault isolation.
  - *Cons:* Exponential cabling cost and hardware port complexity. Used in ISP backbones and critical telemetry.
- **Tree (Hierarchical) Topology:** Combination of Star and Bus topologies arranged in parent-child hierarchy.

---

## Module 2: Network Architectures: OSI 7-Layer vs TCP/IP 5-Layer Models
*Video Timestamps:* `IPvYjXCsTg8` &bull; 1:06:33 (OSI 7 Layers), 1:29:00 (TCP/IP Model); `skvCwFPZ7zM` &bull; 2:15 (Layer Functions)

### 2.1 The OSI 7-Layer Reference Model (ISO/IEC 7498-1)
```
[ Layer 7: Application  ] -> User Interface, HTTP, DNS, SMTP, SSH (Data/Message)
[ Layer 6: Presentation ] -> Encryption/Decryption, Compression, Serialization (Data)
[ Layer 5: Session      ] -> Dialog control, checkpointing, session tokens (Data)
[ Layer 4: Transport    ] -> End-to-End Reliability, Port Addressing (Segments / Datagrams)
[ Layer 3: Network      ] -> Logical IP Routing, Path Determination (Packets)
[ Layer 4: Data Link    ] -> Hop-to-Hop Framing, MAC Addressing, Error Check (Frames)
[ Layer 1: Physical     ] -> Bitstream Transmission, Voltage, Radio Waves (Bits)
```

1. **Layer 7 &mdash; Application Layer:** Interacts directly with software applications. Provides network services (HTTP, HTTPS, FTP, SMTP, DNS, SSH, Telnet).
2. **Layer 6 &mdash; Presentation Layer:** Syntax and semantics translator. Performs **character encoding** (ASCII, UTF-8), **data compression**, and **cryptographic encryption/decryption** (SSL/TLS serialization).
3. **Layer 5 &mdash; Session Layer:** Establishes, maintains, synchronizes, and terminates sessions (dialogue management, simplex/half-duplex/full-duplex control, session recovery via checkpoints).
4. **Layer 4 &mdash; Transport Layer:** True end-to-end process-to-process delivery. Manages **port addressing**, segmentation and reassembly, connection-oriented (TCP) vs connectionless (UDP) transport, flow control (Sliding Window), and congestion control.
5. **Layer 3 &mdash; Network Layer:** Host-to-host delivery across heterogeneous subnets. Manages **logical addressing (IPv4/IPv6)**, packet routing algorithms (OSPF, BGP, RIP), fragmentation, and Network Address Translation (NAT).
6. **Layer 2 &mdash; Data Link Layer (DLL):** Node-to-node (hop-to-hop) error-free frame transfer across a single physical medium. Subdivided into:
   - **LLC (Logical Link Control):** Flow control, multiplexing.
   - **MAC (Media Access Control):** Hardware physical addressing (48-bit MAC) and channel contention (CSMA/CD, CSMA/CA).
7. **Layer 1 &mdash; Physical Layer:** Raw bitstream transmission over physical media (voltages on copper UTP, optical pulses in fiber, RF waves in Wi-Fi). Defines connector pinouts, cable specs, signal modulation.

### 2.2 Data Encapsulation & Decapsulation (PDU Stack)
```
Sender (Encapsulation: Top-Down)              Receiver (Decapsulation: Bottom-Up)
[ Application Data ]                          [ Application Data ]
       |                                             ^
       v [+ L4 TCP Header]                           | [- L4 TCP Header]
[ Segment: Port + Seq + Data ]                [ Segment ]
       |                                             ^
       v [+ L3 IP Header]                            | [- L3 IP Header]
[ Packet: IP Src/Dst + L4 Segment ]           [ Packet ]
       |                                             ^
       v [+ L2 MAC Header + FCS Trailer]             | [- L2 MAC Header/Trailer]
[ Frame: MAC Src/Dst + L3 Packet + CRC ]      [ Frame ]
       |                                             ^
       v                                             |
[ Physical Bits: 0110100110... ] ------------> [ Physical Bits ]
```

### 2.3 OSI Model vs TCP/IP Model Matrix
| Feature | OSI Reference Model | TCP/IP Model (Internet Standard) |
|---|---|---|
| **Origin** | ISO theoretical conceptual standard (1984) | DoD DARPA real-world implementation (ARPANET) |
| **Number of Layers**| 7 Layers | 4 or 5 Layers (Application, Transport, Network, Link, Physical) |
| **Session & Presentation**| Explicit dedicated layers (L5, L6) | Integrated directly into Application Layer (L7) |
| **Protocol Independence**| Model developed *before* protocols | Protocols (TCP, IP) designed *before* the model |
| **Dominance** | Teaching and architectural framework | The actual working architecture of the global Internet |

---

## Module 3: Physical & Data Link Layers
*Video Timestamps:* `IPvYjXCsTg8` &bull; 42:25 (Subsea Cables), 3:55:40 (DLL/Physical); `skvCwFPZ7zM` &bull; 8:40 (MAC & Framing)

### 3.1 Network Hardware Devices
- **Repeater / Hub (Layer 1):** Multiport signal regenerator. Broadcasts incoming bits to all ports indiscriminately. Single collision domain, single broadcast domain. Passive and unintelligent.
- **Bridge / Switch (Layer 2):** Intelligent frame-forwarding device. Inspects Layer 2 destination MAC addresses and maintains a dynamic **MAC Address Table (CAM Table)** via source MAC learning. Isolates collision domains per port! (Single broadcast domain).
- **Router (Layer 3):** Inter-network device inspecting destination IP addresses. Maintains a **Routing Table** to forward packets across distinct subnets and broadcast domains. Isolates broadcast domains.
- **Gateway:** Protocol converter operating up to Layer 7 to bridge incompatible networks (e.g., VoIP gateway connecting SIP to PSTN).

### 3.2 Data Link Layer Functions
1. **Framing:** Encapsulating network packets into frames with start/end delimiters (Character stuffing / Bit stuffing with `01111110` flag).
2. **Physical Addressing:** 48-bit (6-byte) MAC address expressed in hex (e.g., `00:1A:2B:3C:4D:5E`).
   - First 24 bits: OUI (Organizationally Unique Identifier assigned by IEEE).
   - Last 24 bits: Network Interface Controller (NIC) specific serial.
3. **Error Detection Techniques:**
   - **Parity Bit:** Simple 1-bit overhead; detects single-bit errors only.
   - **Checksum:** 16-bit 1's complement sum of segments. Used in IP, TCP, and UDP headers.
   - **CRC (Cyclic Redundancy Check):** Polynomial division ($GF(2)$ arithmetic). Frame Check Sequence (FCS) appended to Ethernet frames. Robustly catches burst errors.
4. **Flow Control Protocols:**
   - **Stop-and-Wait:** Sender transmits 1 frame, pauses until positive ACK arrives. Very poor utilization over high-latency channels.
   - **Sliding Window:** Permits sender to transmit $W$ frames before requiring ACK.
     - **Go-Back-N (GBN):** Window size $N$. Receiver accepts only in-order frames (discards out-of-order frames). Sender re-transmits all frames from the unacknowledged frame on timeout.
     - **Selective Repeat (SR):** Receiver buffers out-of-order frames within receiver window. Sender re-transmits only the specific lost frame. Optimal bandwidth utilization.
5. **Channel Contention: CSMA/CD vs CSMA/CA**
   - **CSMA/CD (Carrier Sense Multiple Access with Collision Detection):** Used in half-duplex wired Ethernet (IEEE 802.3). Listens while transmitting; if a collision occurs, emits a jam signal and backs off using **Binary Exponential Backoff** algorithm ($0 \le r < 2^k$).
   - **CSMA/CA (Collision Avoidance):** Used in wireless Wi-Fi (IEEE 802.11). Collision detection impossible on radio; uses Inter-Frame Spaces (IFS), Contention Windows, and explicit RTS/CTS handshakes.

---

## Module 4: Network Layer (IPv4, IPv6, Subnetting & Routing)
*Video Timestamps:* `IPvYjXCsTg8` &bull; 24:20 (IP Addressing), 3:24:30 (IP Deep Dive), 3:41:42 (IPv4 vs IPv6), 3:52:32 (NAT)

### 4.1 IPv4 Addressing & Classes
- 32-bit logical address formatted as 4 octets in dotted decimal (e.g., `192.168.1.1`).
- Total theoretical address space: $2^{32} \approx 4.29$ billion addresses.

#### Classful Addressing (Legacy)
| Class | First Octet Range | Default Subnet Mask | Leading Bits | Network / Host Ratio | Total Networks | Usable Hosts per Net |
|---|---|---|---|---|---|---|
| **Class A** | 1 &ndash; 126 | `255.0.0.0` (/8) | `0...` | 8 bits Net, 24 bits Host | 126 | $2^{24} - 2 = 16,777,214$ |
| **Class B** | 128 &ndash; 191 | `255.255.0.0` (/16) | `10...` | 16 bits Net, 16 bits Host | 16,384 | $2^{16} - 2 = 65,534$ |
| **Class C** | 192 &ndash; 223 | `255.255.255.0` (/24) | `110...` | 24 bits Net, 8 bits Host | 2,097,152 | $2^8 - 2 = 254$ |
| **Class D** | 224 &ndash; 239 | N/A | `1110...` | Multicasting only | N/A | N/A |
| **Class E** | 240 &ndash; 255 | N/A | `1111...` | Reserved for experimental R&D | N/A | N/A |

*Special Reserved Addresses:*
- `127.0.0.0/8`: Loopback address (`127.0.0.1` represents localhost).
- `0.0.0.0`: Non-routable meta-address representing "any interface" or default route.
- `255.255.255.255`: Limited broadcast address.

#### RFC 1918 Private (Non-Routable) IP Ranges
- **Class A Private:** `10.0.0.0` to `10.255.255.255` (`10.0.0.0/8`)
- **Class B Private:** `172.16.0.0` to `172.31.255.255` (`172.16.0.0/12`)
- **Class C Private:** `192.168.0.0` to `192.168.255.255` (`192.168.0.0/16`)

### 4.2 CIDR (Classless Inter-Domain Routing) & Subnetting Math
- Replaced classful routing to halt IPv4 exhaustion.
- Notation: `IP_Address / Prefix_Length` (e.g., `192.168.10.0/26`).
  - Prefix length $P$ = number of bits fixed for Network ID.
  - Remaining host bits $H = 32 - P$.
  - Number of usable hosts = $2^H - 2$ (Subtract 2 for Network ID and Directed Broadcast Address).

#### Solved Subnetting Numerical:
**Given:** IP block `192.168.1.0/27`.
1. Subnet Mask: 27 consecutive 1s &rarr; `11111111.11111111.11111111.11100000` = `255.255.255.224`.
2. Host bits $H = 32 - 27 = 5$.
3. Total IP addresses per subnet = $2^5 = 32$.
4. Usable hosts = $32 - 2 = 30$ hosts.
5. Block size = 32:
   - First Subnet: `192.168.1.0` (Net ID) to `192.168.1.31` (Broadcast). Usable: `.1` to `.30`.
   - Second Subnet: `192.168.1.32` (Net ID) to `192.168.1.63` (Broadcast). Usable: `.33` to `.62`.

### 4.3 NAT (Network Address Translation) & PAT
- Solves public IPv4 scarcity by translating private RFC 1918 addresses within a local LAN into a single public IPv4 address when accessing the Internet.
- **PAT (Port Address Translation / NAT Overload):** Maps internal `Private IP : Private Port` tuples to `Public IP : Unique High Port` in a NAT translation table.

### 4.4 IPv4 vs IPv6 Architectural Comparison
| Parameter | IPv4 | IPv6 |
|---|---|---|
| **Address Length** | 32 bits (4 bytes) | 128 bits (16 bytes) |
| **Address Space** | $2^{32} \approx 4.29 \times 10^9$ | $2^{128} \approx 3.4 \times 10^{38}$ (Undecillion) |
| **Notation** | Dotted Decimal (e.g., `172.217.16.206`) | Hexadecimal with colons (e.g., `2001:0db8:85a3::8a2e:0370:7334`) |
| **Header Size** | Variable (20 to 60 bytes with options) | Fixed 40 bytes (streamlines router processing) |
| **Checksum in Header**| Yes (must be recomputed at every router hop)| No (Checksum delegated to L2 and L4) |
| **Fragmentation** | Performed by routers and sender | Performed **only by sending host** (Path MTU discovery) |
| **Security** | IPsec optional add-on | IPsec natively baked into architecture |

### 4.5 Routing Algorithms: Distance Vector vs Link State
1. **Distance Vector Routing (Bellman-Ford Algorithm):**
   - Each router shares its complete routing table exclusively with immediate neighbors at regular intervals.
   - Metric: Hop count (e.g., RIP max 15 hops; 16 = unreachable).
   - Susceptible to **Count-to-Infinity Problem** (mitigated via Split Horizon and Poison Reverse).
2. **Link State Routing (Dijkstra’s SPF Algorithm):**
   - Each router floods Link State Advertisements (LSAs) containing the status of its own links to **all routers** in the network.
   - Every router constructs an identical topology map of the entire autonomous system and computes the shortest path tree independently.
   - Fast convergence, zero loops (e.g., OSPF, IS-IS).
3. **BGP (Border Gateway Protocol):** Path Vector protocol running across autonomous systems on the global Internet backbone (TCP port 179).

---

## Module 5: Transport Layer (TCP, UDP & Concurrency)
*Video Timestamps:* `IPvYjXCsTg8` &bull; 34:23 (Ports), 2:32:24 (Transport), 2:54:00 (UDP), 3:02:05 (TCP), 3:09:10 (3-Way Handshake)

### 5.1 Ports & Sockets
- **Socket:** The fundamental endpoint for inter-process network communication defined as `IP Address : Port Number` (e.g., `142.250.190.46:443`).
- **Port Ranges:**
  - **Well-Known Ports (0 &ndash; 1023):** System services (HTTP 80, HTTPS 443, DNS 53, SSH 22, FTP 20/21, SMTP 25, DHCP 67/68).
  - **Registered Ports (1024 &ndash; 49151):** Vendor apps (MySQL 3306, PostgreSQL 5432, Redis 6379, MongoDB 27017).
  - **Dynamic / Ephemeral Ports (49152 &ndash; 65535):** Allocated client-side for temporary outbound connections.

### 5.2 TCP vs UDP Architectural Comparison
| Parameter | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
|---|---|---|
| **Connection State** | Connection-Oriented (Requires 3-way handshake) | Connectionless (No handshake; fire-and-forget) |
| **Reliability** | 100% Reliable (Guaranteed delivery via ACKs & retransmission)| Unreliable (Best-effort; packets may drop or duplicate) |
| **Data Ordering** | Strictly ordered (Sequence numbers reassemble streams) | Unordered (Arrives in arbitrary order) |
| **Header Overhead** | Minimum 20 bytes (up to 60 bytes with options) | Fixed 8 bytes |
| **Flow & Congestion Control**| Yes (Sliding window, AIMD, Slow Start) | None (Transmits at application rate) |
| **Speed** | Slower due to handshakes, ACKs, and windowing | Blazing fast, minimal protocol latency |
| **Ideal Use Cases** | Web (HTTP/HTTPS), File transfers (FTP), Email (SMTP), SSH | Video conferencing (Zoom), Gaming, DNS queries, VoIP |

### 5.3 The TCP 3-Way Handshake (Connection Establishment)
```
      CLIENT                                               SERVER
        |                                                    |
        |  Step 1: SYN (Seq = X)                             |  (Server is in LISTEN state)
        |--------------------------------------------------->|  (Moves to SYN-RCVD state)
        |                                                    |
        |  Step 2: SYN-ACK (Seq = Y, Ack = X + 1)            |
        |<---------------------------------------------------|
  (Moves to ESTABLISHED)                                     |
        |                                                    |
        |  Step 3: ACK (Seq = X + 1, Ack = Y + 1)            |
        |--------------------------------------------------->|  (Moves to ESTABLISHED state)
        |                                                    |
   [ BIDIRECTIONAL FULL-DUPLEX DATA TRANSFER STREAM BEGINS ]
```
- **Why a 3-Way Handshake?** Two steps are insufficient to synchronize both parties' independent Initial Sequence Numbers (ISNs) and confirm mutual bidirectional reception over an unreliable medium.

### 5.4 TCP 4-Way Connection Teardown
```
      CLIENT                                               SERVER
        |                                                    |
        |  Step 1: FIN (Seq = u)                             |  (Client finished sending data)
        |--------------------------------------------------->|  (Server moves to CLOSE-WAIT)
        |                                                    |
        |  Step 2: ACK (Ack = u + 1)                         |
        |<---------------------------------------------------|
  (Client in FIN-WAIT-2)                                     |  (Server finishes sending remaining data)
        |                                                    |
        |  Step 3: FIN (Seq = v, Ack = u + 1)                |
        |<---------------------------------------------------|  (Server moves to LAST-ACK)
        |                                                    |
        |  Step 4: ACK (Ack = v + 1)                         |
        |--------------------------------------------------->|  (Server CLOSED)
  (Client enters TIME-WAIT: 2 * MSL)                         |
        |                                                    |
     (CLOSED after timeout)
```
- **TIME-WAIT State:** The initiating endpoint lingers in `TIME-WAIT` for **$2 \times \text{MSL}$** (Maximum Segment Lifetime, typically 60 to 120 seconds) to ensure the final ACK reached the peer and prevent stale duplicated segments from polluting a new connection on the same port tuple.

### 5.5 TCP Flow Control vs Congestion Control
1. **Flow Control (Receiver Protection):**
   - Regulated by the **Receive Window (`rwnd`)** advertised in TCP headers by the receiving host.
   - Prevents a fast sender from overwhelming a slow receiver's buffer.
2. **Congestion Control (Network Protection):**
   - Regulated by the sender's dynamic **Congestion Window (`cwnd`)**.
   - Transmission rate = $\min(\text{cwnd}, \text{rwnd})$.
   - **Phases:**
     - **Slow Start:** Starts with small $cwnd$ (e.g., 10 MSS); doubles exponentially ($2^k$) every RTT until `ssthresh` (Slow Start Threshold).
     - **Congestion Avoidance (AIMD):** Linear growth; increases $cwnd$ by 1 MSS per RTT.
     - **On Packet Loss (Timeout vs 3 Duplicate ACKs):**
       - *Timeout:* Drastic reset; sets `ssthresh = cwnd / 2`, collapses $cwnd = 1$ MSS (Tahoe).
       - *3 Duplicate ACKs (Fast Retransmit & Fast Recovery):* Reno halves $cwnd$ (`cwnd = cwnd / 2`) and resumes linear growth without dropping to 1.

---

## Module 6: Application Layer Protocols
*Video Timestamps:* `IPvYjXCsTg8` &bull; 1:53:12 (HTTP), 2:04:44 (Status Codes), 2:19:00 (DNS); `skvCwFPZ7zM` &bull; 25:10 (Application Layer)

### 6.1 DNS (Domain Name System) &mdash; Port 53 (UDP & TCP)
- Distributed, hierarchical database translating human-readable FQDNs (e.g., `www.google.com`) into routable IP addresses (`142.250.190.46`).
- Uses **UDP port 53** for fast lightweight lookups; falls back to **TCP port 53** for zone transfers or responses $> 512$ bytes (EDNS0).
- **Hierarchical Tree Structure:**
  1. **Root DNS Servers:** 13 logical root server clusters (`a.root-servers.net` to `m.root-servers.net`) operated via Anycast.
  2. **Top-Level Domain (TLD) Servers:** Manages `.com`, `.org`, `.net`, `.edu`, and ccTLDs (`.in`, `.uk`).
  3. **Authoritative DNS Servers:** The final source of truth managed by domain owners and DNS hosts.
- **Recursive vs Iterative Queries:**
  - *Recursive Query:* Client requests Local DNS Resolver to return the final answer. Resolver assumes the burden of tracking down the IP.
  - *Iterative Query:* Resolver queries root, TLD, and authoritative servers sequentially; each server returns a referral pointer to the next level down.
- **Key DNS Record Types:**
  - `A`: Maps hostname to 32-bit IPv4 address.
  - `AAAA`: Maps hostname to 128-bit IPv6 address.
  - `CNAME`: Canonical Name (alias pointing to another domain).
  - `MX`: Mail Exchange server records with priority rankings.
  - `NS`: Authoritative Name Server for the zone.
  - `PTR`: Pointer record for Reverse DNS lookups (IP to hostname).
  - `TXT`: Arbitrary text data (SPF, DKIM, DMARC email authentication).

### 6.2 HTTP Evolution: HTTP/1.1 vs HTTP/2 vs HTTP/3
| Parameter | HTTP/1.1 (1997) | HTTP/2 (2015) | HTTP/3 (2022) |
|---|---|---|---|
| **Transport Layer** | TCP (Port 80/443) | TCP (Port 443 with TLS 1.2+) | **QUIC over UDP** (Port 443) |
| **Formatting** | Plain text human-readable | Binary Framing Layer (Frames & Streams) | Binary (QUIC native) |
| **Multiplexing** | Sequential (HOL Blocking on connection) | True Multiplexing over single TCP connection | True Multiplexing over UDP |
| **Head-of-Line (HOL) Blocking**| Severe at HTTP application level | Eliminated at HTTP level; **persists at TCP level** if packet drops | **Completely eliminated!** Packet loss in one stream never blocks other streams |
| **Header Compression** | None (Cookies sent repeatedly) | **HPACK** (Static & dynamic Huffman tables) | **QPACK** (Optimized for out-of-order UDP) |
| **Handshake Latency** | TCP (1 RTT) + TLS (1-2 RTT) = 2-3 RTT | TCP (1 RTT) + TLS 1.3 (1 RTT) = 2 RTT | **0-RTT or 1-RTT connection setup** via QUIC! |

### 6.3 HTTP Methods & Status Codes
- **Idempotent Methods:** `GET`, `HEAD`, `PUT`, `DELETE` (Executing multiple identical requests produces the exact same server resource state).
- **Non-Idempotent Methods:** `POST`, `PATCH`.
- **Status Code Categories:**
  - `1xx`: Informational (`101 Switching Protocols`).
  - `2xx`: Success (`200 OK`, `201 Created`, `204 No Content`).
  - `3xx`: Redirection (`301 Moved Permanently`, `302 Found`, `304 Not Modified`).
  - `4xx`: Client Error (`400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`, `429 Too Many Requests`).
  - `5xx`: Server Error (`500 Internal Server Error`, `502 Bad Gateway`, `503 Service Unavailable`, `504 Gateway Timeout`).

### 6.4 HTTPS & TLS 1.3 Handshake Architecture
- HTTPS encrypts HTTP traffic via TLS over TCP port 443.
- Guarantees **Confidentiality** (symmetric AES-GCM encryption), **Integrity** (HMAC/SHA-256), and **Authentication** (X.509 Digital Certificates signed by trusted Certificate Authorities).
- **TLS 1.3 Handshake (1-RTT):**
  1. *ClientHello:* Supported cipher suites + Diffie-Hellman Key Share.
  2. *ServerHello:* Chosen cipher suite + Server Key Share + Digital Certificate + CertificateVerify + Finished.
  3. Client verifies Certificate signature against pre-installed OS root trust store. Both generate matching symmetric session keys!
  4. Encrypted application data flows immediately.

### 6.5 Supporting Application Protocols
- **DHCP (Dynamic Host Configuration Protocol &mdash; UDP 67/68):** Automatic IP assignment via **DORA** sequence:
  1. `Discover` (Client broadcasts `255.255.255.255`).
  2. `Offer` (DHCP Server broadcasts proposed IP).
  3. `Request` (Client requests offered IP).
  4. `Acknowledge` (Server confirms lease duration, default gateway, DNS IP).
- **Email Pipeline:** Client uses **SMTP (TCP 25/587)** to push mail to server; receiver pulls mail from mailbox using **IMAP (TCP 993)** or **POP3 (TCP 995)**.

---

## Module 7: The Master Placement Interview Question
### "What happens under the hood when you type `https://www.google.com` into a web browser and hit Enter?"

```
Step 1: URL Parsing & HSTS Check (Browser checks protocol, port, local HSTS preload list)
     |
Step 2: DNS Resolution Pipeline (Browser Cache -> OS Cache -> Hosts file -> Local DNS Resolver -> Root -> TLD -> Auth)
     |
Step 3: ARP (Address Resolution Protocol): Resolves Default Gateway IP to Router MAC Address
     |
Step 4: TCP 3-Way Handshake (Client SYN -> Server SYN-ACK -> Client ACK on Port 443)
     |
Step 5: TLS 1.3 Cryptographic Handshake (Certificate Validation & Symmetric Key Derivation)
     |
Step 6: HTTP GET Request & Server Processing (Web Server / Reverse Proxy Nginx -> Backend App -> DB)
     |
Step 7: HTTP 200 Response & Browser Rendering (DOM Tree + CSSOM Tree -> Render Tree -> Layout -> Paint)
```

1. **URL Parsing & Input Validation:** Browser parses protocol (`https`), hostname (`www.google.com`), and port (default 443). Verifies HSTS (HTTP Strict Transport Security) list to enforce HTTPS.
2. **DNS Cache Inspection:**
   - Checks Browser DNS Cache (Chrome: `chrome://net-internals/#dns`).
   - Checks OS DNS Cache (`ipconfig /displaydns`).
   - Checks local `hosts` file (`/etc/hosts` or `C:\Windows\System32\drivers\etc\hosts`).
3. **Recursive DNS Lookup:**
   - If uncached, sends UDP query on port 53 to ISP / configured Resolver (`8.8.8.8`).
   - Resolver queries Root Nameserver (`.`), TLD Nameserver (`.com`), and Authoritative Nameserver (`google.com`).
   - Returns IPv4 `A` record (`142.250.190.46`).
4. **ARP Resolution for Default Gateway:**
   - Host checks its local ARP Cache for the MAC address of its default gateway router.
   - If missing, broadcasts an ARP Request: *"Who has 192.168.1.1? Tell 192.168.1.50"*.
   - Router replies with its MAC address (`00:1A:2B:3C:4D:5E`).
5. **TCP 3-Way Handshake:**
   - Client sends `SYN` (Seq = $X$).
   - Server returns `SYN-ACK` (Seq = $Y$, Ack = $X + 1$).
   - Client returns `ACK` (Seq = $X + 1$, Ack = $Y + 1$). TCP socket connection is established!
6. **TLS 1.3 Cryptographic Handshake:**
   - Client sends supported cipher suites and Diffie-Hellman key shares.
   - Server responds with certificate and server key share.
   - Client validates X.509 certificate against trusted root CAs.
   - Shared symmetric session keys generated for encrypted payload.
7. **HTTP Request & Server Response:**
   - Browser sends encrypted `GET / HTTP/2` request with user-agent, headers, and cookies.
   - Server processes request behind reverse proxy / load balancer (Nginx/Envoy) and returns `HTTP/2 200 OK` with HTML payload.
8. **Browser Critical Rendering Path:**
   - Browser parses HTML into DOM Tree.
   - Parses CSS into CSSOM Tree.
   - Combines DOM + CSSOM into **Render Tree**.
   - Executes **Layout (Reflow)** to compute exact pixel geometry.
   - Executes **Paint** to rasterize visual elements onto the screen.

---

## Module 8: Top 30 High-Yield CN Placement Interview Questions
*Source:* Gate Smashers Placement Series (`PLUDPUBNI7KL4`) & Core Campus Interview Questions

1. **Why does TCP use a 3-Way Handshake instead of a 2-Way Handshake?**  
   *Answer:* Two messages can only verify one-way channel health. If an old duplicated SYN segment arrives delayed from a dead connection, a 2-way handshake would force the server to allocate resources and assume a connection is active while the client is oblivious. A 3-way handshake forces mutual acknowledgement of sequence numbers before state allocation.
2. **What is the difference between Flow Control and Congestion Control?**  
   *Answer:* Flow control prevents the sender from overwhelming a specific receiver's limited buffer (governed by advertised `rwnd`). Congestion control prevents the aggregate senders from overwhelming intermediate network routers and switches (governed by sender's calculated `cwnd`).
3. **What is Belady's Anomaly in networking / buffering?**  
   *Answer:* Primarily an OS concept in FIFO page replacement, but in packet buffer caching, allocating larger queue buffers using naive FIFO can paradoxically worsen tail packet latency due to **Bufferbloat**.
4. **Why is DNS primarily deployed over UDP rather than TCP?**  
   *Answer:* DNS query/response packets are typically small ($< 512$ bytes). Establishing a TCP connection requires a 3-way handshake (1 RTT) plus teardown overhead. UDP resolves queries in a single instantaneous round-trip with zero connection state overhead on name servers.
5. **What is the difference between a Hub, a Switch, and a Router?**  
   *Answer:* A Hub (Layer 1) broadcasts bits blindly to all ports (1 collision domain). A Switch (Layer 2) forwards frames intelligently based on destination MAC addresses, isolating collision domains per port. A Router (Layer 3) routes packets between different subnets based on destination IP addresses, isolating broadcast domains.
6. **What is ARP and how does it work?**  
   *Answer:* Address Resolution Protocol maps a known Layer 3 logical IP address to a Layer 2 physical MAC address within the same local broadcast domain via broadcast request and unicast response.
7. **What is RARP and how is it replaced today?**  
   *Answer:* Reverse ARP resolved MAC addresses to IP addresses for diskless workstations. It has been completely superseded by DHCP and BOOTP.
8. **What is the purpose of Subnetting?**  
   *Answer:* Divides a large physical network into multiple smaller, logically independent subnets. Reduces broadcast traffic domains, improves network security, and conserves IP addresses.
9. **Explain the difference between Symmetric and Asymmetric Encryption in HTTPS.**  
   *Answer:* Asymmetric encryption (RSA, ECC, Diffie-Hellman) uses a public/private key pair to securely authenticate the server and negotiate a secret key during the TLS handshake. Symmetric encryption (AES-256-GCM) uses that negotiated shared key to encrypt the actual high-volume data stream at hardware speed.
10. **What is the difference between IPv4 and IPv6 headers?**  
    *Answer:* IPv4 headers are variable (20–60 bytes) and include fields for checksum, flags, and fragmentation. IPv6 headers have a fixed 40-byte size, eliminating the checksum and router-level fragmentation, significantly accelerating router throughput.
11. **Explain the Stop-and-Wait protocol efficiency formula.**  
    *Answer:* Efficiency $\eta = \frac{T_t}{T_t + 2 T_p} = \frac{1}{1 + 2a}$, where $a = \frac{T_p}{T_t} = \frac{\text{Propagation Delay}}{\text{Transmission Delay}}$.
12. **What is the Count-to-Infinity problem in Distance Vector routing?**  
    *Answer:* When a link breaks, neighboring routers update cost vectors incrementally in a loop because they lack global network topology visibility. Mitigated using Split Horizon (never advertise a route back to the neighbor you learned it from) and Poison Reverse.
13. **What is a Proxy Server vs a Reverse Proxy?**  
    *Answer:* A Forward Proxy sits in front of clients, hiding client IPs, caching outbound traffic, and enforcing firewall filters. A Reverse Proxy (Nginx, HAProxy) sits in front of backend servers, handling load balancing, SSL termination, and DDoS mitigation.
14. **What is the Difference between HTTP/1.1 Keep-Alive and HTTP/2 Multiplexing?**  
    *Answer:* HTTP/1.1 Keep-Alive reuses a single TCP connection for sequential requests, suffering from application-level Head-of-Line blocking. HTTP/2 interleaves independent binary streams simultaneously over a single TCP connection without waiting for prior responses.
15. **Why does HTTP/3 switch to UDP?**  
    *Answer:* While HTTP/2 multiplexed streams over TCP, a single dropped TCP packet causes TCP-level Head-of-Line blocking, freezing all multiplexed streams until the missing packet is retransmitted. HTTP/3 builds on QUIC over UDP, ensuring packet loss in one stream never stalls independent streams.
16. **What is MTU vs MSS?**  
    *Answer:* MTU (Maximum Transmission Unit) is the largest Layer 2 physical frame payload (standard Ethernet = 1500 bytes). MSS (Maximum Segment Size) is the maximum Layer 4 TCP data payload ($\text{MSS} = \text{MTU} - 20\text{ bytes IP header} - 20\text{ bytes TCP header} = 1460\text{ bytes}$).
17. **What is the difference between Congestion Window (cwnd) and Receiver Window (rwnd)?**  
    *Answer:* `rwnd` is an explicit buffer limit advertised by the receiver to enforce flow control. `cwnd` is an inferred limit calculated by the sender based on perceived network transit health to prevent network saturation. Effective window = $\min(\text{cwnd}, \text{rwnd})$.
18. **Explain the TCP TIME-WAIT state and why 2 MSL is necessary.**  
    *Answer:* It guarantees that the active closer's final ACK was received by the remote endpoint (otherwise the remote peer re-sends FIN, which is acknowledged). It also ensures all phantom/delayed segments from the connection expire in transit before a new connection rebinds the same port.
19. **What is Anycast routing?**  
    *Answer:* A network addressing technique where a single destination IP address is assigned to multiple physical servers worldwide. BGP automatically routes client packets to the topologically closest server, providing ultra-low latency and DDoS resilience (standard for DNS root servers and CDNs like Cloudflare).
20. **What is the difference between a broadcast domain and a collision domain?**  
    *Answer:* A collision domain is a physical network segment where packets can collide (isolated by switches). A broadcast domain is a logical segment where a broadcast frame (`FF:FF:FF:FF:FF:FF`) reaches every host (isolated only by routers or VLANs).
21. **How does Traceroute work?**  
    *Answer:* Sends a series of UDP or ICMP echo packets with incrementally increasing IP Time-To-Live (TTL) values starting at 1. Each intermediate router decrements TTL; when $\text{TTL} = 0$, the router drops the packet and returns an `ICMP Time Exceeded` message, revealing the router's IP and latency.
22. **What is the difference between Link-State and Distance-Vector routing?**  
    *Answer:* Distance-Vector sends complete routing tables to immediate neighbors based on local views (Bellman-Ford). Link-State floods the status of directly connected links to all routers in the area, allowing every node to construct the complete network graph and calculate shortest paths (Dijkstra).
23. **What is VLAN (Virtual LAN) and IEEE 802.1Q tagging?**  
    *Answer:* Logically segments a physical switch into distinct isolated broadcast domains. 802.1Q inserts a 4-byte VLAN tag into Ethernet frames traversing trunk links between switches.
24. **What is ICMP and why does Ping use it?**  
    *Answer:* Internet Control Message Protocol operates alongside IP (Protocol 1) to transmit network error reports and diagnostics. Ping transmits `ICMP Echo Request` (Type 8) and listens for `ICMP Echo Reply` (Type 0).
25. **What is the difference between Stateful and Stateless Firewalls?**  
    *Answer:* Stateless firewalls filter packets based on static header rules (IP, port) in isolation. Stateful firewalls monitor active connection states (TCP flags, sequence numbers), dynamically permitting outbound reply packets while blocking unsolicited inbound connection attempts.
26. **What is Cookie vs Session in web networking?**  
    *Answer:* A Cookie is a small key-value string stored on the client browser transmitted in HTTP request headers. A Session stores sensitive state data securely on the server, referenced by an opaque session ID stored in the client's cookie.
27. **What is CORS (Cross-Origin Resource Sharing)?**  
    *Answer:* A browser security mechanism that restricts web applications from making asynchronous HTTP requests to a domain, protocol, or port different from the one that served the original web page, regulated via `Access-Control-Allow-Origin` headers.
28. **Explain the difference between TCP Reno and TCP Tahoe.**  
    *Answer:* Tahoe drops the congestion window to 1 MSS on any loss (both timeout and 3 duplicate ACKs). Reno implements Fast Recovery: on 3 duplicate ACKs, it cuts $cwnd$ in half (`cwnd / 2`) and grows linearly without resetting to 1 MSS.
29. **What is BGP Autonomous System (AS)?**  
    *Answer:* A collection of IP routing prefixes under the control of a single administrative entity (ISP, enterprise, university) presenting a unified routing policy to the Internet via Border Gateway Protocol.
30. **What is WebSockets and how does it differ from HTTP polling?**  
    *Answer:* WebSockets initiates with an HTTP Upgrade handshake (`101 Switching Protocols`) and establishes a persistent, bidirectional, full-duplex TCP communication channel with minimal 2-byte framing overhead, replacing expensive HTTP polling loops.
