---
layout: post
title: Wireshark Component
description: >
  I've put necessary terms that we can see when we using Wireshark
sitemap: false
group: true
hide_last_modified: true
image: /assets/img/nsad/wireshark_component/wireshark.jpeg
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
|[Network Layer](#internet-protocol---ipv4-header-network-layer)|3|<span style="color:red">Establishing data transmission routes</span><br/>(responsible for routing between physical networks)|IP, ICMP|<span style="color:blue">Packet</span>
|[Data-Link Layer](#ethernet-ii-data-link-layer)|2|Data <span style="color:red">error detection</span>, flow control|<span style="color:blue">Ethernet</span>|Frame
|Physical Layer|1|Converts <span style="color:red">data into electrical signals</span>|HUB wire, fiber optic cable|<span style="color:blue">Bit</span>


## Frame # (Packet Brief Explanation)
![Frame](/assets/img/nsad/wireshark_component/frame.png "Frame")
> **<span style="color:black">Interface id</span>** 
**: Order of the packets arriving<br/><br/>**
> **<span style="color:black">Encaptulation type</span>** 
**: Encapsulation type of the packet<br/><br/>**
> **<span style="color:black">Arrival Time</span>** 
**: The time the packet was captured<br/><br/>**
> **<span style="color:black">Time shift for this packet</span>** 
**: Use the time shift function to shift the packet display time (generally 0)<br/><br/>**
> **<span style="color:black">Epoch Time</span>** 
**: Serial value in Unix time format (seconds relative to 01/01/1970 00:00)<br/><br/>** 
> **<span style="color:black">Time delta from previous captured frame</span>**
**: Interval from the last captured frame in seconds<br/><br/>**
> **<span style="color:black">Time delta from previous displayed frame</span>**
**: Interval from the last displayed frame in 'seconds'<br/><br/>**
> **<span style="color:black">Time since reference or first frame</span>**
**: The elapsed time from capturing the first packet to capturing the currently selected packet is expressed in 'seconds'<br/><br/>**
> **<span style="color:black">Frame Number</span>**
**: The number of the first captured packet is set to '1', and the number of the captured packet is displayed as a sequence number after that<br/><br/>**
> **<span style="color:black">Frame Length</span>**
**: Size of the packet<br/><br/>**
> **<span style="color:black">Capture Length</span>**
**: Frame size when captured (usually 10 and 11 are the same value, in bytes)<br/><br/>**
> **<span style="color:black">Frame is makred</span>**
**: True or false indicating whether the frame was marked by Wireshark<br/><br/>**
> **<span style="color:black">Frame is ignored</span>**
**: True or false indicating whether the frame was ignored by Wireshark<br/><br/>**
> **<span style="color:black">Protocols in frame</span>**
**: Header included in the packet<br/><br/>**
> **<span style="color:black">Number of per-protocol-data</span>**
**: Number of data included by protocol<br/><br/>**
> **<span style="color:black">Hypertext Transfer Protocol</span>**
**: Information of HTTP protocol<br/><br/>**
> **<span style="color:black">Coloring Rule Name</span>**
**: The name of the rule wireshark used for coloring<br/><br/>**
> **<span style="color:black">Coloring Rule String</span>**
**: Display filter for rules that Wireshark uses for coloring<br/><br/>**


## Ethernet II (**L2<span style="color:red"> Data-Link Layer</span>**)
![Ethernet II](/assets/img/nsad/wireshark_component/ethernet.png "Ethernet II")
![Ethernet II_EX](/assets/img/nsad/wireshark_component/ethernet_ex.png "Ethernet II_EX")

- Packets in red squares are MAC-related information. This part contains ***MAC protocol*** information<br/>
(p.s. ***MAC (physical address) protocol*** : Protocol structure according to IEEE802 standard of DataLinkLayer)
- **MAC address**: The **<span style="color:red">48-bit</span>** hardware address of the network card.<br/>

> **<span style="color:black">Destination</span>** 
**: MAC address of the DESTINATION LAN card<br/><br/>**
> **<span style="color:black">Source</span>** 
**: MAC address of the SOURCE LAN card<br/><br/>**
> **<span style="color:black">Type</span>** 
**: Indicate the header format following 'Ethernet II'(known as Ether Type)<br/><br/>**
> **c.f) In the figure, it is marked as IP (0x0800), which means that the IP header follows**


## Internet Protocol - IPv4 Header (**L3<span style="color:red"> Network Layer</span>**)
![IPv4 Header](/assets/img/nsad/wireshark_component/ipv4_header.png "IPv4 Header")
![IPv4 Header_EX](/assets/img/nsad/wireshark_component/ipv4_header_ex.png "IPv4 Header_EX")