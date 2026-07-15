## What is a Computer Network?

A computer network is a group of connected devices that communicate and exchange data using standard communication protocols.

The main purpose of a network is to enable devices to share information and resources.

---

## Why Do We Use Networks?

Networks allow devices to:

- Exchange data
- Access shared resources
- Communicate with other devices
- Access services such as web servers and databases
- Connect to the Internet

---

## Basic Network Components

### Host

A host is any device connected to a network that has an IP address and can send or receive data.

Examples:

- Laptop
- Smartphone
- Server
- Printer

---

### Client

A client is a host that requests a service or resource from another device.

Example:

A web browser requesting a web page.

---

### Server

A server is a host that provides services or resources to clients.

Examples:

- Web Server
- SSH Server
- Database Server
- DNS Server

---

### Router

A router connects different networks together and forwards packets between them.

It allows devices in a local network to communicate with external networks such as the Internet.

---

### Switch

A switch connects devices within the same local network (LAN).

It forwards data only to the destination device, improving communication efficiency.

---

## Network Interface

A Network Interface is the connection point between a computer and the network.

Its responsibilities include:

- Sending data
- Receiving data
- Holding MAC and IP addresses
- Connecting the device to the network

Common interfaces include:

- Ethernet
- Wi-Fi
- Loopback (lo)

---

## How Programs Send Data

Programs do not communicate directly with network hardware.

The communication flow is:

```text
Program
    ↓
System Call
    ↓
Kernel
    ↓
Socket
    ↓
Network Interface
    ↓
Network Card
    ↓
Network
```

The Linux kernel manages network communication and sends data through the appropriate network interface.

---

## Linux Networking Commands

### hostname

Displays the system hostname.

### hostnamectl

Displays detailed system information, including the hostname.

### ip a

Displays available network interfaces, IP addresses, and interface status.

---

## Summary

- A network connects devices to exchange data.
- Every connected device is a host.
- Clients request services, while servers provide them.
- Routers connect different networks.
- Switches connect devices inside the same LAN.
- Network interfaces connect the operating system to the physical network.
- Programs send data through the Linux kernel using sockets and network interfaces.