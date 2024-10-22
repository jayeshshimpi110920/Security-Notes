## 7-layer OSI model (Open Systems Interconnection)
It is a 7-layer architecture with each layer having specific functionality to perform. All these 7 layers work collaboratively to transmit the data from one person to another across the globe. When we transfer information from one device to another, it travels through 7 layers of OSI model. First data travels down through 7 layers from the sender’s end and then climbs back 7 layers on the receiver’s end.

![image](https://github.com/user-attachments/assets/4f965446-c150-433f-9ab2-27ff41c11b05)

Let’s look at it with an Example:

Luffy sends an e-mail to his friend Zoro.

**Step 1:** Luffy interacts with e-mail application like Gmail , outlook , etc. Writes his email to send. (This happens in Layer 7: Application layer )

**Step 2:** Mail application prepares for data transmission like encrypting data and formatting it for transmission. (This happens in Layer 6: Presentation Layer )

**Step 3:** There is a connection established between the sender and receiver on the internet. and ensure the session is open during data transmission (This happens in Layer 5: Session Layer )

**Step 4:** Email data is broken into smaller segments. It adds sequence number and error-checking information to maintain the reliability of the information. (This happens in Layer 4: Transport Layer )

**Step 5:** Addressing of packets is done in order to find the best route for transfer.The segments are packaged into packets and an IP address is attached (both source and destination addresses) so the data knows where it’s going. Routers determine the best path for the data (This happens in Layer 3: Network Layer )

**Step 6:** Data packets are encapsulated into frames, then MAC address is added for local devices and then it checks for error using error detection. (This happens in Layer 2: Data Link Layer ) The packets are framed for delivery to the physical network (such as Wi-Fi or Ethernet).

**Step 7:** Lastly Frames are transmitted in the form of electrical/ optical signals over a physical network medium like ethernet cable or WiFi.
After the email reaches the receiver i.e. Zoro, the process will reverse and decrypt the e-mail content. At last, the email will be shown on Zoro’s email client. The frames are converted into electrical, light, or radio signals that physically travel through cables, fiber optics, or wireless signals to the destination.
These raw bits are sent over the physical medium (e.g., network cables, Wi-Fi).

---
Data flows through the OSI model in a step-by-step process:

* Application Layer: Applications create the data. **HTTP, FTP, DNS, SMTP (email).** Devices: Proxy servers, firewalls (can operate at application layer).
* Presentation Layer: Data is formatted and encrypted.  **SSL/TLS for encryption, JPEG, GIF for formats.**
* Session Layer: Connections are established and managed. **Session establishment protocols like SMB (Server Message Block), PPTP (Point-to-Point Tunneling Protocol).**
* Transport Layer: Data is broken into segments for reliable delivery.**TCP (Transmission Control Protocol), UDP (User Datagram Protocol).** Devices: Gateways, firewalls (operating at transport layer).
* Network Layer : Segments are packaged into packets and routed. Examples: **IP addresses, routers.** Devices: Routers, layer-3 switches.
* Data Link Layer: Packets are framed and sent to the next device. Examples: **MAC (Media Access Control) addresses, switches**. Devices: Switches, bridges.
* Physical Layer: Frames are converted into bits and transmitted physically. Examples: **Ethernet cables, fiber optics, radio frequencies**. Devices: Hubs, repeaters, network interface cards (NICs).
















