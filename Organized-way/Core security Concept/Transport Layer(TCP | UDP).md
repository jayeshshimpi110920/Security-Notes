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
