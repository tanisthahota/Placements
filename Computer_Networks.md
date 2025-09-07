# Computer Networks 

## Network Fundamentals

### What is a Computer Network?
- Collection of interconnected devices that can communicate and share resources
- Enables data sharing, resource sharing, and communication
- Can be local (LAN) or distributed across large distances (WAN)

### Network Components
- *Nodes*: Devices connected to network (computers, routers, switches)
- *Links*: Physical or wireless connections between nodes
- *Protocols*: Rules governing communication
- *Network Interface Card (NIC)*: Hardware for network connectivity
- *Medium*: Physical pathway for data transmission

### Types of Networks by Size
- *PAN (Personal Area Network)*: Within 10 meters (Bluetooth, USB)
- *LAN (Local Area Network)*: Single building or campus
- *MAN (Metropolitan Area Network)*: City-wide coverage
- *WAN (Wide Area Network)*: Large geographical area
- *Internet*: Global network of networks

### Types of Networks by Topology
- *Bus*: Single cable, all devices connected to it
- *Star*: Central hub with devices connected to it
- *Ring*: Devices connected in circular fashion
- *Mesh*: Every device connected to every other device
- *Tree*: Hierarchical structure
- *Hybrid*: Combination of multiple topologies

## OSI Model (7 Layers)

### Layer 7: Application Layer
- *Purpose*: Interface between user and network
- *Protocols*: HTTP, HTTPS, FTP, SMTP, DNS
- *Examples*: Web browsers, email clients
- *Functions*: Network process to application, user authentication

### Layer 6: Presentation Layer
- *Purpose*: Data translation, encryption, compression
- *Functions*: Format conversion, encryption/decryption, compression
- *Examples*: SSL/TLS, JPEG, GIF, ASCII

### Layer 5: Session Layer
- *Purpose*: Session management between applications
- *Functions*: Session establishment, maintenance, termination
- *Examples*: SQL sessions, RPC, NetBIOS

### Layer 4: Transport Layer
- *Purpose*: End-to-end reliable data transfer
- *Protocols*: TCP, UDP, SCTP
- *Functions*: Segmentation, flow control, error control, multiplexing
- *Port numbers*: Identify specific services/applications

### Layer 3: Network Layer
- *Purpose*: Routing and logical addressing
- *Protocols*: IP, ICMP, ARP
- *Functions*: Routing, logical addressing, path determination
- *Devices*: Routers, Layer 3 switches

### Layer 2: Data Link Layer
- *Purpose*: Node-to-node delivery, error detection
- *Protocols*: Ethernet, WiFi
- *Functions*: Framing, physical addressing, error detection
- *Devices*: Switches, bridges
- *Addressing*: MAC addresses (48-bit)

### Layer 1: Physical Layer
- *Purpose*: Transmission of raw bits
- *Functions*: Bit transmission, physical topology, transmission modes
- *Examples*: Cables, hubs, repeaters, transceivers
- *Specifications*: Voltage levels, timing, physical data rates

## TCP/IP Model (4 Layers)

### Application Layer
- Combines OSI layers 5, 6, and 7
- Direct interface with end user
- Protocols: HTTP, FTP, SMTP, DNS

### Transport Layer
- Same as OSI Transport Layer
- TCP for reliable, UDP for fast transmission
- Port-based addressing

### Internet Layer
- Same as OSI Network Layer
- IP addressing and routing
- Protocols: IP, ICMP, ARP

### Network Access Layer
- Combines OSI Physical and Data Link layers
- Hardware addressing and physical transmission
- Technology specific (Ethernet, WiFi, etc.)

## IP Addressing

### IPv4 Addressing
- *Format*: 32-bit address (4 octets)
- *Notation*: Dotted decimal (192.168.1.1)
- *Total addresses*: ~4.3 billion
- *Classes*:
  - Class A: 1.0.0.0 to 126.255.255.255 (/8)
  - Class B: 128.0.0.0 to 191.255.255.255 (/16)
  - Class C: 192.0.0.0 to 223.255.255.255 (/24)
  - Class D: 224.0.0.0 to 239.255.255.255 (Multicast)
  - Class E: 240.0.0.0 to 255.255.255.255 (Reserved)

### Special IPv4 Addresses
- *127.0.0.1*: Loopback address
- *0.0.0.0*: Default route
- *255.255.255.255*: Broadcast address
- *Private addresses*:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16

### Subnetting
- *Purpose*: Divide large network into smaller subnetworks
- *Subnet Mask*: Identifies network and host portions
- *CIDR Notation*: /24 indicates 24 network bits
- *Benefits*: Better organization, security, reduced broadcast traffic

### IPv6 Addressing
- *Format*: 128-bit address (8 groups of 4 hex digits)
- *Notation*: 2001:db8::1
- *Total addresses*: ~340 undecillion
- *Types*: Unicast, Multicast, Anycast
- *Benefits*: Larger address space, better security, auto-configuration

## Routing and Routing Protocols

### Static vs Dynamic Routing
- *Static*: Manually configured routes, simple but inflexible
- *Dynamic*: Automatically learned routes, adaptive to network changes

### Routing Algorithms
- *Distance Vector*: Routing Information Protocol(RIP), uses hop count
- *Link State*: Open Shortest Path First(OSPF), maintains complete network topology
- *Path Vector*: Broader Gateway Protocol(BGP), considers path information

### Interior Gateway Protocols (IGP)
- *RIP (Routing Information Protocol)*:
  - Distance vector, hop count metric (max 15)
  - Updates every 30 seconds
  - Simple but limited scalability

- *OSPF (Open Shortest Path First)*:
  - Link state protocol
  - Uses Dijkstra's algorithm
  - Fast convergence, supports VLSM

- *EIGRP (Enhanced Interior Gateway Routing Protocol)*:
  - Cisco proprietary (now open standard)
  - Hybrid protocol
  - Fast convergence, minimal bandwidth usage

### Exterior Gateway Protocols (EGP)
- *BGP (Border Gateway Protocol)*:
  - Path vector protocol
  - Used between autonomous systems
  - Policy-based routing decisions

## Transport Layer Protocols

### TCP (Transmission Control Protocol)
- *Characteristics*: Connection-oriented, reliable, ordered delivery
- *Features*:
  - Three-way handshake (SYN, SYN-ACK, ACK)
  - Flow control (sliding window)
  - Congestion control
  - Error detection and recovery
  - Full-duplex communication

### UDP (User Datagram Protocol)
- *Characteristics*: Connectionless, unreliable, fast
- *Features*:
  - No handshake required
  - No guarantee of delivery or ordering
  - Lower overhead than TCP
  - Used for real-time applications

### TCP vs UDP Comparison
| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Connection-oriented | Connectionless |
| Reliability | Reliable | Unreliable |
| Ordering | Yes | No |
| Flow Control | Yes | No |
| Overhead | High | Low |
| Use Cases | Web, Email, File Transfer | DNS, DHCP, Streaming |

## Application Layer Protocols

### HTTP/HTTPS
- *HTTP*: Hypertext Transfer Protocol, port 80
- *HTTPS*: HTTP Secure, port 443
- *Methods*: GET, POST, PUT, DELETE, PATCH
- *Status Codes*: 200 (OK), 404 (Not Found), 500 (Server Error)

### DNS (Domain Name System)
- *Purpose*: Translate domain names to IP addresses
- *Port*: 53 (UDP for queries, TCP for zone transfers)
- *Hierarchy*: Root servers, TLD servers, authoritative servers
- *Record Types*: A, AAAA, CNAME, MX, NS, PTR

### FTP (File Transfer Protocol)
- *Purpose*: File transfer between systems
- *Ports*: 21 (control), 20 (data)
- *Modes*: Active vs Passive
- *Security*: Plain text, use SFTP or FTPS for security

### SMTP/POP3/IMAP
- *SMTP*: Simple Mail Transfer Protocol, port 25/587
- *POP3*: Post Office Protocol, port 110/995
- *IMAP*: Internet Message Access Protocol, port 143/993

### DHCP (Dynamic Host Configuration Protocol)
- *Purpose*: Automatically assign IP addresses
- *Process*: Discover, Offer, Request, Acknowledge (DORA)
- *Lease time*: Duration for which IP is assigned

## Network Devices

### Physical Layer Devices
- *Hub*: Multi-port repeater, operates at Physical layer
- *Repeater*: Amplifies signals, extends cable length

### Data Link Layer Devices
- *Bridge*: Connects two LAN segments, filters traffic
- *Switch*: Multi-port bridge with learning capabilities
- *Features*: MAC address table, collision domain separation

### Network Layer Devices
- *Router*: Connects different networks, operates at Network layer
- *Functions*: Routing, packet filtering, NAT
- *Layer 3 Switch*: Combines switching and routing capabilities

### Modern Network Devices
- *Firewall*: Security device filtering traffic based on rules
- *Load Balancer*: Distributes incoming requests across servers
- *Proxy Server*: Intermediary for client-server communication
- *Gateway*: Connects networks using different protocols

## Wireless Networks

### WiFi Standards (IEEE 802.11)
- *802.11a*: 5 GHz, 54 Mbps
- *802.11b*: 2.4 GHz, 11 Mbps
- *802.11g*: 2.4 GHz, 54 Mbps
- *802.11n*: 2.4/5 GHz, 600 Mbps, MIMO
- *802.11ac*: 5 GHz, 6.93 Gbps
- *802.11ax (WiFi 6)*: 2.4/5 GHz, 9.6 Gbps

### WiFi Security
- *WEP*: Weak encryption, easily broken
- *WPA*: Improved security over WEP
- *WPA2*: Strong encryption using AES
- *WPA3*: Latest standard with enhanced security

### Cellular Networks
- *1G*: Analog voice
- *2G*: Digital voice, SMS (GSM, CDMA)
- *3G*: Mobile internet (UMTS, CDMA2000)
- *4G/LTE*: High-speed mobile broadband
- *5G*: Ultra-fast, low latency, IoT support

## Network Security

### Common Threats
- *Malware*: Viruses, worms, trojans
- *DDoS*: Distributed Denial of Service attacks
- *Man-in-the-Middle*: Intercepting communication
- *Phishing*: Social engineering attacks
- *SQL Injection*: Database attacks through web applications

### Security Mechanisms
- *Encryption*: Data confidentiality (AES, RSA)
- *Authentication*: Verify user identity (passwords, certificates)
- *Authorization*: Control access to resources
- *Integrity*: Ensure data hasn't been modified (hash functions)
- *Non-repudiation*: Prevent denial of actions (digital signatures)

### Security Protocols
- *SSL/TLS*: Secure web communication
- *IPSec*: Network layer security
- *SSH*: Secure remote access
- *VPN*: Virtual Private Network for secure remote access

### Firewalls
- *Packet Filtering*: Examine individual packets
- *Stateful Inspection*: Track connection states
- *Application Layer*: Deep packet inspection
- *Next-Generation*: Advanced threat protection

## Network Performance 

### Performance Metrics
- *Bandwidth*: Maximum data transfer rate
- *Throughput*: Actual data transfer rate
- *Latency*: Time for data to travel from source to destination
- *Jitter*: Variation in latency
- *Packet Loss*: Percentage of lost packets

### Quality of Service (QoS)
- *Purpose*: Prioritize network traffic based on requirements
- *Techniques*:
  - Traffic shaping
  - Packet prioritization
  - Bandwidth allocation
  - Queue management

### Congestion Control
- *TCP Congestion Control*: Slow start, congestion avoidance
- *Traffic Shaping*: Control data transmission rate
- *Load Balancing*: Distribute traffic across multiple paths



## Network Calculations

### Subnetting Calculations
- *Number of subnets*: 2^n (n = borrowed bits)
- *Hosts per subnet*: 2^h - 2 (h = host bits)
- *Subnet increment*: 256 - subnet mask value

### Example: 192.168.1.0/26
- Network bits: 26, Host bits: 6
- Subnets: 2^2 = 4
- Hosts per subnet: 2^6 - 2 = 62
- Subnets: 192.168.1.0/26, 192.168.1.64/26, 192.168.1.128/26, 192.168.1.192/26

### Bandwidth Calculations
- *Throughput*: Consider protocol overhead
- *Utilization*: (Used bandwidth / Total bandwidth) × 100
- *Latency calculations*: Propagation + transmission + processing + queuing delays
