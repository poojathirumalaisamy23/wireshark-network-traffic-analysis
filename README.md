# Task 5: Capture and Analyze Network Traffic Using Wireshark

## 📌 Objective
Capture live network packets on a Kali Linux environment and identify basic protocols and traffic types.

## 🛠️ Tools Used
- **OS:** Kali Linux
- **Tool:** Wireshark (CLI: `tshark` version 4.6.6)
- **Interface:** `eth0` (VirtualBox NAT)

## 📊 Capture Summary
- **File:** `capture.pcap`
- **Total Packets:** 77
- **File Size:** 17 KB
- **Duration:** ~30 seconds

## 🔍 Protocols Identified
During the capture window, the following 6 protocols were successfully identified:

| Protocol | Frames | Bytes | Description |
|----------|--------|-------|-------------|
| **DNS** | 14 | 1,277 | Domain resolution (nslookup openai.com) |
| **ICMP** | 16 | 1,568 | Ping requests/replies (google.com & 8.8.8.8) |
| **TCP** | 33 | 10,368 | Transport layer connections (HTTPS) |
| **TLS** | 13 | 7,524 | Encrypted HTTPS session (example.com) |
| **ARP** | 8 | 424 | MAC address resolution for local gateway |
| **IPv6/ICMPv6** | 39 / 6 | 11,076 / 708 | Modern stack traffic & neighbor discovery |

## 📸 Evidence & Screenshots

### 1. Capture & Protocol Hierarchy
Using `tshark -i eth0 -w capture.pcap` and analyzing it with `-z io,phs`.
![Capture and Protocols](screenshots/01_tshark_capture_and_protocols.png)

### 2. Traffic Generation (Ping & DNS)
Generating ICMP and DNS traffic during the capture window.
![Traffic Part 1](screenshots/02_traffic_generation_part1.png)

### 3. Traffic Generation (HTTPS & ICMP)
Generating TLS/HTTPS traffic via cURL and more ICMP traffic.
![Traffic Part 2](screenshots/03_traffic_generation_part2.png)

## 💡 Findings & Conclusion
- The capture successfully recorded a mix of diagnostic (ICMP), resolution (DNS/ARP), and web browsing (TCP/TLS) traffic.
- While HTTPS payloads (TLS) are encrypted, metadata such as IP addresses, ports, and DNS queries remain visible in plaintext.
- A total of 6 distinct protocols were identified, exceeding the assignment requirement of at least 3.

## 🚀 How to Reproduce
1. Start the capture: `tshark -i eth0 -w capture.pcap`
2. Generate traffic in a separate terminal: 
   `ping -c 4 google.com; nslookup openai.com; curl -I https://example.com`
3. Stop the capture (`Ctrl+C`) and analyze: `tshark -r capture.pcap -q -z io,phs`# wireshark-network-traffic-analysis
Task 5: Network Traffic Analysis
