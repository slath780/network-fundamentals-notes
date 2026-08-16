# Data Flow and Packet Journey

## Overview

A network is not simply a collection of connected devices.

When one device communicates with another, data passes through multiple components, protocols, and layers before reaching its destination.

The general communication flow is:

```text
Application
    ↓
Socket
    ↓
Kernel
    ↓
Transport Protocol
    ↓
IP
    ↓
Network Interface
    ↓
Network
    ↓
Routers
    ↓
Destination Network
    ↓
Destination Host
```

---

## 1. How Data Moves Between Devices

Assume a device wants to send data to another device.

For example:

```text
Host A
192.168.1.10
     |
     v
  Router
     |
     v
  Network
     |
     v
Host B
192.168.5.20
```

The process begins inside an application.

The application creates data and uses a network socket to request communication from the operating system.

The application does not directly control the network hardware.

Instead:

```text
Application
     ↓
Socket
     ↓
Kernel
```

The Linux kernel handles the networking operations and prepares the data for transmission.

The data is then processed by the networking stack and sent through the appropriate network interface.

---

## 2. Encapsulation

Data does not travel through the network as plain application data.

Each networking layer adds information required for communication.

Conceptually:

```text
Application Data
      ↓
TCP Segment
      ↓
IP Packet
      ↓
Ethernet / Wi-Fi Frame
```

This process is called:

**Encapsulation**

The resulting structure can be represented as:

```text
Frame
└── Packet
    └── Segment
        └── Application Data
```

---

## 3. Segment

A TCP Segment is the unit of data handled by TCP.

TCP adds information such as:

- Source Port
- Destination Port
- Sequence Number
- Acknowledgment information
- TCP Flags

TCP is responsible for transport-level communication between applications.

It provides mechanisms for:

- Reliable delivery
- Ordering
- Retransmission
- Flow control

---

## 4. Packet

An IP Packet contains an IP header and its payload.

The IP header contains information such as:

- Source IP Address
- Destination IP Address
- TTL
- Protocol information

The Destination IP is particularly important for routing.

Routers examine the destination IP to determine where the packet should be forwarded.

Conceptually:

```text
Source IP
     ↓
Destination IP
     ↓
Routing decision
     ↓
Next Hop
```

---

## 5. Frame

A Frame is the data unit used at the local network-link level.

For Ethernet, the frame contains information such as:

- Source MAC Address
- Destination MAC Address
- Payload
- Error-detection information

The frame allows data to be transmitted across the current local link.

Therefore:

```text
Segment → Transport level
Packet  → Network level
Frame   → Local link level
```

---

## 6. Packet Journey Through the Network

A packet usually does not travel directly from the source device to the destination.

It travels through multiple network hops.

Example:

```text
Host A
   ↓
Router A
   ↓
Router B
   ↓
Router C
   ↓
Router D
   ↓
Host B
```

Each router receives the packet and examines its destination IP.

The router then consults its routing table and determines the appropriate next hop.

Conceptually:

```text
Destination IP
      ↓
Routing Table
      ↓
Best Matching Route
      ↓
Next Hop
```

The process is repeated by each router until the packet reaches the destination network.

---

## 7. Routing and Next Hop

A router does not necessarily know the complete physical path from the source to the destination.

Instead, each router makes a local forwarding decision.

For example:

```text
Destination Network    Next Hop

192.168.1.0/24         Directly Connected
192.168.5.0/24         10.0.0.2
0.0.0.0/0              10.0.0.1
```

If the destination is:

```text
192.168.5.20
```

the router selects the appropriate route and forwards the packet toward the next hop.

When multiple routes match, routing generally uses the most specific matching route, known as:

**Longest Prefix Match**

---

## 8. Frames Change Between Hops

The packet may travel across multiple network links.

The frame used on one link does not necessarily remain the same on the next link.

Conceptually:

```text
Link 1:

Frame A
└── Packet
    └── Segment


Router


Link 2:

Frame B
└── Packet
    └── Segment
```

The local frame is removed and a new frame is created for the next link.

This is because MAC addresses are relevant to the current local link, while IP addressing provides the logical destination used for routing.

---

## 9. Role of Protocols

Network communication depends on multiple protocols.

Each protocol solves a different problem.

### Application Protocol

Examples:

- HTTP
- DNS
- SSH

Application protocols define how applications communicate and what information they exchange.

---

### TCP

TCP provides transport-level communication between applications.

It uses ports to identify application endpoints and provides mechanisms such as:

- Ordering
- Acknowledgments
- Retransmission
- Flow control

---

### IP

IP provides logical addressing and routing.

It answers the question:

> Where should this packet go?

It uses:

```text
Source IP
Destination IP
```

---

### Ethernet / Wi-Fi

These protocols handle communication across the local network link.

They use information such as MAC addresses to deliver frames across the current link.

---

## 10. Decapsulation

When the data reaches the destination host, the receiving system processes the layers in the opposite direction.

Conceptually:

```text
Frame
   ↓
Packet
   ↓
Segment
   ↓
Application Data
```

The network interface receives the frame.

The kernel processes the network information and delivers the appropriate transport data to the correct socket.

Finally, the application receives the original data.

---

## 11. Complete Communication Model

The complete conceptual flow is:

```text
Application
     ↓
Socket
     ↓
TCP
     ↓
IP
     ↓
Network Interface
     ↓
Frame
     ↓
Network
     ↓
Router
     ↓
Next Hop
     ↓
Router
     ↓
Destination Network
     ↓
Destination Host
     ↓
Network Interface
     ↓
IP
     ↓
TCP
     ↓
Socket
     ↓
Application
```

---

## 12. Key Concepts

### Segment

Transport-layer unit associated with TCP.

### Packet

Network-layer unit associated with IP.

### Frame

Link-layer unit used to transfer data across a local network link.

### Hop

One step from one network device to the next, usually involving a router.

### Next Hop

The next router or network destination selected by a routing decision.

### Encapsulation

Adding protocol information as data moves down the networking stack.

### Decapsulation

Removing and processing protocol information as data moves up the networking stack.

---

## Final Mental Model

The most important idea is:

```text
Application
     ↓
Data
     ↓
Segment
     ↓
Packet
     ↓
Frame
     ↓
Network
     ↓
Hop
     ↓
Hop
     ↓
Hop
     ↓
Destination
     ↓
Frame
     ↓
Packet
     ↓
Segment
     ↓
Data
     ↓
Application
```

A network therefore works as a coordinated system of protocols and devices.

Applications generate the data, transport protocols manage communication between applications, IP provides logical addressing and routing, and link-layer technologies deliver frames across individual network links.