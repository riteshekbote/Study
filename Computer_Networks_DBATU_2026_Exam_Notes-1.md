# BTCOC602 — Computer Networks
## DBATU Top 20 Most Repeated Questions (2026 Exam Notes)

> Based on deep analysis of 7 previous papers: Winter 2025, Summer 2025 (x2), Winter 2024, Summer 2024, Winter 2023 (x2), Jan 2024.
> These 20 questions cover **70–80% of total marks** in every paper. Master these first.

---

# UNIT 1: Introduction & Physical Layer

---

## Q1. Compare OSI Model and TCP/IP Model

### Definition
The **OSI Model** is a 7-layer theory model that shows how network communication should work.
The **TCP/IP Model** is a 4-layer model that is actually used to run the real Internet.

### Explanation
Think of OSI as a "rulebook" made by experts, and TCP/IP as the "real tool" engineers actually built and use every day. Both break communication into layers so each layer only does one job.

### Important Points
- **OSI** = Open Systems Interconnection, has **7 layers**.
- **TCP/IP** = has **4 layers** (sometimes shown as 5).
- OSI is a **reference model** (theory). TCP/IP is a **working/implemented model**.
- OSI separates **Session** and **Presentation** layers. TCP/IP merges them into Application layer.

### Diagram
```
        OSI MODEL                    TCP/IP MODEL
   ---------------------          ---------------------
7  | Application       |    ---\  |                    |
6  | Presentation       |   ----\ |    Application      |
5  | Session            |   ----/ |                    |
   ---------------------          ---------------------
4  | Transport          | ------> |    Transport        |
   ---------------------          ---------------------
3  | Network             | ------> |    Internet          |
   ---------------------          ---------------------
2  | Data Link           |   ----\ |                    |
1  | Physical             |   ----/ |    Network Access    |
   ---------------------          ---------------------
```

### Comparison Table
| Feature | OSI Model | TCP/IP Model |
|---|---|---|
| Layers | 7 | 4 |
| Developed by | ISO | DARPA/Internet |
| Approach | Theoretical, general | Practical, protocol-based |
| Session/Presentation | Separate layers | Merged into Application |
| Usage today | Used for teaching/reference | Used in real Internet |
| Reliability | Reliable at Network + Transport | Reliable only at Transport |

### 6-Mark Answer
**OSI (Open Systems Interconnection)** model has **7 layers**: Physical, Data Link, Network, Transport, Session, Presentation, and Application. It is a **reference model** — it tells us *how* communication should be designed, but it is not directly used on the real Internet.

**TCP/IP** model has **4 layers**: Network Access (Link), Internet, Transport, and Application. It is the model that the **actual Internet uses**, built around real protocols like TCP, IP, UDP, HTTP.

**Key Differences:**
- OSI has 7 layers, TCP/IP has 4 layers.
- OSI is protocol-independent (a general design); TCP/IP is protocol-dependent (built around real protocols).
- OSI keeps Session and Presentation layers separate; TCP/IP merges Session + Presentation + Application into one **Application layer**.
- OSI was made first as a standard but is rarely fully used; TCP/IP is what actually runs the Internet today.
- OSI guarantees reliability at both Network and Transport layer; TCP/IP guarantees reliability mainly at Transport layer (TCP).

**Example:** When you open a website, TCP/IP's Application layer uses HTTP, Transport layer uses TCP, Internet layer uses IP, and Network Access layer sends bits over Wi-Fi/Ethernet.

### Memory Trick
**"Please Do Not Throw Sausage Pizza Away"** = Physical, Data link, Network, Transport, Session, Presentation, Application (OSI layers bottom to top).

---

## Q2. Explain Design Issues of Network Layers (Protocol Hierarchy)

### Definition
**Design issues** are the common problems every layer must solve, like addressing, error control, and flow control, no matter which layer it is.

### Explanation
Every layer in a network talks to the same layer on the other computer using a **protocol** (a set of rules). Even though each layer does a different job, they all face similar basic problems.

### Important Points
- **Addressing**: Every layer needs a way to identify sender and receiver.
- **Error Control**: Detect and fix errors caused during transmission.
- **Flow Control**: Fast sender should not flood a slow receiver.
- **Multiplexing**: Combining multiple connections onto one channel.
- **Routing**: Choosing the best path when many paths exist.
- **Protocol vs Service**: A **service** is what a layer offers (its job); a **protocol** is the rules used to do that job.

### 6-Mark Answer
Network software is organized as a **stack of layers**, each layer using a **protocol** to talk to the same layer on the remote machine. This is called **protocol hierarchy**.

**Design issues faced at every layer:**
1. **Addressing** — Every layer must have a way to say who is sending and who is receiving.
2. **Error Control** — Since the physical medium is not perfect, layers must detect/correct errors.
3. **Flow Control** — Preventing a fast sender from overwhelming a slow receiver.
4. **Multiplexing/Demultiplexing** — Sharing one physical connection between many logical connections.
5. **Routing** — When there are multiple paths between source and destination, the best path must be chosen.
6. **Connection-oriented vs Connectionless** — Deciding whether to set up a session first (like TCP) or just send data directly (like UDP).

**Protocol vs Service:** A service is the **set of operations** a layer provides to the layer above it (interface). A protocol is the **set of rules and formats** used by peer entities to implement that service. So: *service defines what a layer does; protocol defines how it is done.*

### Memory Trick
**"A FEW MR"** → Addressing, Flow control, Error control, multiplexing (W), Multiplexing, Routing.

---

## Q3. Bandwidth-Delay Product / Bit Length Numerical

### Definition
**Bit length** is the physical length (in meters) that one bit occupies on the transmission medium.
**Bandwidth-Delay Product (BDP)** tells us how much data can be "in transit" (in flight) on a link at any moment.

### Formula
```
Bit Length = Propagation Speed / Bandwidth (bits per second)

Bandwidth-Delay Product = Bandwidth × Round Trip Delay
```

### Important Points
- Propagation speed is usually given as **2 × 10⁸ m/s**.
- BDP tells you the **"pipe capacity"** — how many bits can be in the wire at once.
- Higher BDP = need bigger buffer/window size for efficient transfer.

### 6-Mark Answer (Worked Example)
**Given:** Propagation speed = 2×10⁸ m/s.

**Formula:** Bit length = Propagation speed ÷ Bandwidth

**(i) Bandwidth = 1 Mbps = 10⁶ bps**
Bit length = (2×10⁸) / (10⁶) = **200 meters**

**(ii) Bandwidth = 10 Mbps = 10×10⁶ bps**
Bit length = (2×10⁸) / (10×10⁶) = **20 meters**

**(iii) Bandwidth = 100 Mbps = 100×10⁶ bps**
Bit length = (2×10⁸) / (100×10⁶) = **2 meters**

**Conclusion:** As bandwidth increases, each bit occupies a **shorter physical length** on the wire.

**Bandwidth-Delay Product Example:** If bandwidth = 10 Mbps and round-trip delay = 500 ms:
BDP = 10 Mbps × 0.5 sec = **5 Mbits** in transit. This means 5 Mbits of data can be sent before the first bit's acknowledgment comes back — this is the ideal window size for full link utilization.

### Memory Trick
**"Bit length = Speed ÷ Speed of sending"** — the faster you send (higher bandwidth), the shorter each bit becomes on the wire.

---

## Q4. Wireless Technologies: Wi-Fi, WiMAX, Bluetooth, RFID

### Definition
These are wireless technologies used to connect devices without wires, each designed for a different **range** and **purpose**.

### Explanation
- **Wi-Fi** connects devices in a home/office (like a wireless LAN).
- **Bluetooth** connects nearby devices like earphones, mouse (very short range).
- **WiMAX** connects whole cities or rural areas (long range broadband).
- **RFID** is used to identify tags, like in shopping cards or toll booths.

### Comparison Table
| Technology | Standard | Range | Speed | Use Case |
|---|---|---|---|---|
| **Wi-Fi** | IEEE 802.11 | ~50–100m indoor | High | Home/office wireless internet |
| **Bluetooth** | IEEE 802.15.1 | ~10m | Low | Earphones, mouse, file sharing (forms a **piconet**) |
| **WiMAX** | IEEE 802.16 | Several km | High (long range) | Rural/metro broadband internet |
| **RFID** | — | cm to few meters | Low | Tags: inventory, toll, access cards |

### 802.11 (Wi-Fi) Architecture
- Basic unit = **BSS (Basic Service Set)** — group of stations.
- **Infrastructure mode**: stations connect via an **Access Point (AP)**.
- **Ad-hoc mode (IBSS)**: stations connect directly, no AP.
- Multiple BSS connected together = **ESS (Extended Service Set)**.

### Bluetooth Architecture
- Devices form a **piconet**: 1 master + up to 7 active slave devices.
- All slaves sync to the master's clock and frequency-hopping pattern.
- Multiple piconets linked = **scatternet**.

### 6-Mark Answer
**Wi-Fi (IEEE 802.11)** is used for wireless LAN inside homes/offices. Its architecture uses a **BSS (Basic Service Set)** — a group of stations that talk either through an **Access Point** (infrastructure mode) or directly to each other (ad-hoc mode). Several BSSs joined via a distribution system form an **ESS**.

**Bluetooth (IEEE 802.15.1)** is for very short-range communication (~10m), like connecting a phone to earphones. It forms a **piconet**: one master device controls up to 7 slave devices, all synced to its clock.

**WiMAX (IEEE 802.16)** is designed for **long-distance broadband wireless access**, ideal for rural areas where laying cables is expensive. It can cover several kilometers, unlike Wi-Fi's short range.

**RFID** uses radio tags to identify objects — used in toll booths, inventory tracking, and access cards.

**Real-life application example:** A village without cable internet uses **WiMAX** towers to give broadband to homes, while inside each home, **Wi-Fi** distributes internet to devices, and **Bluetooth** connects phone to wireless earphones.

### Memory Trick
**"Wi-Fi = Wide inside, Bluetooth = Body-near, WiMAX = Miles away"**

---

# UNIT 2: Data Link Layer

---

## Q5. Framing: Byte Stuffing and Bit Stuffing

### Definition
**Framing** means breaking the stream of bits into separate **frames**, so the receiver knows where one frame ends and the next begins.

### Explanation
Imagine sending many sentences without any full stops — the reader gets confused. Framing adds "full stops" (special markers) so the receiver can split the data correctly.

### Important Points
- **Byte Count method**: First field tells how many bytes are in the frame. **Problem**: if this count gets corrupted, everything after it is also lost (cascading error).
- **Byte Stuffing (Character Stuffing)**: Uses special **FLAG bytes** to mark start/end of frame. If FLAG pattern appears inside real data, an **ESC (escape byte)** is inserted before it.
- **Bit Stuffing**: Uses a bit pattern like `01111110` as flag. Whenever **five consecutive 1s** appear in data, a **0 is stuffed** after them.

### Worked Example — Byte Stuffing
Given: A = 01000111, B = 11100011, FLAG = 01111110, ESC = 11100000

To send frame: **A B ESC FLAG**

Since data contains **ESC** and **FLAG** as literal characters, we must stuff an extra ESC before each:

```
FLAG + A + B + ESC(stuff) + ESC + ESC(stuff) + FLAG + FLAG
```
Final bit stream = `FLAG A B ESC ESC ESC FLAG FLAG`
(one ESC is stuffed before the literal ESC, one ESC is stuffed before the literal FLAG, and the whole frame is wrapped in FLAG bytes at both ends)

### Worked Example — Bit Stuffing
Data = `110111111111100`

Rule: after every five consecutive 1s, insert a 0.

```
Original: 1101 11111 11111 00
Stuffed:  1101 111110 111110 00
```

### 6-Mark Answer
**Framing** breaks the continuous bit stream into frames so the receiver can identify frame boundaries.

**1. Byte/Character Count**: The frame header has a field stating the number of bytes in the frame. Simple, but if this count field is damaged during transmission, the receiver completely loses synchronization (cascading failure). Rarely used alone.

**2. Byte Stuffing (Character Stuffing)**: Special reserved **FLAG bytes** (e.g. `01111110`) mark the start and end of every frame. If the actual data contains a byte equal to FLAG or ESC, an extra **ESC byte** is inserted before it so the receiver does not confuse data with a real flag. The receiver removes stuffed ESC bytes while reading.

**3. Bit Stuffing**: Uses bit pattern `01111110` as the flag. The sender inserts a `0` after every five consecutive `1`s in the data, ensuring the flag pattern never appears accidentally inside real data. The receiver removes the stuffed `0`s.

**Example (Bit Stuffing):** Data `110111111111100` becomes `11011111011111000` after stuffing.

### Memory Trick
**"5 ones → add a zero"** for bit stuffing. **"Special byte inside data → add ESC before it"** for byte stuffing.

---

## Q6. CRC (Cyclic Redundancy Check) — Numerical

### Definition
**CRC** is an error detection method that uses **binary (polynomial) division** to generate a check code, which is sent along with data to detect transmission errors.

### Explanation
The sender divides the message by a fixed **generator number** using XOR, gets a remainder, and attaches that remainder to the message. The receiver repeats the division — if the remainder is **zero**, data is correct.

### Steps
1. Let message = **M**, generator = **G** (of degree r, i.e., r+1 bits).
2. Append **r zeros** to M → get M'.
3. Divide M' by G using **XOR (modulo-2) division** — no borrow/carry, just XOR.
4. The remainder (**r bits**) is the **CRC code**.
5. **Transmitted Codeword = M + CRC** (replace the appended zeros with the remainder).
6. **At Receiver**: Divide received codeword by same G.
   - Remainder = 0 → **No error**
   - Remainder ≠ 0 → **Error detected**

### Worked Example
Message = `1101011` (7 bits), Generator = `1101` (4 bits, degree 3)

**Step 1:** Append 3 zeros → `1101011000`

**Step 2:** XOR Division:
```
1101011000
1101
----
0000111000
    1101
    ----
    0010100
    1101
    ----
    0001100
     1101
     ----
     0000100   (remainder shown after final step)
```
Suppose final remainder = `100`

**Step 3:** Transmitted Codeword = `1101011` + `100` = **`1101011100`**

**Step 4 (Check at receiver):** Divide `1101011100` by `1101` again.
- If remainder = `000` → No error, data accepted.
- If remainder ≠ `000` → Error detected, ask for retransmission.

### 6-Mark Answer
CRC (Cyclic Redundancy Check) detects errors using **polynomial (modulo-2) division**.

**Method:**
1. Append **r zeros** to the message (where r = degree of generator polynomial).
2. **XOR-divide** this extended message by the generator polynomial.
3. The **remainder** becomes the CRC bits.
4. Replace the appended zeros with this remainder → this is the **transmitted codeword**.
5. Receiver divides the received codeword by the same generator. **Remainder = 0 means no error**; otherwise an error is detected.

**Example:** For message `1101011` and generator `1101`, after appending 3 zeros and performing XOR division, we get a 3-bit CRC. This CRC is attached to the message to form the final transmitted frame. At the receiver, the same division is performed; a non-zero remainder signals a transmission error.

**Note:** Always show every XOR step in the exam — partial marks are given even if final remainder is slightly wrong.

### Memory Trick
**"Append zeros, XOR divide, remainder = CRC"** — remember: **A-X-R** (Append, XOR, Remainder).

---

## Q7. Hamming Code (Error Correction) — Numerical

### Definition
**Hamming Code** is an error-correcting code that can detect **and correct** a single-bit error using extra **parity bits**.

### Explanation
Parity bits are placed at positions that are **powers of 2** (1, 2, 4, 8...). Each parity bit checks a specific group of bits. If there's an error, the pattern of failed checks tells us exactly **which bit** is wrong.

### Important Points
- Parity bit positions: **1, 2, 4, 8, ...**
- Data bit positions: all others (3, 5, 6, 7, ...)
- Each parity bit **P_k** checks positions whose binary form has that bit set.
- Combine check results (C4 C2 C1) as binary number = **position of error bit**.
- If result = 0 → **No error**.

### Steps to Check Received Code
1. Number bits from **1** (leftmost) to n.
2. Identify parity positions: 1, 2, 4, 8...
3. For each parity bit, check even/odd parity of its group.
4. Each check gives 0 (OK) or 1 (fail).
5. Arrange results as binary number → tells **exact error position**.
6. **Flip that bit** to correct it.

### Worked Example
Received 7-bit Hamming code = `1011011` (positions 1 to 7), assume **even parity**.

| Position | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| Bit | 1 | 0 | 1 | 1 | 0 | 1 | 1 |

- **P1** (checks 1,3,5,7) = 1,1,0,1 → sum of 1s = 3 (odd) → parity fails → **C1 = 1**
- **P2** (checks 2,3,6,7) = 0,1,1,1 → sum of 1s = 3 (odd) → parity fails → **C2 = 1**
- **P4** (checks 4,5,6,7) = 1,0,1,1 → sum of 1s = 3 (odd) → parity fails → **C4 = 1**

Error position (C4 C2 C1) = **111 = 7 (decimal)**

**Conclusion:** Bit at **position 7 is wrong**. Flip it to correct: `1011011` → `1011010`.

### 6-Mark Answer
Hamming Code corrects single-bit errors using redundant **parity bits** placed at power-of-2 positions (1, 2, 4, 8...).

**Method:** For a received code, check each parity bit's group for correct parity. Each check gives a pass (0) or fail (1). Combine fail results as a binary number — this number directly gives the **position of the wrong bit**. If the combined result is 0, there is no error. If not zero, flip the bit at that position to correct the code.

**Example:** For received code `1011011` with even parity, checking P1, P2, P4 groups shows all three checks fail, giving error position = `111` (binary) = **7**. So bit 7 is wrong; flipping it corrects the code to `1011010`.

### Memory Trick
**"Parity fails at powers of 2, combine to find culprit position"** — remember positions **1, 2, 4** are always the checkers.

---

## Q8. Go-Back-N ARQ — Numerical

### Definition
**Go-Back-N ARQ** is a sliding window protocol where the sender can send **multiple frames** without waiting for each ACK, but if an error occurs, it must **resend all frames** from the error point onward.

### Explanation
The receiver only accepts frames **in correct order**. If a frame is lost/damaged, the receiver discards every frame after it too. The sender must "go back" and resend starting from the lost frame.

### Important Points
- Sender can send up to **window size N** frames without individual ACK.
- **Cumulative ACK**: ACK number *k* means "I have correctly received all frames up to k−1, and I expect frame *k* next."
- Any out-of-order frame at receiver is **discarded**.

### Worked Example
Sender sends 8 frames, numbered **0 to 7**. Receiver sends **ACK number 6**.

- ACK 6 means: frames **0,1,2,3,4,5** were received correctly.
- Receiver is now expecting frame **6** next.
- So frames **6 and 7** were lost or damaged.

**Answer: Sender must retransmit 2 frames — frame 6 and frame 7.**

### Diagram
```
Sender:    0   1   2   3   4   5   6   7
                                    X   X   <- lost/corrupted
Receiver:  ACK1 ACK2 ACK3 ACK4 ACK5 ACK6 (expecting frame 6)
                                     |
                     Sender goes back and resends: 6, 7
```

### 6-Mark Answer
**Go-Back-N ARQ** is a sliding-window flow/error control protocol. The sender can transmit up to **N frames** continuously without waiting for individual acknowledgments, improving efficiency over stop-and-wait.

**Working:**
- The receiver uses **cumulative acknowledgment** — ACK number *k* confirms all frames up to *k−1* were received correctly and it now expects frame *k*.
- The receiver only accepts frames in the **correct sequence**; any frame arriving out of order is discarded, even if it is error-free.
- If the sender does not receive expected ACKs (timeout) or receives an ACK indicating missing frames, it must **retransmit all frames starting from the lost frame onward** — this is why it's called "Go-Back-N."

**Numerical:** Sender sends 8 frames (0–7). It receives **ACK number 6**, meaning frames 0–5 arrived safely and frame 6 is expected next. Therefore, frames **6 and 7 (2 frames)** must be retransmitted.

### Memory Trick
**"ACK number = next expected frame"** — subtract to find how many frames need resending.

---

## Q9. Ethernet Frame Format (IEEE 802.3)

### Definition
The **Ethernet frame** is the standard format used to send data over wired LANs, defined by **IEEE 802.3**.

### Diagram
```
+----------+-----+------------+-------------+-------+---------------+-----+
| Preamble | SFD | Dest MAC   | Source MAC  | Type/ | Data/Payload  | FCS |
| 7 bytes  |1byte| 6 bytes    | 6 bytes     |Length | 46-1500 bytes |4byte|
|          |     |            |             |2 bytes|               |     |
+----------+-----+------------+-------------+-------+---------------+-----+
```

### Field-by-Field Explanation
| Field | Size | Function |
|---|---|---|
| **Preamble** | 7 bytes | Pattern `10101010` repeated — helps receiver's clock **synchronize** |
| **SFD (Start Frame Delimiter)** | 1 byte | Signals "**real frame starts now**" (pattern `10101011`) |
| **Destination MAC** | 6 bytes | Physical address of receiving device |
| **Source MAC** | 6 bytes | Physical address of sending device |
| **Type/Length** | 2 bytes | Tells which upper-layer protocol (e.g., IPv4) or frame length |
| **Data/Payload** | 46–1500 bytes | Actual data; **padded** with extra bits if less than 46 bytes |
| **FCS (Frame Check Sequence)** | 4 bytes | **CRC-based** error detection code |

### 6-Mark Answer
The **Ethernet Frame (IEEE 802.3)** format has the following fields in order:

1. **Preamble (7 bytes)** — alternating 1s and 0s used to synchronize the receiver's clock with the sender's.
2. **Start of Frame Delimiter/SFD (1 byte)** — special pattern that tells the receiver the actual frame data is about to begin.
3. **Destination MAC Address (6 bytes)** — hardware address of the receiving NIC.
4. **Source MAC Address (6 bytes)** — hardware address of the sending NIC.
5. **Type/Length (2 bytes)** — if value > 1500, indicates the upper-layer protocol type (e.g., IPv4 = 0x0800); if ≤ 1500, indicates frame length.
6. **Data/Payload (46–1500 bytes)** — the actual message; if data is smaller than 46 bytes, padding is added to meet the minimum frame size.
7. **FCS/Frame Check Sequence (4 bytes)** — a CRC checksum used to detect transmission errors.

**Minimum frame size = 64 bytes, Maximum frame size = 1518 bytes** (including all header fields).

### Memory Trick
**"Please Send Data, Source, Type, Payload, Finish!"** = Preamble, SFD, Dest MAC, Source MAC, Type, Payload, FCS.

---

# UNIT 3: Network Layer — IP Addressing

---

## Q10. IPv4 vs IPv6 Comparison

### Definition
**IPv4** is the older Internet addressing system using 32-bit addresses. **IPv6** is the newer system using 128-bit addresses to support many more devices.

### Comparison Table
| Feature | IPv4 | IPv6 |
|---|---|---|
| **Address length** | 32 bits | 128 bits |
| **Address space** | ~4.3 billion addresses | Practically unlimited (2¹²⁸) |
| **Header** | Complex, variable length, has checksum | Simplified, fixed 40-byte header, **no checksum** |
| **Security** | Optional (IPSec add-on) | **Built-in IPSec support** |
| **Fragmentation** | Done by routers **and** sender | Done **only by sending host** |
| **Address notation** | Dotted decimal (192.168.1.1) | Hexadecimal, colon-separated (2001:db8::1) |
| **Configuration** | Manual / DHCP | Auto-configuration supported |

### 6-Mark Answer
**IPv4** uses a **32-bit address**, giving about 4.3 billion unique addresses, written in **dotted decimal** notation (e.g., 192.168.1.1). Its header is complex and variable in length, includes a checksum field, and fragmentation can happen at **both routers and the sending host**.

**IPv6** uses a **128-bit address**, giving a virtually unlimited address space, written in **hexadecimal colon-separated** notation (e.g., 2001:db8::1). Its header is **simplified and fixed at 40 bytes**, dropping the checksum field for faster processing at routers. IPv6 also has **built-in security (IPSec)** support and fragmentation is done **only by the sending host**, not by routers — making routing faster.

**Why IPv6 was needed:** IPv4's 4.3 billion addresses are running out due to the explosion of internet-connected devices; IPv6 solves this address exhaustion problem.

### Memory Trick
**"4 = 32 bits (small), 6 = 128 bits (huge)"** — IPv6 number is bigger, so is its address size.

---

## Q11. IP Fragmentation — Numerical

### Definition
**Fragmentation** is splitting a large IP packet into smaller pieces so it can pass through a network link with a smaller **MTU (Maximum Transmission Unit)**.

### Formula
```
Usable data per fragment = (MTU − fragment IP header), rounded DOWN to multiple of 8

Number of fragments = ceil(Total data to fragment / Usable data per fragment)

Fragmentation Offset (in fragment N) = (cumulative data sent before this fragment) / 8
```

### Worked Example
**Given:** Total IP packet = 4500 bytes (20-byte IP header + 40-byte TCP header + 4440 bytes data). Router MTU = 600 bytes. Fragment IP header = 20 bytes. First fragment offset = 0.

**Step 1:** Usable data per fragment = 600 − 20 = 580 → round down to multiple of 8 = **576 bytes**

**Step 2:** Total data to fragment (excluding original IP header) = 4500 − 20 = **4480 bytes**

**Step 3:** Number of fragments = ceil(4480 / 576) = **8 fragments** (last one smaller)

**Step 4:** Offset values (offset = cumulative bytes sent so far ÷ 8):
- Fragment 1: offset = 0
- Fragment 2: offset = 576/8 = **72**
- Fragment 3: offset = 1152/8 = **144**

**Answer: 3rd fragment offset = 144, Total fragments = 8**

### 6-Mark Answer
**IP Fragmentation** happens when a packet is too large for a network link's **MTU (Maximum Transmission Unit)**. The router splits the packet into smaller fragments, each with its own IP header.

**Formula used:**
- Usable data per fragment = (MTU − fragment's IP header size), rounded down to the nearest multiple of 8 (since offset field is measured in units of 8 bytes).
- Total fragments = total data to be fragmented ÷ usable data per fragment (rounded up).
- **Fragmentation offset** of each fragment = (total data sent in previous fragments) ÷ 8.

**Worked Example:** For a 4500-byte packet (20-byte IP header + 4480 bytes of data) going through a 600-byte MTU router (20-byte fragment header), usable data per fragment = 576 bytes. This gives **8 total fragments**. The 3rd fragment's offset = (576+576)/8 = **144**.

### Memory Trick
**"Offset is always in units of 8 bytes"** — divide cumulative data by 8 to get offset.

---

## Q12. Classful IP Addressing — Find Class, Network ID, Host ID

### Definition
**Classful addressing** divides IPv4 addresses into classes (A, B, C, D, E) based on the value of the **first octet**.

### Comparison Table
| Class | First Octet Range | Default Mask | Used For |
|---|---|---|---|
| **A** | 1 – 126 | 255.0.0.0 | Large networks |
| **B** | 128 – 191 | 255.255.0.0 | Medium networks |
| **C** | 192 – 223 | 255.255.255.0 | Small networks |
| **D** | 224 – 239 | — | Multicast |
| **E** | 240 – 255 | — | Experimental/Research |

### Worked Example
**Given IP:** 222.151.210.34

**Step 1:** First octet = 222. Since 192 ≤ 222 ≤ 223 → **Class C**

**Step 2:** Class C default mask = 255.255.255.0 → first **3 octets = Network ID**, last octet = **Host ID**

- **Network ID = 222.151.210.0**
- **Host ID = 34**

### 6-Mark Answer
**Classful addressing** splits the 32-bit IPv4 address space into 5 classes (A–E), identified by the value of the **first octet**:
- **Class A** (1–126): First octet = network, remaining 3 octets = host. Used for very large organizations.
- **Class B** (128–191): First 2 octets = network, last 2 = host. Used for medium-sized networks.
- **Class C** (192–223): First 3 octets = network, last octet = host. Used for small networks.
- **Class D** (224–239): Reserved for **multicast**.
- **Class E** (240–255): Reserved for **experimental/research** use.

**Example:** For IP address **222.151.210.34**, the first octet is 222, which falls in the Class C range (192–223). So:
- **Class = C**
- **Network ID = 222.151.210.0**
- **Host ID = 34**

### Memory Trick
**"A-B-C = 1-2-3 octets for Network"** — Class A uses 1 octet for network, Class B uses 2, Class C uses 3.

---

## Q13. TCP/UDP Header — Decoding a Hex Dump

### Definition
Network headers are often given as a **hexadecimal dump**; converting each field's hex value to decimal reveals the port numbers, length, and other details.

### UDP Header Format (8 bytes fixed)
```
+----------------+-----------------+
| Source Port(2B)| Dest Port (2B)  |
+----------------+-----------------+
| Length (2B)    | Checksum (2B)   |
+----------------+-----------------+
```

### Worked Example — UDP
Hex dump: `0045 DE00 FE20 0058`

- **Source Port** = 0045 (hex) = **69** (decimal) → well-known port (69 = TFTP)
- **Destination Port** = DE00 (hex) = **56832** (decimal) → high-numbered, random port
- **Total UDP Length** = FE20 (hex) = **65056** (decimal, in bytes)
- **Checksum** = 0058 (hex)

**Client vs Server:** Since port 69 is a **well-known port (0–1023)**, this is the **server side**. The high port (56832) belongs to the **client**. So the packet is going from **server to client**.

### TCP Header Format (minimum 20 bytes)
```
Source Port (2B) | Dest Port (2B)
Sequence Number (4B)
Acknowledgement Number (4B)
Header Length+Flags (2B) | Window Size (2B)
Checksum (2B) | Urgent Pointer (2B)
```

### Worked Example — TCP
Hex dump: `0532 0021 00000000 00000000 5002 07FF 00000000`

- **Source Port** = 0532 (hex) = **1330** (decimal)
- **Destination Port** = 0021 (hex) = **33** (decimal)
- **Sequence Number** = 00000000 = **0**
- **Ack Number** = 00000000 = **0**
- **Header Length**: top nibble of `5002` = **5** → Header length = 5 × 4 = **20 bytes**
- **Window Size** = 07FF (hex) = **2047** (decimal)

### 6-Mark Answer
Header fields in a hex dump are decoded by converting each **4-hex-digit (2-byte)** or **8-hex-digit (4-byte)** group into decimal, matching the known header structure.

**UDP Header (8 bytes)**: Source Port (2B) | Destination Port (2B) | Length (2B) | Checksum (2B). Convert each group from hex to decimal directly.

**TCP Header (minimum 20 bytes)**: Source Port (2B) | Destination Port (2B) | Sequence Number (4B) | Acknowledgement Number (4B) | Header Length+Flags (2B, top 4 bits ×4 = header length in bytes) | Window Size (2B) | Checksum (2B) | Urgent Pointer (2B).

**Trick to identify client vs server:** Well-known ports (0–1023) usually belong to the **server**; high random ports (above 1023) belong to the **client**.

### Memory Trick
**"4 hex digits = 1 field of 2 bytes"** — convert each group directly using hex-to-decimal conversion.

---

# UNIT 4: Routing & Congestion Control

---

## Q14. Distance Vector vs Link State Routing + Dijkstra's Algorithm

### Definition
**Distance Vector Routing** shares distance tables with only neighbors. **Link State Routing** shares full network map with all routers, then runs **Dijkstra's algorithm** to compute shortest paths.

### Comparison Table
| Feature | Distance Vector | Link State |
|---|---|---|
| Info shared | Distance to all destinations | Cost to direct neighbors only |
| Shared with | Only neighbors | **All routers (flooding)** |
| Algorithm used | Bellman-Ford | Dijkstra's |
| Convergence | Slow | Fast |
| Problem | **Count-to-Infinity** | Higher overhead (flooding) |
| Example protocol | RIP | OSPF |

### Dijkstra's Algorithm — Worked Example
**Given graph:** A–B=4, A–D=2, B–D=3, B–C=6, C–F=1, D–E=5, E–F=2. Find shortest path from **A**.

### Diagram
```
        4         6
   A -------- B -------- C
   |  \       |          |
  2|   \3     |          |1
   |    \     |          |
   D ---------+          F
   |  5                 /
   E ------------------ 2
```

**Trace Table:**
| Step | Node Visited | dist[B] | dist[C] | dist[D] | dist[E] | dist[F] |
|---|---|---|---|---|---|---|
| 1 | A (0) | 4 | ∞ | 2 | ∞ | ∞ |
| 2 | D (2) | 4 (via A) | ∞ | — | 7 (2+5) | ∞ |
| 3 | B (4) | — | 10 (4+6) | — | 7 | ∞ |
| 4 | E (7) | — | 10 | — | — | 9 (7+2) |
| 5 | F (9) | — | 10 (stays) | — | — | — |
| 6 | C (10) | — | — | — | — | — |

**Final Distance Table:**
| Node | Distance from A | Path |
|---|---|---|
| A | 0 | A |
| B | 4 | A→B |
| D | 2 | A→D |
| E | 7 | A→D→E |
| F | 9 | A→D→E→F |
| C | 10 | A→D→E→F→C |

### 6-Mark Answer
**Distance Vector Routing:** Each router keeps a table of (destination, distance, next-hop) and shares it with **only its direct neighbors** periodically. It uses the **Bellman-Ford** principle: `new_distance = min(own_distance, neighbor_distance + cost_to_neighbor)`. Its main drawback is the **Count-to-Infinity problem**.

**Link State Routing:** Each router discovers costs to its neighbors, then **floods** this information to **every router** in the network. Every router builds a **complete map (topology)** and independently runs **Dijkstra's algorithm** to compute shortest paths. It has more overhead but converges faster and avoids loops better.

**Dijkstra's Algorithm (example above):** Starting from source A, we repeatedly pick the unvisited node with the smallest known distance, and relax (update) its neighbors' distances. Following this process on the given graph yields: B=4, D=2, E=7, F=9, C=10, with the shortest path to C being **A→D→E→F→C**.

### Memory Trick
**"Distance Vector = gossip with neighbors only; Link State = broadcast to everyone"**

---

## Q15. Count-to-Infinity Problem

### Definition
**Count-to-Infinity** is a problem in Distance Vector Routing where routers keep **slowly increasing** their distance estimates to a failed destination, taking a very long time to realize the destination is unreachable.

### Explanation
When a link fails, neighboring routers don't immediately know it's gone. They keep believing their neighbor has a path (through them!), so the distance count keeps climbing higher and higher — like counting toward infinity.

### Worked Example
```
A --- B --- C   (link cost = 1 each)
```
If link between B and C breaks:
- C tells B: "C is unreachable" — actually C is gone.
- But B still remembers an old route via C... 
- A thinks: "I can reach C via B, distance = 2"
- B thinks: "I can reach C via A, distance = 3" (using A's outdated info)
- A updates: "via B, distance = 4"
- This keeps increasing endlessly → **Count-to-Infinity**

### Solutions
- **Split Horizon**: Don't send route back to the neighbor you learned it from.
- **Split Horizon with Poison Reverse**: Send the route back but mark distance as **infinity**, explicitly saying "don't use me for this route."
- **Setting a maximum finite value** (like 16 in RIP) to represent "infinity" — after this, the route is considered unreachable.

### 6-Mark Answer
**Count-to-Infinity** occurs in **Distance Vector Routing** when a link or node fails. Since routers only share information with direct neighbors and only periodically, outdated information keeps circulating. Each router increments the distance slightly, believing the destination is still reachable through another router, causing the reported distance to slowly climb toward infinity instead of quickly marking the route as broken.

**Example:** If the link between B and C fails, and A still has an old route to C via B, then A and B may keep updating each other with increasingly wrong (larger) distances, since each believes the other still has a valid path.

**Solutions:**
1. **Split Horizon** — a router never advertises a route back to the neighbor it learned that route from.
2. **Split Horizon with Poison Reverse** — the route is advertised back but with a distance of infinity, actively warning the neighbor not to use it.
3. **Defining Infinity** — setting a small maximum hop count (e.g., 16 in RIP) so that after this value, the route is declared unreachable instead of counting forever.

### Memory Trick
**"Bad news travels slow in Distance Vector"** — that's why the count keeps climbing.

---

## Q16. Leaky Bucket & Token Bucket (Congestion Control)

### Definition
Both are traffic-shaping algorithms used to **control the rate** of data sent into a network to prevent congestion.

### Explanation
**Leaky Bucket** = a bucket with a small hole; water (data) leaks out at a **constant rate**, no matter how much is poured in.
**Token Bucket** = tokens are generated at a fixed rate; a packet needs a token to be sent, allowing **bursts** if tokens have piled up.

### Diagram
```
LEAKY BUCKET                    TOKEN BUCKET
                                 
  Bursty data in                Tokens added
   ↓ ↓  ↓                       at fixed rate
  [ bucket ]                    ┌─────────┐
      |                         │ Tokens  │← packets need
      | constant                │ Bucket  │  a token to go
      | leak rate                └─────────┘
      ↓                              ↓
  Smooth, fixed-rate out          Bursty output allowed
```

### Comparison Table
| Feature | Leaky Bucket | Token Bucket |
|---|---|---|
| Output rate | **Fixed, constant** | Variable (allows bursts) |
| Handles burst input | Smooths it out completely | Allows burst if tokens saved up |
| Packet loss | If bucket full, packet dropped | If no tokens, packet waits/dropped |
| Flexibility | Rigid | More flexible |

### 6-Mark Answer
**Leaky Bucket Algorithm:** Imagine a bucket with a small hole at the bottom. Data packets are poured in irregularly (bursty traffic), but they **leak out at a constant, fixed rate**, no matter how bursty the input is. If the bucket becomes full, extra incoming packets are **discarded**. This converts bursty traffic into a **smooth, constant-rate output stream**, enforcing a strict output rate.

**Token Bucket Algorithm:** Tokens are generated at a fixed rate and stored in a bucket (up to a maximum capacity). A packet can only be transmitted if a **token is available** (one token is consumed per packet/byte sent). Unlike Leaky Bucket, this **allows bursts** — if the host was idle and tokens accumulated, a burst of packets can be sent all at once (up to the number of available tokens).

**Key Difference:** Leaky Bucket enforces a **rigid, constant** output rate regardless of traffic pattern. Token Bucket allows **controlled burstiness** while still keeping the average rate bounded — making it more flexible for real traffic.

### Memory Trick
**"Leaky = strict and constant; Token = flexible, allows bursts"**

---

## Q17. Congestion Control: General Principles & Prevention Policies

### Definition
**Congestion** happens when too much data is sent into the network, causing packet loss and delay. **Congestion control** is the set of techniques used to prevent or manage this.

### Important Points
- **Open Loop (Prevention)**: Solve congestion **before** it happens — good design decisions.
- **Closed Loop (Feedback-based)**: Detect congestion and **react** to it after it happens.

### Open-Loop Prevention Policies
| Policy | Description |
|---|---|
| **Retransmission Policy** | Design retransmission timers carefully to avoid unnecessary resends |
| **Window Policy** | Use selective repeat instead of go-back-N to reduce redundant traffic |
| **Acknowledgement Policy** | Don't acknowledge every packet; use cumulative ACKs |
| **Discarding Policy** | Drop less important packets first (e.g., low-priority packets) |
| **Admission Policy** | Reject new connections if network is already congested |

### Closed-Loop Policies
- **Traffic Throttling**: Slow down the sending rate when congestion is detected (e.g., via ECN bits).
- **Load Shedding**: Routers intentionally drop packets when overloaded, prioritizing important ones.
- **Backpressure**: Congested node signals the previous node to slow down, which cascades backward.

### 6-Mark Answer
**Congestion** occurs when the number of packets sent into the network is greater than what the network can handle, leading to increased delay and packet loss.

**General principles of congestion control:**
1. **Monitor the system** — detect where and when congestion occurs.
2. **Pass information** to places where action can be taken.
3. **Adjust system operation** to correct the problem.

**Open-Loop (Prevention) policies** — designed into the system beforehand:
- **Retransmission Policy**: careful timer design to avoid excess retransmissions.
- **Window Policy**: choosing selective repeat over go-back-N reduces wasted retransmissions.
- **Discarding Policy**: routers drop less important packets under pressure.
- **Admission Policy**: refuse new virtual circuits if the network is already congested.

**Closed-Loop (Feedback) policies** — react after congestion is detected:
- **Traffic Throttling**: sender is told (via congestion bits) to slow down.
- **Load Shedding**: routers simply drop packets when buffers are full, ideally choosing less important ones to drop.
- **Backpressure**: congestion signal propagates backward, hop by hop, causing every upstream node to slow down.

### Memory Trick
**"Prevent before (Open Loop), React after (Closed Loop)"**

---

# UNIT 5: Application Layer & Network Security

---

## Q18. DNS — Working & Name Resolution

### Definition
**DNS (Domain Name System)** translates human-readable domain names (like `www.google.com`) into machine-readable **IP addresses**.

### Explanation
DNS is like a **phonebook for the Internet** — you know a person's name (domain), and DNS looks up their phone number (IP address) for you.

### Important Points
- DNS is a **distributed, hierarchical database** — no single server holds all records.
- Hierarchy: **Root servers → TLD servers (.com, .org, .in) → Authoritative Name servers**.
- A single domain name **can have multiple IP addresses** — used for **load balancing** and **CDNs** (Content Delivery Networks).

### Diagram — Name Resolution Steps
```
User's Browser
     |
     | "What is IP of www.example.com?"
     ↓
Local DNS Resolver (ISP) --- checks cache first
     |
     ↓ (if not cached)
Root DNS Server -----> refers to TLD server (.com)
     |
     ↓
TLD Server -----------> refers to Authoritative server
     |
     ↓
Authoritative Server --> returns final IP address
     |
     ↓
Resolver caches it & sends IP back to Browser
```

### 6-Mark Answer
**DNS (Domain Name System)** converts human-friendly domain names into numeric **IP addresses** that computers use to locate each other. It is a **distributed, hierarchical database system** — maintained by many servers around the world, not a single central server.

**Hierarchy:**
1. **Root Servers** — top of the hierarchy, know where TLD servers are.
2. **TLD (Top-Level Domain) Servers** — handle domains like `.com`, `.org`, `.in`.
3. **Authoritative Name Servers** — hold actual records for a specific domain.

**Name Resolution Process:**
1. User's browser asks the **local DNS resolver** (usually provided by the ISP) to resolve a domain name.
2. The resolver checks its **cache** first; if not found, it queries a **root server**.
3. The root server refers it to the correct **TLD server**.
4. The TLD server refers it to the domain's **authoritative server**.
5. The authoritative server returns the actual **IP address**, which the resolver caches and passes back to the browser.

**Can one DNS name have multiple IPs?** Yes — this is common with **load balancing** (round-robin DNS) and **CDNs**, where a single domain maps to multiple servers/IPs across the world for speed and redundancy.

### Memory Trick
**"Root → Top → Authoritative"** = **R-T-A**, like climbing down a family tree to find the exact address.

---

## Q19. SMTP, POP3 & FTP Protocols

### Definition
**SMTP** sends email. **POP3** receives/downloads email. **FTP** transfers files between computers.

### Comparison Table — SMTP vs POP3
| Feature | SMTP | POP3 |
|---|---|---|
| Function | **Sends** mail | **Receives** mail |
| Model | **Push** protocol | **Pull** protocol |
| Port | 25 | 110 |
| Scope | Client→Server AND Server→Server | Only Client→Server |

### FTP (File Transfer Protocol)
- Uses **two parallel TCP connections**:
  - **Control connection (port 21)** — stays open, used for commands (LOGIN, LIST, GET).
  - **Data connection (port 20)** — opens only when actual file transfer happens.
- This separation means control commands (like "list files") are never delayed by large file transfers.

### Diagram
```
CLIENT                          SERVER
   |------ Control (port 21) ------|   (stays open)
   |------ Data (port 20) ---------|   (opens only for transfer)
```

### 6-Mark Answer
**SMTP (Simple Mail Transfer Protocol)** is used to **send/push** email from a client to a mail server, and between mail servers, using **port 25**. It works in a **push model** — the sender actively pushes the message forward.

**POP3 (Post Office Protocol v3)** is used to **receive/pull** email from a mail server down to the client, using **port 110**. It works in a **pull model**, and traditionally downloads and deletes mail from the server after retrieval (though "keep copy" is common today).

**FTP (File Transfer Protocol)** is used to transfer files between computers. It uses **two separate parallel TCP connections**:
- The **control connection (port 21)** stays open for the entire session, handling login and commands like LIST, GET, PUT.
- The **data connection (port 20)** opens only when actual file data needs to be transferred, and closes after.

This separation ensures that sending commands (control) is never blocked by an ongoing large file transfer (data).

### Memory Trick
**"SMTP = Sends Mail, POP = Pulls mail Off Post office"**; **"FTP = 2 lines: Control talks, Data walks"**

---

## Q20. Cryptography, Digital Signatures, Firewalls, AES vs DES

### Definition
**Cryptography** protects data using secret codes. **Symmetric (Private Key)** uses one shared key. **Asymmetric (Public Key)** uses a pair of keys (public + private).

### Explanation
Think of a **private key** like a single house key that both people must share secretly. A **public key** is like a mailbox slot — anyone can drop a letter in (encrypt), but only the house owner with the private key can open it (decrypt).

### Important Points
- **Symmetric Encryption** (e.g., DES, AES): Same key for encryption and decryption. Fast, but sharing the key safely is hard.
- **Asymmetric Encryption** (Public Key): Two keys — a **public key** (shared openly) and a **private key** (kept secret).
  - **To send a secret message**: Encrypt with **receiver's public key**; only receiver's private key can decrypt.
  - **To create a Digital Signature**: Sign with **sender's own private key**; anyone can verify using sender's public key — proves authenticity and **non-repudiation** (sender can't deny sending it).
- **Digital Certificate**: Issued by a trusted **Certificate Authority (CA)**; binds a public key to an identity, preventing man-in-the-middle attacks.

### Diagram — Public Key Cryptography
```
SENDER                                    RECEIVER
 Message                                  
    |                                     
    | Encrypt with Receiver's PUBLIC key  
    ↓                                     
 Ciphertext  --------- sent over network -------->  Ciphertext
                                                        |
                                            Decrypt with Receiver's
                                            OWN PRIVATE key
                                                        ↓
                                                     Message
```

### Firewalls — 3 Types
| Type | Layer | Description |
|---|---|---|
| **Packet-Filtering Firewall** | Network layer | Checks packet headers (IP, port) against rules; fast, limited context |
| **Stateful Inspection Firewall** | Network/Transport | Tracks state of active connections; allows only packets matching an established session |
| **Application-Layer (Proxy) Firewall** | Application layer | Inspects actual content (e.g., HTTP requests); deepest inspection, but slower |

### AES vs DES
| Feature | DES | AES |
|---|---|---|
| **Key length** | 56-bit (weak) | 128/192/256-bit (very strong) |
| **Block size** | 64-bit, Feistel structure | 128-bit, Substitution-Permutation Network |
| **Security** | Broken by brute force since late 1990s | Extremely secure, no practical attack |
| **Rounds** | 16 rounds | 10/12/14 rounds depending on key size |

### 6-Mark Answer
**Symmetric (Private/Secret Key) Cryptography** uses the **same key** for both encryption and decryption (e.g., DES, AES). It is fast but sharing the secret key safely between two parties is difficult.

**Asymmetric (Public Key) Cryptography** uses a **key pair**: a public key (shared openly) and a private key (kept secret).
- To send a **confidential message**: the sender encrypts using the receiver's **public key**; only the receiver's **private key** can decrypt it.
- To create a **Digital Signature**: the sender encrypts (signs) using their **own private key**; anyone can verify it using the sender's public key — this proves the message is authentic and the sender cannot deny sending it (**non-repudiation**).

**Digital Certificates** are issued by a trusted **Certificate Authority (CA)**. They bind a public key to a verified identity (like a website), preventing man-in-the-middle attacks by proving the key genuinely belongs to that entity.

**Firewalls control network access** and come in three types: **Packet-filtering** (checks headers only, fast), **Stateful inspection** (tracks connection state), and **Application-layer/Proxy** (inspects full content, most secure but slowest).

**Why AES is more secure than DES:**
1. **Key length**: DES uses only a 56-bit key (crackable by brute force); AES supports 128/192/256-bit keys (far harder to break).
2. **Structure**: DES uses a Feistel structure with a small 64-bit block; AES uses a Substitution-Permutation Network with a larger 128-bit block, giving stronger diffusion of data.
3. **Design maturity**: AES was chosen through an open NIST competition and has more rounds with better resistance to modern cryptanalysis; DES has been practically broken since the late 1990s.

**Securing Online Banking (synthesis):** Digital certificates authenticate the bank's server via a CA. Public/private key cryptography (via TLS/SSL handshake) encrypts session data. Firewalls filter malicious traffic at the network boundary. Together these provide **confidentiality, authentication, integrity, and access control**.

### Memory Trick
**"Public key LOCKS (encrypt), Private key OPENS (decrypt)"** for confidentiality.
**"Private key SIGNS, Public key VERIFIES"** for digital signature.
**AES vs DES: "A for Advanced, bigger key, safer"**

---

# Quick Reference — Important Protocol Names & Ports

| Protocol | Full Name | Port | Purpose |
|---|---|---|---|
| **HTTP** | HyperText Transfer Protocol | 80 | Web browsing |
| **HTTPS** | HTTP Secure | 443 | Secure web browsing |
| **FTP** | File Transfer Protocol | 21 (control), 20 (data) | File transfer |
| **SMTP** | Simple Mail Transfer Protocol | 25 | Sending email |
| **POP3** | Post Office Protocol v3 | 110 | Receiving email |
| **DNS** | Domain Name System | 53 | Name resolution |
| **TCP** | Transmission Control Protocol | — | Reliable, connection-oriented |
| **UDP** | User Datagram Protocol | — | Unreliable, connectionless |
| **TFTP** | Trivial FTP | 69 | Simple file transfer |
| **Telnet** | — | 23 | Remote login |

---

# Master Mnemonics List

| Concept | Mnemonic |
|---|---|
| OSI 7 Layers (bottom-up) | **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way |
| TCP/IP 4 Layers | **N**ever **I**gnore **T**his **A**dvice (Network Access, Internet, Transport, Application) |
| Bit Stuffing rule | **5 ones → add a zero** |
| CRC steps | **A-X-R**: Append zeros, XOR divide, Remainder = CRC |
| Hamming parity positions | Always powers of **2** → 1, 2, 4, 8 |
| SMTP vs POP | **S**MTP **S**ends, **P**OP **P**ulls |
| Leaky vs Token Bucket | **L**eaky = **L**ocked constant rate; **T**oken = allows bursts |
| DNS hierarchy | **R**oot → **T**LD → **A**uthoritative (R-T-A) |
| Public vs Private key | **Public LOCKS, Private OPENS** (encryption); **Private SIGNS, Public VERIFIES** (signature) |
| Classful addressing | **A-B-C = 1-2-3 octets** used for Network ID |
| Go-Back-N ARQ | **ACK number = next expected frame** — retransmit from there |
| Distance Vector vs Link State | **DV = gossip with neighbors; LS = broadcast to everyone** |

---

### Final Exam Strategy
- Attempt all questions from this list first — they carry the **highest probability of repetition**.
- For every numerical (CRC, Hamming, Dijkstra's, Fragmentation, Go-Back-N, Header decode), **show all working steps** — partial marks are given even for a wrong final answer.
- Always draw the **diagram/table** where mentioned — DBATU examiners give separate marks for diagrams.
- Keep answers **structured with headings and bullet points** — this matches the DBATU answer-sheet style and scores full marks faster.

**Good luck — focus on these 20 questions and you'll be ready for close to a full paper.**
