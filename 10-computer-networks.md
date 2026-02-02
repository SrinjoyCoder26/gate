# 🌐 Computer Networks - Last Minute Notes

## Quick Navigation
- [Network Models](#network-models)
- [Physical Layer](#physical-layer)
- [Data Link Layer](#data-link-layer)
- [Network Layer](#network-layer)
- [Transport Layer](#transport-layer)
- [Application Layer](#application-layer)
- [Network Security](#network-security)

---

# Network Models

## 1. OSI Model

### 💡 Seven Layers (Top to Bottom)
```
Layer 7: Application    - User interface (HTTP, FTP, SMTP)
Layer 6: Presentation   - Data format, encryption, compression
Layer 5: Session        - Session management, synchronization
Layer 4: Transport      - End-to-end delivery (TCP, UDP)
Layer 3: Network        - Routing, logical addressing (IP)
Layer 2: Data Link      - Framing, MAC addressing, error detection
Layer 1: Physical       - Bits on wire, cables, signals
```

### 💡 Memory Trick (Bottom to Top)
```
"Please Do Not Throw Sausage Pizza Away"
Physical → Data Link → Network → Transport → Session → Presentation → Application
```

### 💡 PDU at Each Layer
```
Application/Presentation/Session: Data
Transport: Segment (TCP) / Datagram (UDP)
Network: Packet
Data Link: Frame
Physical: Bits
```

---

## 2. TCP/IP Model

### 💡 Four/Five Layers
```
Application Layer      (OSI 5,6,7)
Transport Layer        (OSI 4)
Internet/Network Layer (OSI 3)
Network Access Layer   (OSI 1,2)
```

### OSI vs TCP/IP
| OSI | TCP/IP |
|-----|--------|
| 7 layers | 4 layers |
| Reference model | Implementation model |
| Session/Presentation separate | Combined in Application |
| Less used practically | Widely used |

---

# Physical Layer

## 1. Transmission Media

### 💡 Types
```
Guided Media:
• Twisted Pair (UTP, STP) - LAN, telephone
• Coaxial Cable - Cable TV, earlier LANs
• Fiber Optic - High speed, long distance

Unguided Media:
• Radio waves - Wi-Fi, cellular
• Microwave - Point-to-point
• Infrared - Short range, line of sight
```

---

## 2. Multiplexing

### 💡 Types
```
FDM (Frequency Division): Different frequency bands
TDM (Time Division): Different time slots
  - Synchronous TDM: Fixed slots
  - Statistical TDM: Dynamic allocation
WDM (Wavelength Division): For fiber optic

CDM (Code Division): Different codes (CDMA)
```

---

## 3. Channel Capacity

### 💡 Nyquist Theorem (Noiseless Channel)
```
Maximum data rate = 2 × B × log₂(L) bits/sec

B = Bandwidth (Hz)
L = Number of signal levels
```

### 💡 Shannon's Theorem (Noisy Channel)
```
Maximum capacity = B × log₂(1 + S/N) bits/sec

B = Bandwidth (Hz)
S/N = Signal-to-Noise ratio
S/N (dB) = 10 × log₁₀(S/N)
```

---

# Data Link Layer

## 1. Framing

### 💡 Methods
```
1. Character Count: Frame starts with count
   Problem: If count corrupted, all following frames lost

2. Byte Stuffing: Start/End flags with escape characters
   Flag: Special byte pattern
   Escape: Before flag in data

3. Bit Stuffing: Flag pattern 01111110
   Stuff 0 after five consecutive 1s in data
```

---

## 2. Error Detection

### 💡 Techniques
```
Parity Bit:
• Single bit added to detect odd number of errors
• Even parity: Total 1s is even
• Odd parity: Total 1s is odd

Checksum:
• Sum of data segments
• Receiver recalculates and compares

CRC (Cyclic Redundancy Check):
• Divide data by generator polynomial
• Append remainder
• Can detect all single, double, odd errors
• Can detect all burst errors ≤ degree of polynomial
```

### 💡 CRC Calculation
```
Given: Data D, Generator G (degree r)

1. Append r zeros to D → D'
2. Divide D' by G using XOR
3. Remainder R has r bits
4. Transmit: D followed by R

Receiver: Divide by G, if remainder = 0, no error
```

### 💡 Hamming Distance
```
Hamming distance: Number of bit positions where two codewords differ

To detect d errors: Need dₘᵢₙ ≥ d + 1
To correct d errors: Need dₘᵢₙ ≥ 2d + 1

Hamming code: Correct single bit errors
For m data bits, r check bits: 2^r ≥ m + r + 1
```

---

## 3. Flow Control

### 💡 Stop-and-Wait
```
Send 1 frame → Wait for ACK → Send next

Efficiency = 1 / (1 + 2a)
Where a = Propagation time / Transmission time

Problems: Low utilization on high bandwidth-delay paths
```

### 💡 Sliding Window Protocol
```
Sender can send multiple frames before ACK
Window size determines how many

Go-Back-N (GBN):
• Sender window: N frames
• Receiver window: 1 frame
• On error: Retransmit from error frame onwards
• Max window size: 2^n - 1 (n = sequence bits)

Selective Repeat (SR):
• Sender window: N frames
• Receiver window: N frames
• On error: Retransmit only error frame
• Max window size: 2^(n-1)
```

### 💡 Efficiency
```
Stop-and-Wait: η = 1 / (1 + 2a)

Sliding Window (W ≥ 1 + 2a): η = 1
Sliding Window (W < 1 + 2a): η = W / (1 + 2a)

Where:
a = Tₚ / Tₜ = (Propagation delay) / (Transmission time)
W = Window size
```

---

## 4. MAC (Medium Access Control)

### 💡 ALOHA
```
Pure ALOHA:
• Send whenever data ready
• Vulnerable time = 2T (T = frame time)
• Max throughput: S = G × e^(-2G) = 0.184 at G = 0.5

Slotted ALOHA:
• Send only at slot boundaries
• Vulnerable time = T
• Max throughput: S = G × e^(-G) = 0.368 at G = 1
```

### 💡 CSMA (Carrier Sense Multiple Access)
```
1-persistent: Sense, if idle send; if busy, wait and send when idle
Non-persistent: Sense, if idle send; if busy, wait random time
P-persistent: Sense, if idle send with probability p

CSMA/CD (Collision Detection):
• Used in Ethernet
• Detect collision, stop, wait random time, retry
• Minimum frame size = 2 × Propagation delay × Bandwidth
• Slot time = 2 × Propagation time

CSMA/CA (Collision Avoidance):
• Used in Wi-Fi
• RTS/CTS handshake to avoid hidden terminal problem
```

---

## 5. Ethernet (IEEE 802.3)

### 💡 Frame Format
```
Preamble (7) | SFD (1) | Dest MAC (6) | Src MAC (6) | Type (2) | Data (46-1500) | CRC (4)

Minimum frame size: 64 bytes (for collision detection)
Maximum frame size: 1518 bytes
```

### MAC Address
```
48 bits (6 bytes)
Format: XX:XX:XX:XX:XX:XX
First 3 bytes: OUI (Organization)
Last 3 bytes: Device specific
```

---

# Network Layer

## 1. IP Addressing

### 💡 IPv4 Classes
| Class | First Bits | Range | Network Bits | Host Bits | Default Mask |
|-------|------------|-------|--------------|-----------|--------------|
| A | 0 | 1-126 | 8 | 24 | 255.0.0.0 |
| B | 10 | 128-191 | 16 | 16 | 255.255.0.0 |
| C | 110 | 192-223 | 24 | 8 | 255.255.255.0 |
| D | 1110 | 224-239 | Multicast |
| E | 1111 | 240-255 | Reserved |

### Special Addresses
```
127.x.x.x: Loopback
0.0.0.0: This network
255.255.255.255: Limited broadcast
Private: 10.x.x.x, 172.16-31.x.x, 192.168.x.x
```

---

## 2. Subnetting

### 💡 CIDR (Classless Inter-Domain Routing)
```
Format: IP/prefix
Example: 192.168.1.0/24

Subnet mask from prefix:
/24 → 255.255.255.0
/26 → 255.255.255.192

Hosts per subnet = 2^(32 - prefix) - 2
(Subtract 2 for network and broadcast addresses)
```

### 💡 Subnetting Steps
```
1. Determine required subnets and hosts
2. Calculate bits needed:
   Subnet bits: ⌈log₂(subnets)⌉
   Host bits: ⌈log₂(hosts + 2)⌉
3. New prefix = original prefix + subnet bits
4. Calculate subnet addresses
```

### Example
```
Given: 192.168.1.0/24, need 4 subnets

Subnet bits needed: ⌈log₂(4)⌉ = 2
New prefix: /26
Hosts per subnet: 2^6 - 2 = 62

Subnets:
192.168.1.0/26   (0-63)
192.168.1.64/26  (64-127)
192.168.1.128/26 (128-191)
192.168.1.192/26 (192-255)
```

---

## 3. Routing Algorithms

### 💡 Distance Vector (Bellman-Ford)
```
• Each router knows distance to neighbors
• Exchange tables with neighbors periodically
• Update: D(v) = min{c(x,v) + D(v)}
• Count-to-infinity problem

Examples: RIP
```

### 💡 Link State (Dijkstra)
```
• Each router knows complete topology
• Flood link state packets
• Calculate shortest path using Dijkstra
• Faster convergence than DV

Examples: OSPF
```

### 💡 Comparison
| Feature | Distance Vector | Link State |
|---------|-----------------|------------|
| Information | Distance to all | Complete topology |
| Exchange with | Neighbors only | All routers |
| Algorithm | Bellman-Ford | Dijkstra |
| Convergence | Slow | Fast |
| Memory | Low | High |
| Bandwidth | Low (periodic) | High (floods) |

---

## 4. IPv6

### 💡 IPv6 Features
```
Address: 128 bits (8 groups of 4 hex digits)
Example: 2001:0db8:85a3:0000:0000:8a2e:0370:7334

No broadcast (uses multicast)
No fragmentation by routers
No checksum (handled by higher layers)
Simplified header
```

---

## 5. Network Address Translation (NAT)

```
Maps private IP:port to public IP:port
Enables multiple devices to share single public IP
Types: Static, Dynamic, PAT (Port Address Translation)
```

---

# Transport Layer

## 1. TCP vs UDP

### 💡 Comparison
| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Connection-oriented | Connectionless |
| Reliability | Reliable (ACKs, retransmission) | Unreliable |
| Ordering | In-order delivery | No ordering |
| Flow Control | Yes (sliding window) | No |
| Congestion Control | Yes | No |
| Header Size | 20-60 bytes | 8 bytes |
| Use Cases | HTTP, FTP, Email | DNS, VoIP, Gaming |

---

## 2. TCP Features

### 💡 TCP Header (20-60 bytes)
```
Source Port (16) | Dest Port (16)
Sequence Number (32)
Acknowledgment Number (32)
Header Length (4) | Reserved (6) | Flags (6) | Window (16)
Checksum (16) | Urgent Pointer (16)
Options (variable)

Flags: URG, ACK, PSH, RST, SYN, FIN
```

### 💡 TCP Connection (3-Way Handshake)
```
Client → Server: SYN (seq = x)
Server → Client: SYN-ACK (seq = y, ack = x+1)
Client → Server: ACK (seq = x+1, ack = y+1)
```

### 💡 TCP Connection Termination (4-Way)
```
A → B: FIN
B → A: ACK
B → A: FIN
A → B: ACK
```

---

## 3. TCP Flow Control

### 💡 Sliding Window
```
Receiver advertises window size
Sender can send up to window size bytes
Window size = min(congestion window, receiver window)
```

---

## 4. TCP Congestion Control

### 💡 Phases
```
Slow Start:
• cwnd starts at 1 MSS
• Double cwnd each RTT (exponential growth)
• Until ssthresh or loss

Congestion Avoidance:
• Increase cwnd by 1 MSS per RTT (linear growth)
• After cwnd reaches ssthresh

Fast Retransmit:
• On 3 duplicate ACKs, retransmit immediately
• Don't wait for timeout

Fast Recovery:
• After fast retransmit
• ssthresh = cwnd/2
• cwnd = ssthresh + 3 MSS
• Linear increase until new loss
```

### 💡 On Timeout
```
ssthresh = cwnd / 2
cwnd = 1 MSS
Enter Slow Start
```

### 💡 On 3 Duplicate ACKs
```
ssthresh = cwnd / 2
cwnd = ssthresh
Enter Congestion Avoidance (Fast Recovery)
```

---

## 5. UDP

### 💡 UDP Header (8 bytes)
```
Source Port (16) | Dest Port (16)
Length (16) | Checksum (16)
```

### Characteristics
```
• No connection establishment
• No guaranteed delivery
• No ordering
• No congestion control
• Low overhead, faster
```

---

## 6. Port Numbers

### 💡 Well-Known Ports
| Port | Protocol | Service |
|------|----------|---------|
| 20, 21 | TCP | FTP (data, control) |
| 22 | TCP | SSH |
| 23 | TCP | Telnet |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 67, 68 | UDP | DHCP |
| 80 | TCP | HTTP |
| 110 | TCP | POP3 |
| 143 | TCP | IMAP |
| 443 | TCP | HTTPS |

---

# Application Layer

## 1. DNS (Domain Name System)

### 💡 DNS Hierarchy
```
Root (.)
  ↓
TLD (.com, .org, .net, .edu)
  ↓
Second Level (google.com)
  ↓
Subdomains (www.google.com)
```

### DNS Record Types
| Type | Description |
|------|-------------|
| A | IPv4 address |
| AAAA | IPv6 address |
| CNAME | Canonical name (alias) |
| MX | Mail exchange |
| NS | Name server |
| PTR | Reverse lookup |
| SOA | Start of authority |

### DNS Resolution
```
Recursive: Resolver does all the work
Iterative: Resolver asks each server in turn

Resolution path:
1. Local cache
2. Local DNS server
3. Root server
4. TLD server
5. Authoritative server
```

---

## 2. HTTP

### 💡 HTTP Methods
```
GET: Retrieve resource
POST: Submit data
PUT: Update/Create resource
DELETE: Remove resource
HEAD: GET without body
OPTIONS: Supported methods
```

### HTTP Status Codes
```
1xx: Informational
2xx: Success (200 OK, 201 Created)
3xx: Redirection (301 Moved, 302 Found, 304 Not Modified)
4xx: Client Error (400 Bad Request, 401 Unauthorized, 404 Not Found)
5xx: Server Error (500 Internal Server Error, 503 Service Unavailable)
```

### HTTP vs HTTPS
```
HTTP: Port 80, Unencrypted
HTTPS: Port 443, Encrypted (TLS/SSL)
```

---

## 3. Email Protocols

### 💡 Protocol Comparison
| Protocol | Port | Direction | Description |
|----------|------|-----------|-------------|
| SMTP | 25 | Send | Simple Mail Transfer Protocol |
| POP3 | 110 | Receive | Download and delete |
| IMAP | 143 | Receive | Sync across devices |

---

## 4. DHCP

### 💡 DORA Process
```
Discover: Client broadcasts to find server
Offer: Server offers IP address
Request: Client requests offered IP
Acknowledge: Server confirms assignment
```

---

# Network Security

## 1. Cryptography Basics

### 💡 Types
```
Symmetric Key: Same key for encryption/decryption
  Examples: AES, DES, 3DES
  Faster, key distribution problem

Asymmetric Key: Public/Private key pair
  Examples: RSA, DSA, ECC
  Slower, solves key distribution
```

---

## 2. Security Protocols

### 💡 TLS/SSL
```
Provides: Confidentiality, Integrity, Authentication
Uses: Both symmetric and asymmetric encryption
Handshake establishes session key
```

### 💡 IPSec
```
Network layer security
Modes:
  Transport: Only payload encrypted
  Tunnel: Entire packet encrypted
Protocols:
  AH: Authentication Header (integrity)
  ESP: Encapsulating Security Payload (encryption + integrity)
```

---

## 3. Firewalls

### 💡 Types
```
Packet Filter: Layer 3/4, inspect headers
Stateful: Track connection state
Application Gateway (Proxy): Layer 7, full inspection
```

---

## Quick Memory Tricks 🧠

1. **OSI Layers**: "Please Do Not Throw Sausage Pizza Away"
2. **TCP 3-Way**: "SYN, SYN-ACK, ACK"
3. **Class A**: First byte 1-126, /8 mask
4. **CIDR /24**: 256 - 2 = 254 hosts
5. **ALOHA efficiency**: Pure = 18%, Slotted = 37%
6. **Stop-Wait**: η = 1/(1+2a)
7. **GBN window**: 2^n - 1, SR window: 2^(n-1)

---

## 💡 Quick Formulas

```
Transmission Time = Packet Size / Bandwidth
Propagation Delay = Distance / Propagation Speed
RTT = 2 × Propagation Delay

Efficiency (Stop-Wait) = 1 / (1 + 2a)
Efficiency (Sliding Window) = min(1, W / (1 + 2a))

Hosts per subnet = 2^(32-prefix) - 2

Nyquist: 2B × log₂L
Shannon: B × log₂(1 + S/N)

ALOHA: Pure S = Ge^(-2G), Slotted S = Ge^(-G)
```

---

## Common Mistakes to Avoid ⚠️

1. Forgetting to subtract 2 for usable hosts (network + broadcast)
2. Confusing transmission delay with propagation delay
3. CSMA/CD for wired (Ethernet), CSMA/CA for wireless (Wi-Fi)
4. TCP uses 3-way handshake to open, 4-way to close
5. On timeout, cwnd = 1; on 3 dup ACKs, cwnd = ssthresh
6. GBN retransmits all from error; SR retransmits only errored
7. IPv6 is 128 bits, not 64
8. DNS uses both TCP and UDP (UDP for queries, TCP for zone transfers)
