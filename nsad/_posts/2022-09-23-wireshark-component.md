---
layout: post
title: Wireshark Component
description: >
  I've put necessary terms that we can see when we using Wireshark
sitemap: false
group: true
hide_last_modified: true
image: /assets/img/wireshark.jpeg
---
## Inspecting Wireshark

## Wireshark
Wireshark is simply a packet capture analysis program that helps you analyze packets.


## OSI 7 layer 
**OSI** known as **Open Systems Interconnection Reference Mode**, is a model developed by the International Organization for Standardization (ISO), it shows the communication process by dividing it into 7 steps.


| Name | Layer | Function | Protocol Suite | Unit of Data in Protocol (PDU) |
|------|-------|----------|----------------|--------------------------------|
|Application Layer|7|Allows users to access the network|HTTP, FTP, SNMP,DNS|Data
|Presentation Layer|6|Data (I/O data into a single expression) has the format of <span style="color:red">conversion, compression, encryption and decryption</span>|JPEG, MPEG, AFP|Data
|Session Layer|5|Compose communication session,<br/> <span style="color:red">Port connection/control/management</span>, etc.| <span style="color:blue">SSH</span>, TSL|Data
|Transport Layer|4|Reliable <span style="color:red">Data Transmission(TCP)</span>|<span style="color:blue">TCP,UDP</span>|Segment
|Network Layer|3|<span style="color:red">Establishing data transmission routes</span><br/>(responsible for routing between physical networks)|IP, ICMP|<span style="color:blue">Packet</span>
|Data-Link Layer|2|Data <span style="color:red">error detection</span>, flow control|<span style="color:blue">Ethernet</span>|Frame
|Physical Layer|1|Converts <span style="color:red">data into electrical signals</span>|HUB wire, fiber optic cable|<span style="color:blue">Bit</span>


##