# Network Discovery and Port Scanning Lab

## Overview

This project demonstrates basic network reconnaissance using Nmap and packet analysis using Wireshark on a local network. The objective was to identify active hosts, discover open ports, and analyze the network traffic generated during the scan.

## Tools Used

* Nmap 7.99
* Zenmap
* Wireshark
* Windows 11

## Objectives

* Discover active devices on the local network
* Identify open ports and running services
* Capture scan traffic using Wireshark
* Analyze TCP SYN scan behavior
* Document findings and potential security considerations

## Network Discovery

A host discovery scan was performed against the local subnet:

```bash
nmap -sn 192.168.1.0/24
```

### Results

Six active hosts were detected on the network, including the router and several client devices.

## Port Scanning

A SYN Stealth Scan was performed against the router:

```bash
nmap -sS -Pn 192.168.1.1
```

### Open Ports Identified

| Port      | Service                |
| --------- | ---------------------- |
| 53/tcp    | DNS                    |
| 80/tcp    | HTTP                   |
| 443/tcp   | HTTPS                  |
| 52869/tcp | Dynamic/Router Service |

## Wireshark Analysis

Traffic generated during the Nmap scan was captured and analyzed using Wireshark.

### Display Filters Used

```text
tcp.flags.syn == 1
```

Used to identify SYN packets sent by Nmap.

```text
tcp.flags.syn == 1 && tcp.flags.ack == 1
```

Used to identify SYN-ACK responses from open ports.

```text
tcp.flags.reset == 1
```

Used to identify closed ports responding with TCP Reset packets.

### Findings

* Nmap generated TCP SYN probes to multiple destination ports.
* Open ports responded with SYN-ACK packets.
* Closed ports responded with RST packets.
* Traffic analysis confirmed the behavior of a TCP SYN (Stealth) Scan.

## Security Considerations

* HTTP services may expose web management interfaces without encryption.
* HTTPS services should use strong authentication and updated certificates.
* DNS services should be restricted to authorized clients.
* Unknown or high-numbered ports should be reviewed periodically.

## Files Included

* `network_scan.txt` - Host discovery results
* `.nmap` / XML scan output
* `packets.pcapng` - Wireshark packet capture
* Screenshots of Zenmap and Wireshark analysis

## Learning Outcomes

Through this project I gained practical experience with:

* Network reconnaissance
* Host discovery techniques
* TCP SYN scanning
* Packet capture and protocol analysis
* Basic security assessment of network services

## Disclaimer

This project was conducted on devices and networks owned by or authorized for testing by the researcher. The techniques demonstrated are intended solely for educational and defensive security purposes.
