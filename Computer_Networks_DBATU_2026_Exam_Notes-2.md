# BTCOC602 — Computer Networks
## DBATU Exam-Ready Notes (Final Structure)

> Format for every question: **Definition → Diagram (if needed) → Important Points (full answer) → Table (if applicable) → Solved Example (if numerical) → Conclusion → Exam Keywords.**

---

# UNIT 1: Introduction & Physical Layer

---

## 1. Compare OSI Model and TCP/IP Model

### Definition
OSI Model is a 7-layer reference model for network communication. TCP/IP Model is a 4-layer model that is actually used to run the Internet.

### Diagram
```
+----------------------+       +----------------------+
|   Application          |       |                        |
+----------------------+       |    Application         |
|   Presentation          |  --->|                        |
+----------------------+       +----------------------+
|   Session                |       |                        |
+----------------------+       +----------------------+
|   Transport              | ---->|    Transport             |
+----------------------+       +----------------------+
|   Network                  | ---->|    Internet               |
+----------------------+       +----------------------+
|   Data Link                |       |                        |
+----------------------+       |    Network Access         |
|   Physical                  |       |                        |
+----------------------+       +----------------------+
      OSI (7 Layers)                 TCP/IP (4 Layers)
```

### Important Points
- **OSI Model** has **7 layers**: Physical, Data Link, Network, Transport, Session, Presentation, Application. It is a **reference model** used to design and understand network systems.
- **TCP/IP Model** has **4 layers**: Network Access, Internet, Transport, Application. It is the model that the **real Internet** actually uses.
- OSI is not tied to one protocol (protocol independent); TCP/IP is built around real protocols like TCP, IP, UDP.
- OSI keeps **Session** and **Presentation** as separate layers; TCP/IP merges them into the single Application layer.
- Reliability (guaranteed, ordered delivery) is mainly provided by the **Transport Layer** in both models.

### Comparison Table
| Feature | OSI Model | TCP/IP Model |
|---|---|---|
| Layers | 7 | 4 |
| Developed by | ISO | DARPA/Internet |
| Nature | Theoretical | Practical |
| Session/Presentation | Separate layers | Merged in Application |
| Usage today | Teaching/reference | Real Internet |

### Conclusion
OSI is used to **understand** networking layer-by-layer, while TCP/IP is what **actually runs** the Internet today.

### Exam Keywords
OSI, ISO, Layer, Protocol, Interface, TCP/IP, Reference Model, Session Layer, Presentation Layer

---

## 2. Explain Design Issues of Network Layers (Protocol Hierarchy)

### Definition
Design issues are common problems that every layer must solve, such as addressing, error control, and flow control.

### Diagram
```
+------------------------------+
|  Layer N (uses a protocol)      |
+------------------------------+
          | Service
          v
+------------------------------+
|  Layer N-1                      |
+------------------------------+
```

### Important Points
- **Addressing** — every layer needs a way to identify the sender and receiver.
- **Error Control** — since the medium is not perfect, errors must be detected and corrected.
- **Flow Control** — prevents a fast sender from overwhelming a slow receiver.
- **Multiplexing/Demultiplexing** — allows many logical connections to share one physical connection.
- **Routing** — best path is chosen when multiple paths exist between source and destination.
- **Protocol vs Service**: **Service** = what a layer offers to the layer above it (the job). **Protocol** = the rules used by peer layers to do that job (how it is done).

### Conclusion
Every layer, no matter its job, must solve the same core problems: addressing, error control, flow control, multiplexing, and routing.

### Exam Keywords
Protocol, Service, Layer Arrangement, Addressing, Flow Control, Error Control, Multiplexing, Routing

---

## 3. Explain Applications of Computer Networks

### Definition
Computer network applications are the real-world uses of connecting computers together to share resources and exchange information.

### Important Points
- **Resource Sharing** — many users can share hardware like printers, scanners, and storage over a network.
- **Communication** — email, video calls, instant messaging connect people across the world instantly.
- **Business Applications** — remote work, video conferencing, online meetings, and shared company databases.
- **E-Commerce** — online shopping, net banking, online bill payments all run over networks.
- **Access to Remote Information** — web browsing, cloud storage, online databases, digital libraries.
- **Entertainment** — video/music streaming, online gaming, social networking sites.

### Conclusion
Computer networks are used almost everywhere today — in business, education, banking, entertainment, and communication — making them essential to modern life.

### Exam Keywords
Resource Sharing, Communication, E-Commerce, Remote Access, Cloud, Entertainment, Business Application

---

## 4. Explain Types of Computer Networks (LAN, MAN, WAN)

### Definition
Networks are classified by their geographical coverage area into LAN, MAN, and WAN.

### Diagram
```
LAN (small)   -->   MAN (city-wide)   -->   WAN (country/world-wide)
[Home/Office]        [Connects multiple LANs    [Connects multiple MANs
                       in a city]                 across countries]
```

### Important Points
- **LAN (Local Area Network)** — covers a small area like a home, office, or single building. High speed, low cost, owned privately. Example: office network connected via Ethernet/Wi-Fi.
- **MAN (Metropolitan Area Network)** — covers a city or town, connecting multiple LANs together. Example: cable TV network, city-wide college network.
- **WAN (Wide Area Network)** — covers a large geographical area, even across countries. Uses leased telephone lines, satellites. Example: the Internet itself.
- As area covered increases (LAN → MAN → WAN), speed generally decreases and cost/complexity increases.

### Comparison Table
| Feature | LAN | MAN | WAN |
|---|---|---|---|
| Coverage | Building/campus | City | Country/World |
| Speed | Very high | High | Comparatively lower |
| Ownership | Private | Private/Public | Public/Multiple orgs |
| Example | Office network | Cable TV network | Internet |

### Conclusion
LAN, MAN, and WAN differ mainly in the geographical area they cover, which directly affects their speed, cost, and ownership.

### Exam Keywords
LAN, MAN, WAN, Geographical Area, Ethernet, Internet

---

## 5. Compare Connection-Oriented and Connectionless Services

### Definition
Connection-oriented service sets up a dedicated path before sending data. Connectionless service sends data directly without any prior setup.

### Diagram
```
Connection-Oriented:               Connectionless:
Sender --- Setup ---> Receiver     Sender ---> Data Packet ---> Receiver
Sender --- Data  ---> Receiver     (No setup, no guaranteed order)
Sender --- Teardown-> Receiver
```

### Important Points
- **Connection-Oriented Service** — a connection is established first (like a phone call), data is sent in order, and the connection is closed after use. Example: **TCP**.
- **Connectionless Service** — no connection setup; data (datagrams) is sent independently and may arrive out of order or get lost. Example: **UDP**.
- Connection-oriented is **reliable** but slower due to setup overhead; connectionless is **faster** but unreliable.
- Connection-oriented service is good for applications needing accuracy (file transfer); connectionless is good for applications needing speed (video streaming).

### Comparison Table
| Feature | Connection-Oriented | Connectionless |
|---|---|---|
| Setup | Required before data transfer | Not required |
| Reliability | Reliable, ordered delivery | Unreliable, no order guarantee |
| Speed | Slower | Faster |
| Example Protocol | TCP | UDP |
| Analogy | Phone call | Postal mail |

### Conclusion
Connection-oriented service prioritizes reliability and order, while connectionless service prioritizes speed and simplicity.

### Exam Keywords
Connection-Oriented, Connectionless, TCP, UDP, Virtual Circuit, Datagram

---

# UNIT 3: Data Link Layer

---

## 1. Explain Framing (Byte Stuffing and Bit Stuffing)

### Definition
Framing means breaking the bit stream into separate frames so the receiver knows where one frame ends and the next begins.

### Diagram
```
+------+------+------+--- ... ---+------+
| FLAG | Data | Data |    ...    | FLAG |
+------+------+------+--- ... ---+------+
```

### Important Points
- **Byte/Character Count method** — first field of the frame header states the number of bytes in the frame. Problem: if this count field is damaged, the receiver loses synchronization completely (cascading failure).
- **Byte Stuffing (Character Stuffing)** — special **FLAG bytes** (e.g. `01111110`) mark the start and end of every frame. If real data contains a byte equal to FLAG or ESC, an extra **ESC byte** is inserted before it. The receiver removes stuffed ESC bytes while reading.
- **Bit Stuffing** — uses a bit pattern `01111110` as the flag. The sender inserts a **0** after every **five consecutive 1s** in the data, so the flag pattern never appears accidentally inside real data. The receiver removes stuffed 0s after every run of five 1s.

### Solved Example — Byte Stuffing
Given: A = 01000111, B = 11100011, FLAG = 01111110, ESC = 11100000

Frame to send: **A B ESC FLAG**
```
Final stream: FLAG A B ESC-ESC ESC-FLAG FLAG
```

### Solved Example — Bit Stuffing
Data = `110111111111100`
```
After stuffing: 11011111011111000
```

### Conclusion
Byte stuffing works on whole bytes using ESC characters; bit stuffing works on individual bits by inserting extra 0s — both prevent the flag pattern from appearing accidentally inside real data.

### Exam Keywords
Framing, Byte Stuffing, Bit Stuffing, FLAG, ESC, Byte Count, Frame Synchronization

---

## 2. Explain Data Link Layer Design Issues

### Definition
Data Link Layer design issues are the core problems this layer must solve: framing, addressing, flow control, error control, and access control.

### Important Points
- **Framing** — the layer breaks the raw bit stream from the physical layer into manageable frames.
- **Physical Addressing** — MAC addresses are added to frame headers to identify source and destination on the same network.
- **Flow Control** — ensures a fast sender does not overwhelm a slow receiver (e.g., sliding window).
- **Error Control** — detects and corrects errors using techniques like CRC, checksum, or Hamming code.
- **Access Control** — when multiple devices share the same channel, this layer decides who transmits when (e.g., CSMA/CD in Ethernet, token passing in Token Ring).

### Conclusion
The Data Link Layer's core job is to convert an unreliable physical link into a reliable, well-framed, and properly addressed link for the Network Layer above it.

### Exam Keywords
Data Link Layer, Framing, Flow Control, Error Control, Access Control, MAC Address

---

## 3. Explain Services Provided by Data Link Layer

### Definition
The Data Link Layer offers specific services to the Network Layer above it, which vary in reliability and connection type.

### Diagram
```
Network Layer
      ^
      | Service
+-----------------+
| Data Link Layer  |
+-----------------+
      | Frames
      v
Physical Layer
```

### Important Points
- **Unacknowledged Connectionless Service** — sender sends frames with no acknowledgment and no connection setup; receiver does not confirm receipt. Used where errors can be fixed at higher layers (e.g., Ethernet).
- **Acknowledged Connectionless Service** — no connection is set up, but every frame sent is individually acknowledged. Useful for unreliable channels like wireless links.
- **Acknowledged Connection-Oriented Service** — a connection is set up first, data is sent as a numbered sequence of frames, and every frame is guaranteed to be delivered exactly once, in order.
- These services allow the Network Layer above to rely on a certain level of reliability without worrying about the physical medium's errors.

### Conclusion
The Data Link Layer can provide three levels of service (unacknowledged connectionless, acknowledged connectionless, acknowledged connection-oriented), giving flexibility based on how reliable the underlying physical link is.

### Exam Keywords
Unacknowledged Service, Acknowledged Service, Connection-Oriented, Connectionless, Network Layer

---

## 4. Explain Flow Control and Error Control

### Definition
Flow control matches the speed of the sender and receiver. Error control detects and corrects errors that occur during transmission.

### Important Points
- **Flow Control** ensures a fast sender does not overwhelm a slow receiver's buffer.
  - **Stop-and-Wait** — sender sends one frame and waits for its acknowledgment before sending the next.
  - **Sliding Window** — sender can send multiple frames (up to window size) before needing an acknowledgment, improving efficiency.
- **Error Control** ensures data received is the same as data sent.
  - **Error Detection** — methods like Parity Check, Checksum, and CRC detect if an error occurred.
  - **Error Correction** — methods like Hamming Code can also correct the error, not just detect it.
  - **ARQ (Automatic Repeat Request)** — if an error is detected, the receiver requests retransmission (e.g., Stop-and-Wait ARQ, Go-Back-N ARQ, Selective Repeat ARQ).

### Comparison Table
| Feature | Flow Control | Error Control |
|---|---|---|
| Purpose | Match sender/receiver speed | Detect/correct transmission errors |
| Techniques | Stop-and-Wait, Sliding Window | Parity, Checksum, CRC, Hamming Code |
| Goal | Prevent buffer overflow | Ensure data accuracy |

### Conclusion
Flow control and error control work together to make the Data Link Layer's frame delivery both efficient (no overwhelmed receiver) and accurate (no undetected errors).

### Exam Keywords
Flow Control, Error Control, Stop-and-Wait, Sliding Window, ARQ, Parity, Checksum

---

## 5. Explain CRC (Cyclic Redundancy Check)

### Definition
CRC is an error detection method that uses binary (modulo-2) division to generate a check code sent along with data.

### Diagram
```
Message + r zeros
      |
      v  (XOR divide by Generator G)
+-----------------+
| Modulo-2 Division |
+-----------------+
      |
      v
   Remainder = CRC bits
      |
      v
Transmitted Codeword = Message + CRC
```

### Important Points
- Let message = **M**, generator = **G** (degree r, i.e., r+1 bits).
- Append **r zeros** to M.
- Divide using **XOR (modulo-2) division** — no borrow/carry.
- The remainder (r bits) is the **CRC code**.
- **Transmitted Codeword = M + CRC** (remainder replaces appended zeros).
- **At Receiver:** divide received codeword by the same G. Remainder = 0 → No error. Remainder ≠ 0 → Error detected.

### Solved Example
**Given:** Message = `1101011` (7 bits), Generator = `1101` (4 bits, degree 3)

- **Step 1:** Append 3 zeros → `1101011000`
- **Step 2:** Perform modulo-2 (XOR) division of `1101011000` by `1101`.
- **Step 3:** The obtained remainder (3 bits) is the CRC code. Suppose remainder = `100`.
- **Step 4:** Transmitted Codeword = Message + CRC = `1101011` + `100` = **`1101011100`**
- **Step 5 (Check at Receiver):** Divide received codeword `1101011100` by `1101` again. Remainder = `000` → accepted, no error. Remainder ≠ `000` → error detected, request retransmission.

### Conclusion
CRC detects errors reliably using polynomial division; the method (append zeros → XOR divide → attach remainder) stays the same for any message/generator given in the exam.

### Exam Keywords
CRC, Generator Polynomial, Modulo-2 Division, XOR, Remainder, Checksum, Error Detection

---

## 6. Explain Go-Back-N ARQ

### Definition
Go-Back-N ARQ is a sliding window protocol where the sender sends multiple frames without waiting for each ACK, but resends all frames from the error point if a frame is lost.

### Diagram
```
Sender:    0    1    2    3    4    5    6    7
                                        X    X   <- lost
Receiver: ACK1 ACK2 ACK3 ACK4 ACK5 ACK6 (expects frame 6)
                                    |
                Sender goes back and resends: 6, 7
```

### Important Points
- Sender can send up to **window size N** frames without waiting for individual acknowledgments, improving efficiency over stop-and-wait.
- **Cumulative ACK:** ACK number k means "frames up to k-1 received correctly; expecting frame k next."
- Receiver accepts frames only in correct sequence; any out-of-order frame is **discarded**, even if error-free.
- If frames are lost, sender **retransmits all frames from the lost frame onward** — this is why it's called "Go-Back-N."

### Solved Example
Sender sends 8 frames, numbered 0 to 7. Receiver sends **ACK number 6**.
- ACK 6 means frames 0-5 were received correctly; frame 6 is expected next.
- **Answer: Frames 6 and 7 (2 frames) must be retransmitted.**

### Conclusion
Go-Back-N improves efficiency over stop-and-wait by allowing multiple frames in flight, but wastes bandwidth by resending correctly-received frames after an error point.

### Exam Keywords
Go-Back-N, ARQ, Sliding Window, Cumulative ACK, Retransmission, Sequence Number

---

# UNIT 4: Network Layer

---

## 1. Compare IPv4 and IPv6

### Definition
IPv4 is the older Internet addressing system using 32-bit addresses. IPv6 is the newer system using 128-bit addresses.

### Important Points
- IPv4 uses a **32-bit address**, giving about 4.3 billion addresses, written in dotted decimal (e.g., 192.168.1.1).
- IPv6 uses a **128-bit address**, giving a virtually unlimited address space, written in hexadecimal, colon-separated (e.g., 2001:db8::1).
- IPv4 header is complex and variable-length with a checksum field; IPv6 header is **simplified and fixed at 40 bytes**, with no checksum, for faster router processing.
- IPv4 security (IPSec) is optional; IPv6 has **built-in IPSec support**.
- IPv4 fragmentation happens at routers and sender; IPv6 fragmentation happens **only at the sending host**.

### Comparison Table
| Feature | IPv4 | IPv6 |
|---|---|---|
| Address length | 32 bits | 128 bits |
| Address space | ~4.3 billion | Practically unlimited |
| Header | Complex, variable, has checksum | Simplified, fixed 40 bytes, no checksum |
| Security | Optional (IPSec add-on) | Built-in IPSec support |
| Fragmentation | By routers and sender | Only by sending host |
| Notation | Dotted decimal | Hex, colon-separated |

### Conclusion
IPv6 solves IPv4's address shortage problem with a much larger address space, simpler header, and built-in security.

### Exam Keywords
IPv4, IPv6, Address Space, Header, IPSec, Fragmentation, Address Exhaustion

---

## 2. Compare TCP and UDP

### Definition
TCP is a reliable, connection-oriented transport protocol. UDP is a fast, connectionless transport protocol.

### Important Points
- **TCP (Transmission Control Protocol)** is connection-oriented — a connection is set up (3-way handshake) before data transfer, and provides **reliable delivery** using acknowledgements, sequence numbers, and retransmission of lost data. It guarantees data arrives **in the correct order**.
- **UDP (User Datagram Protocol)** is connectionless — data is sent directly without setting up a connection. It is **unreliable**; no guarantee of delivery or order, and no retransmission.
- UDP has a smaller header (8 bytes) than TCP (20 bytes), making it faster with less overhead.
- **TCP is used for:** web browsing (HTTP), email, file transfer — where accuracy matters.
- **UDP is used for:** video streaming, online gaming, DNS — where speed matters more than perfection.

### Comparison Table
| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliability | Reliable (ACK, retransmission) | Unreliable (no ACK) |
| Speed | Slower | Faster |
| Ordering | Data arrives in order | No ordering guarantee |
| Header size | 20 bytes | 8 bytes |
| Usage | Web (HTTP), Email, File transfer | Video streaming, DNS, Gaming |

### Conclusion
TCP trades speed for reliability; UDP trades reliability for speed. The choice depends on whether the application needs guaranteed delivery or fast real-time transfer.

### Exam Keywords
TCP, UDP, Connection-Oriented, Connectionless, Reliability, Handshake, Header

---

## 3. Compare Distance Vector Routing and Link State Routing

### Definition
Distance Vector Routing shares distance tables with neighbors only. Link State Routing shares the full network map with all routers, then runs Dijkstra's Algorithm.

### Diagram
```
Distance Vector:                  Link State:
A ---> shares table ---> B        A ---> floods info ---> ALL routers
(only with neighbor)              (every router builds full map)
```

### Important Points
- **Distance Vector Routing**: Each router keeps a table of (destination, distance, next-hop), shared only with **direct neighbors**. Uses **Bellman-Ford**: new_distance = min(own_distance, neighbor_distance + cost). Main drawback: **Count-to-Infinity problem** — when a link fails, routers slowly increase distance estimates instead of quickly detecting the failure. Solved using **Split Horizon**.
- **Link State Routing**: Each router discovers neighbor costs, then **floods** this to every router. Every router builds a full topology map and runs **Dijkstra's Algorithm** independently to compute shortest paths. More overhead due to flooding, but converges faster and is more robust to loops.

### Comparison Table
| Feature | Distance Vector | Link State |
|---|---|---|
| Info shared | Distance to all destinations | Cost to direct neighbors |
| Shared with | Only neighbors | All routers (flooding) |
| Algorithm | Bellman-Ford | Dijkstra's |
| Convergence | Slow | Fast |
| Main problem | Count-to-Infinity | High flooding overhead |
| Example protocol | RIP | OSPF |

### Conclusion
Link State converges faster and is more robust than Distance Vector, at the cost of higher flooding overhead.

### Exam Keywords
Distance Vector, Link State, Bellman-Ford, Dijkstra's Algorithm, Flooding, Count-to-Infinity, RIP, OSPF

---

## 4. Explain Quality of Service (QoS)

### Definition
Quality of Service (QoS) is a set of techniques used to guarantee a certain level of performance (speed, reliability) to specific network traffic.

### Important Points
- **Reliability** — how error-free the data delivery is; critical applications (email, file transfer) need high reliability.
- **Delay** — time taken for data to travel from sender to receiver; low delay is critical for voice/video calls.
- **Jitter** — variation in delay between packets; high jitter disturbs live audio/video streaming.
- **Bandwidth** — amount of data that can be transmitted per second; video streaming needs high bandwidth.
- **Techniques to achieve QoS**: Traffic Shaping (Leaky Bucket, Token Bucket), Scheduling (priority to important packets), Resource Reservation (reserving bandwidth in advance), Admission Control (accepting a connection only if resources are available).

### Comparison Table
| QoS Parameter | Meaning | Example Where Critical |
|---|---|---|
| Reliability | Error-free delivery | Email, file transfer |
| Delay | Time to deliver | Video/voice calls |
| Jitter | Delay variation | Live streaming |
| Bandwidth | Data rate | Video streaming |

### Conclusion
QoS ensures that important or delay-sensitive traffic (like video calls) gets the network resources it needs, instead of all traffic being treated equally.

### Exam Keywords
QoS, Reliability, Delay, Jitter, Bandwidth, Traffic Shaping, Resource Reservation

---

## 5. Explain Leaky Bucket Algorithm

### Definition
The Leaky Bucket Algorithm is a traffic-shaping technique that converts bursty incoming traffic into a smooth, constant-rate output.

### Diagram
```
Bursty data in
   | | |
+---------+
| Bucket  |
+---------+
     |
     | constant leak rate
     v
 Smooth output
```

### Important Points
- Works like a bucket with a small hole at the bottom — water (data) is poured in irregularly, but leaks out at a **constant, fixed rate**.
- If the bucket becomes full, extra incoming packets are **discarded**.
- Converts bursty traffic into a **smooth, constant-rate output stream**, enforcing a strict output rate no matter how bursty the input is.
- Simple to implement, but rigid — it cannot allow any burst even if the network has spare capacity at that moment.

### Conclusion
Leaky Bucket is best used when a network needs a strictly constant, predictable output rate regardless of how bursty the input traffic is.

### Exam Keywords
Leaky Bucket, Traffic Shaping, Constant Rate, Congestion Control, Packet Discard

---

## 6. Explain Token Bucket Algorithm

### Definition
The Token Bucket Algorithm is a traffic-shaping technique that allows controlled bursts of data while still keeping the average rate within a limit.

### Diagram
```
Tokens added
at fixed rate
+---------+
| Tokens  |<- packet needs
| Bucket  |   a token to go
+---------+
     |
     v
Bursty output allowed
```

### Important Points
- Tokens are generated at a **fixed rate** and stored in a bucket, up to a maximum capacity.
- A packet can only be transmitted if a **token is available** — one token is consumed per packet (or per byte).
- If the host was idle and tokens accumulated, a **burst of packets** can be sent all at once, up to the number of available tokens.
- Unlike Leaky Bucket, Token Bucket **allows burstiness** while still bounding the long-term average rate.

### Comparison Table
| Feature | Leaky Bucket | Token Bucket |
|---|---|---|
| Output rate | Fixed, constant | Variable (allows bursts) |
| Burst handling | Smooths out completely | Allows burst if tokens saved |
| Flexibility | Rigid | More flexible |

### Conclusion
Token Bucket is more flexible than Leaky Bucket because it allows bursty traffic when tokens have accumulated, making better use of available network capacity.

### Exam Keywords
Token Bucket, Traffic Shaping, Burst, Congestion Control, Token Rate

---

# UNIT 5: Application Layer & Network Security

---

## 1. Explain DNS (Domain Name System)

### Definition
DNS (Domain Name System) translates human-readable domain names into IP addresses.

### Diagram — Name Resolution Steps
```
Browser
   |  "IP of www.example.com?"
   v
Local DNS Resolver (checks cache)
   |
   v
Root Server ---> refers to TLD Server (.com)
   |
   v
TLD Server ---> refers to Authoritative Server
   |
   v
Authoritative Server ---> returns IP address
   |
   v
Resolver caches it, sends IP to Browser
```

### Important Points
- **DNS** is a **distributed, hierarchical database** — no single server holds all records.
- **Hierarchy:** **Root Servers** (top level, know where TLD servers are) → **TLD Servers** (handle .com, .org, .in) → **Authoritative Name Servers** (hold actual records for a specific domain).
- **Name Resolution Process:** Browser asks the local resolver → resolver checks cache, else queries a root server → root refers to TLD server → TLD refers to authoritative server → authoritative server returns the IP → resolver caches it and returns it to the browser.
- **Multiple IPs for one name:** Yes, common with **load balancing (round-robin DNS)** and **CDNs**, mapping one domain to many servers for speed and redundancy.
- DNS mainly uses **UDP port 53** for queries.

### Conclusion
DNS works like a phonebook for the Internet, resolving names to IPs through a hierarchical chain of servers.

### Exam Keywords
DNS, Root Server, TLD, Authoritative Server, Name Resolution, Load Balancing

---

## 2. Explain HTTP (HyperText Transfer Protocol)

### Definition
HTTP is the application layer protocol used to transfer web pages between a client (browser) and a web server.

### Diagram
```
CLIENT (Browser)                      SERVER
     |----- HTTP Request (GET) ------->|
     |<---- HTTP Response (HTML) ------|
```

### Important Points
- HTTP works on a **request-response** model, using **port 80** (HTTPS uses port 443 for secure browsing).
- It is a **stateless protocol** — each request is independent; the server does not remember previous requests.
- **HTTP Methods**: **GET** (retrieve data), **POST** (submit data), **PUT** (update a resource), **DELETE** (remove a resource).
- **Non-Persistent HTTP** — a new TCP connection is opened for every single request/response, then closed; slower due to repeated connection setup.
- **Persistent HTTP** — the same TCP connection is reused for multiple requests/responses, reducing overhead and improving speed. This is the default in HTTP/1.1.

### Comparison Table
| Feature | Non-Persistent HTTP | Persistent HTTP |
|---|---|---|
| Connection | New connection per request | Same connection reused |
| Speed | Slower | Faster |
| Overhead | High (repeated setup) | Low |

### Conclusion
HTTP is the backbone protocol of the web, and persistent connections in HTTP/1.1 make browsing significantly faster than the older non-persistent model.

### Exam Keywords
HTTP, Request-Response, Stateless, GET, POST, Persistent, Non-Persistent, Port 80

---

## 3. Compare SMTP and POP3

### Definition
SMTP sends email. POP3 receives/downloads email.

### Important Points
- **SMTP (Simple Mail Transfer Protocol)** sends/pushes email from client to server, and server to server, using **port 25**. It works in a **push model**.
- **POP3 (Post Office Protocol v3)** receives/pulls email from server to client, using **port 110**. It works in a **pull model**, and traditionally downloads and deletes mail from the server after retrieval.

### Comparison Table
| Feature | SMTP | POP3 |
|---|---|---|
| Function | Sends mail | Receives mail |
| Model | Push protocol | Pull protocol |
| Port | 25 | 110 |
| Scope | Client-Server, Server-Server | Only Client-Server |

### Conclusion
SMTP and POP3 together handle the full email cycle — SMTP for sending, POP3 for receiving.

### Exam Keywords
SMTP, POP3, Push Protocol, Pull Protocol, Port 25, Port 110

---

## 4. Explain FTP (File Transfer Protocol)

### Definition
FTP is a protocol used to transfer files between a client and a server over a network.

### Diagram
```
CLIENT                          SERVER
  |---- Control (port 21) -------|   (stays open)
  |---- Data (port 20) ----------|   (opens only for transfer)
```

### Important Points
- FTP uses **two parallel TCP connections**: a **Control connection (port 21)** and a **Data connection (port 20)**.
- The **Control connection** stays open for the entire session, handling commands like LOGIN, LIST, GET, PUT.
- The **Data connection** opens only when actual file transfer happens, and closes right after.
- This separation ensures control commands (like listing files) are never delayed by an ongoing large file transfer.
- FTP requires the user to **login** (username/password) before transferring files, though anonymous FTP is also possible.

### Conclusion
FTP's dual-connection design (separate control and data channels) allows commands and file transfer to work independently and efficiently.

### Exam Keywords
FTP, Control Connection, Data Connection, Port 21, Port 20, File Transfer

---

## 5. Explain Firewall and its Types

### Definition
A firewall is a network security system that monitors and controls incoming and outgoing traffic based on defined rules.

### Diagram
```
Internet <----> [ FIREWALL ] <----> Internal Network
                 (filters traffic)
```

### Important Points
- **Packet-Filtering Firewall** (Network layer) — checks packet headers (IP address, port number) against a set of rules; fast, but has limited context about the connection.
- **Stateful Inspection Firewall** — tracks the state of active connections, allowing only packets that match an already established, legitimate session.
- **Application-Layer (Proxy) Firewall** — inspects the actual content/data at the application level (e.g., HTTP requests); offers the deepest inspection, but is slower than the other types.
- Firewalls are used to **control network access** and block unauthorized or malicious traffic from entering/leaving a network.

### Comparison Table
| Type | Layer | Description |
|---|---|---|
| Packet-Filtering | Network layer | Checks headers (IP, port) against rules; fast |
| Stateful Inspection | Network/Transport | Tracks state of active connections |
| Application-Layer (Proxy) | Application layer | Inspects full content; deepest, slowest |

### Conclusion
Firewalls provide layered network protection — from fast header-only checks to deep content inspection — based on the level of security needed.

### Exam Keywords
Firewall, Packet Filtering, Stateful Inspection, Proxy Firewall, Network Security, Access Control

---

## 6. Explain Public Key Cryptography (Asymmetric Encryption)

### Definition
Public Key Cryptography uses a pair of keys — a public key (shared openly) and a private key (kept secret) — to encrypt and decrypt data.

### Diagram
```
SENDER                                RECEIVER
Message
  |
  | Encrypt with Receiver's PUBLIC key
  v
Ciphertext --------- sent over network -------> Ciphertext
                                                     |
                                       Decrypt with Receiver's
                                       OWN PRIVATE key
                                                     v
                                                  Message
```

### Important Points
- Uses a **key pair**: **public key** (shared openly with everyone) and **private key** (kept secret by the owner).
- **For confidentiality:** sender encrypts the message using the receiver's **public key**; only the receiver's **private key** can decrypt it.
- **For Digital Signature:** sender encrypts (signs) using their **own private key**; anyone can verify it using the sender's public key — this proves **authenticity** and **non-repudiation** (sender cannot deny sending it).
- Solves the key-distribution problem of symmetric (private key) cryptography, where both parties must securely share the same secret key beforehand.
- Slower than symmetric encryption, so it is often used to securely exchange a symmetric session key, which then encrypts the actual bulk data.

### Conclusion
Public Key Cryptography enables secure communication and authentication without needing to share a secret key beforehand, forming the basis of secure Internet protocols like TLS/SSL.

### Exam Keywords
Public Key, Private Key, Asymmetric Encryption, Digital Signature, Non-Repudiation, Confidentiality

---

## 7. Explain Digital Certificate

### Definition
A Digital Certificate is an electronic document that binds a public key to a verified identity, issued by a trusted Certificate Authority (CA).

### Diagram
```
+------------------------------+
|      DIGITAL CERTIFICATE       |
|  Owner Identity: example.com    |
|  Public Key: XXXX...            |
|  Issued by: Certificate Authority|
|  Digital Signature of CA         |
+------------------------------+
```

### Important Points
- Issued by a trusted **Certificate Authority (CA)** after verifying the identity of the requester (e.g., a website owner).
- Binds a **public key** to a verified identity, so others can trust that the public key genuinely belongs to that entity.
- Prevents **man-in-the-middle attacks**, where an attacker could otherwise impersonate a website by presenting a fake public key.
- Contains fields like: owner's identity, public key, issuing CA, validity period, and the CA's own digital signature.
- Used heavily in **HTTPS/TLS/SSL** to verify that a website is genuine before establishing a secure encrypted connection.

### Conclusion
Digital Certificates are essential for establishing trust on the Internet — they confirm that a public key truly belongs to the claimed owner, preventing impersonation.

### Exam Keywords
Digital Certificate, Certificate Authority, Public Key, TLS/SSL, Man-in-the-Middle, Trust

---

# One Page Revision

```
OSI          = 7 Layers
TCP/IP       = 4 Layers
LAN/MAN/WAN  = Building / City / Country
Connection-Oriented = TCP (reliable, setup first)
Connectionless      = UDP (fast, no setup)
CRC          = XOR Division
Bit Stuffing = 5 ones -> add 0
Byte Stuffing= ESC before FLAG/ESC
Go-Back-N    = ACK number = next expected frame
IPv4         = 32 bit
IPv6         = 128 bit
TCP          = Reliable, Connection-Oriented
UDP          = Fast, Connectionless
Distance Vector = Bellman-Ford, shares with neighbors only
Link State       = Dijkstra, floods to all routers
QoS          = Reliability + Delay + Jitter + Bandwidth
Leaky Bucket = Constant output rate
Token Bucket = Allows bursts
DNS          = Name -> IP (Root -> TLD -> Authoritative)
HTTP         = Request-Response, Port 80, Stateless
SMTP         = Send Mail (port 25, Push)
POP3         = Receive Mail (port 110, Pull)
FTP          = Control(21) + Data(20)
Firewall     = Packet Filter / Stateful / Proxy
Public Key   = Locks (Encrypt) / Verifies Signature
Private Key  = Opens (Decrypt) / Creates Signature
Digital Certificate = Binds Public Key to Identity (issued by CA)
```

---

### Final Exam Strategy
- Attempt all questions above first — they are structured exactly as the DBATU paper pattern (Unit 1, Unit 3, Unit 4, Unit 5).
- For every numerical, show all working steps under Solved Example — partial marks given even for wrong final answer.
- Always draw the diagram/table mentioned — separate marks are given for diagrams.
- Use the Important Points directly as your exam answer — they are already written in exam-ready bullet form.
- Underline/bold the **Exam Keywords** wherever they appear in your written answer.

**Good luck for your DBATU Computer Networks exam.**
