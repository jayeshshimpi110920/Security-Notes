The **Transport Layer (Layer 4)** of the OSI Model handles the reliable delivery of data between devices. Two primary protocols operate at this layer: **TCP (Transmission Control Protocol)** and **UDP (User Datagram Protocol)**. Here's a breakdown of both:

---

### **TCP (Transmission Control Protocol)**
- **Connection-oriented**: TCP establishes a connection before transmitting data. It ensures that data is delivered in the correct order, without errors.
- **Reliable**: TCP ensures reliable delivery by using acknowledgment packets (ACK) to confirm receipt of data. If data is lost or corrupted, TCP retransmits it.
- **Flow control**: TCP uses flow control mechanisms to prevent the sender from overwhelming the receiver.
- **Error detection**: TCP checks for errors during transmission and ensures that data arrives correctly.
- **Segment sequencing**: TCP splits data into smaller chunks called "segments" and sequences them so they can be reassembled in the correct order.
- **Applications**: Used where reliability is critical (e.g., web browsing, email, file transfers).
  - **Examples**: HTTP/HTTPS, FTP, SMTP, Telnet.

**How TCP works**:
1. **Three-way handshake**: TCP establishes a connection by performing a three-step process:
   - SYN (synchronize): The sender sends a SYN request to start the connection.
   - SYN-ACK: The receiver acknowledges the SYN request and responds with SYN-ACK.
   - ACK: The sender sends an ACK back, and the connection is established.
2. **Data transfer**: TCP sends data segments, ensuring they are received in the correct order and without errors.
3. **Connection termination**: Once data transmission is complete, TCP performs a four-step process to close the connection.

---

### **UDP (User Datagram Protocol)**
- **Connectionless**: UDP does not establish a connection before transmitting data. It sends data as "datagrams" without guaranteeing delivery.
- **Unreliable**: Unlike TCP, UDP does not provide acknowledgments or retransmissions. Data might arrive out of order or be lost entirely.
- **No flow control**: UDP does not manage how much data is sent at once, so there's a risk of overwhelming the receiver.
- **Low overhead**: UDP is faster than TCP because it doesn't perform error checking or retransmission, making it ideal for time-sensitive applications.
- **Applications**: Used where speed is critical, and occasional data loss is acceptable (e.g., streaming, gaming, voice over IP).
  - **Examples**: DNS, VoIP, online gaming, video streaming (e.g., Netflix, YouTube).

**How UDP works**:
1. **No handshake**: UDP sends datagrams directly without establishing a connection.
2. **Data transfer**: Each datagram is sent independently, and there’s no guarantee it will reach its destination. UDP doesn’t track which data was received.
3. **No closing**: Since there’s no connection, UDP simply stops sending data when finished.

---

### **Key Differences Between TCP and UDP**:

| Feature            | **TCP**                               | **UDP**                            |
|--------------------|---------------------------------------|------------------------------------|
| **Connection**     | Connection-oriented                   | Connectionless                     |
| **Reliability**    | Reliable (ensures delivery and order) | Unreliable (no guarantees)         |
| **Speed**          | Slower (due to error-checking, etc.)  | Faster (low overhead)              |
| **Error Checking** | Yes (includes checks and retransmits) | No (errors are not corrected)      |
| **Use Cases**      | Web browsing, email, file transfer    | Streaming, gaming, DNS lookups     |

In summary:
- **Use TCP** when reliability and order matter (e.g., loading a webpage).
- **Use UDP** when speed is more important than reliability (e.g., watching a live stream).

---
### **What is a Datagram?**

A **datagram** is a basic unit of data transfer in a **connectionless** communication protocol, specifically in the **User Datagram Protocol (UDP)**. It is a self-contained packet of data that carries enough information to be routed from the sender to the receiver without needing an established connection between the two. Unlike the packets in **TCP**, datagrams are sent without acknowledgment, meaning there's no guarantee of delivery, order, or error-checking.

### Key Characteristics of a Datagram:
- **Connectionless**: Sent without establishing a prior connection between the sender and receiver.
- **Independent**: Each datagram is treated independently, with no relation to other datagrams.
- **Unreliable**: No guarantee that the datagram will reach its destination, and if it does, it may not be in order.
- **No error correction**: UDP does not check for or correct errors in the datagram.

### **Which Protocol is Used When You Search for "www.google.com"?**

When a user searches for **www.google.com** (or any website), a combination of **UDP** and **TCP** protocols are used during the process, specifically for **DNS resolution** and **HTTP/HTTPS requests**.

1. **Step 1: DNS Lookup (UDP)**
   - The first thing your computer does is resolve the domain name (www.google.com) into an IP address. This is done using the **Domain Name System (DNS)**.
   - **UDP** is used for DNS queries because it's faster and does not require a connection. If the DNS query fails, it simply retries.
   - The DNS query is sent to a DNS server, and the server responds with the IP address of **www.google.com**.
   - **Protocol**: **UDP** (usually on port 53).

2. **Step 2: Connecting to the Web Server (TCP)**
   - Once your browser knows the IP address of **www.google.com**, it establishes a connection with Google's web server to retrieve the webpage.
   - **TCP** is used here because HTTP (or HTTPS for secure connections) requires a reliable connection to ensure that the web page data (HTML, CSS, images) arrives correctly and in order.
   - The browser uses the **TCP** protocol to establish a reliable connection with the web server via a **three-way handshake**.
   - **Protocol**: **TCP** (usually on port 80 for HTTP, or port 443 for HTTPS).

### **Summary of the Process:**
- **DNS lookup**: Uses **UDP** for fast, connectionless domain name resolution.
- **Fetching the webpage**: Uses **TCP** for reliable data transfer when retrieving the web page content.

So, when you search for **www.google.com**, both **UDP (for DNS)** and **TCP (for web page retrieval)** are used.
