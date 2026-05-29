# Packet Observations

## DNS Observation

Observed DNS queries and responses for google.com using Wireshark.

Filter used:
dns

---

# TCP Observation

Observed TCP 3-way handshake:
- SYN
- SYN-ACK
- ACK

Filter used:
tcp

---

# TLS Observation

Observed TLS handshake packets during HTTPS connection.

Filter used:
tls

---

# General Observation

Opening a website generates multiple packets:
- DNS
- TCP
- TLS
- HTTP/HTTPS traffic