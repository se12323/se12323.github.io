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
|[Application Layer](#http-protocol-application-layer)|7|users to access the network|HTTP, FTP, SNMP,DNS|Data
|Presentation Layer|6|Data (I/O data into a single expression) has the format of <span style="color:red">conversion, compression, encryption and decryption</span>|JPEG, MPEG, AFP|Data
|Session Layer|5|Compose communication session,<br/> <span style="color:red">Port connection/control/management</span>, etc.| <span style="color:blue">SSH</span>, TSL|Data
|[Transport Layer](#tcp-protocol-transport-layer)|4|<span style="color:red">Data Transmission(TCP)</span>|<span style="color:blue">TCP,UDP</span>|Segment
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


## [Ethernet II (**<span style="color:red">Data-Link Layer</span>**)](#osi-7-layer)
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
**: Indicate the header format following 'Ethernet II'(known as Ether Type)<br/>**
> - **c.f) In the picture, it is marked as IP (0x0800), which means that the IP header follows**


## [Internet Protocol - IPv4 Header (**<span style="color:red">Network Layer</span>**)](#osi-7-layer)
![IPv4 Header](/assets/img/nsad/wireshark_component/ipv4_header.png "IPv4 Header")
![IPv4 Header_EX](/assets/img/nsad/wireshark_component/ipv4_header_ex.png "IPv4 Header_EX")

- IPv4 is an IP address (32-bit) and plays a role in determining the route from the source to the destination.

- (If you see the packet, it seems to check the IP address of the source and destination)

> **<span style="color:black">Version</span>** 
**: Indicates the IP version<br/><br/>**
> **<span style="color:black">Header Length</span>** 
**: Indicates the length of the IP header (IP header used in general communication is 20 bytes without any options)<br/><br/>**
> **<span style="color:black">Differentiated Services Field</span>** 
**: Indicates the importance of the packet<br/>**
> - **c.f) In the picture, the sevice type and priority for communication are indicated<br/>**
> - **p.s) All 0's are displayed on the screen, which indicates standard priority without performing special bandwith control or QoS usch as 'remove unimportant packets'<br/><br/>**
> 
> **<span style="color:black">Total Length</span>** 
**: Indicates the total length of packet in bytes<br/><br/>**
> **<span style="color:black">Identification</span>** 
**: Indicates packet identification information<br/><br/>**
> **<span style="color:black">Flags</span>** 
**: Indicates packet identification information<br>**
> - **'Reserved bit' part is reserved for IP protocol extension in the future<br/>**
> - **'Don't Fragment' is a bit to prohibit packet fragmentation<br/>**
>   - **<span style="color:black">1</span> : Prohibit packet splitting**
>   - **<span style="color:black">0</span> : packet segmentation possible**
> - **'More Fragments' is a bit to indicate that fragmented packets are continued after<br/>**
>   - **<span style="color:black">1</span> : There are packets that are split and continue**
>   - **<span style="color:black">0</span> : No consecutive packets**
> 
> **<span style="color:black">Fragment offset</span>** 
**: Indicates the position of the current packet within the segmented packet<br/>** 
> - **c.f) In the picture, it is 0, which means it is the first packet)<br/><br/>**
>
> **<span style="color:black">Time to live</span>** 
**: Packet lifetime (how long it can survive)<br/>**
> - **p.s) This number has a structure in which the value decreases by 1 when a packet is transmitted to the network as it passes through the router<br/>**
> - **p.s) When the value becomes 0, the packet can no longer exist, and the packet is dropped by the router or layer 3 switch</br>**
> 
> **<span style="color:black">Protocol</span>** 
**: Specifies the header format to follow after the IP<br/>**
> - **c.f) In this picture, we can see that the TCP header is followed.<br/>**
> 
> **<span style="color:black">Header checksum</span>** 
**: Check whether the IP header of the packet is incorrect by comparing the calculated value by putting the contents of the IP header into the calculation formula and the header checksum value<br/><br/>**
> **<span style="color:black">Source</span>** 
**: Indicates the SOURCE IP address<br/><br/>**
> **<span style="color:black">Destination</span>** 
**: Indicates the DESTINATION IP address<br/><br/>**
> **<span style="color:black">Source GeoIP</span>** 
**: Refers to the GeoIP database from the source IP address to indicate the location where the IP address is connected.<br/><br/>**
> **<span style="color:black">Destination GeoIP</span>** 
**: Refers to the GeoIP database from the destination IP address to indicate the location where the IP address is connected.<br/><br/>**


## [TCP Protocol (**<span style="color:red">Transport Layer</span>**)](#osi-7-layer)
![TRANSPORT](/assets/img/nsad/wireshark_component/transport.png "TRANSPORT")
![TRANSPORT_EX](/assets/img/nsad/wireshark_component/transport_ex.png "TRANSPORT_EX")

- The yellow box contains information about the transport layer and TCP Protocol.
> **<span style="color:black">Source Port</span>** 
**: Port number that identifies the application process of the sending side<br/><br/>**
> **<span style="color:black">Destination Port</span>** 
**: Port number that identifies the application process on the receiving side<br/><br/>**
> **<span style="color:black">Stream index</span>** 
**: In Wireshark, in order to make it easier to trace or analyze a TCP connection, it analyzes the stream from the beginning to the end of the TCP connection as a single TCP stream, and assigns the stream number in the order in which it appears in the packet.<br/>**
> - **c.f) In this picture, since it is the third TCP stream, index number 3 is attached.<br/><br/>**
> 
> **<span style="color:black">TCP Segment Len</span>** 
**: Indicates length of TCP stream<br/><br/>**
> **<span style="color:black">Sequence number</span>** 
**: The position of the TCP segment currently being transmitted is displayed as a number.<br/><br/>**
> **<span style="color:black">Next sequence number</span>** 
**: The next sequence number appears (Actually, it is a number obtained by adding the size of the TCP data to be transmitted to the current sequence number)<br/><br/>**
> **<span style="color:black">Acknowledgement number</span>** 
**: Indicates position of the received TCP segment<br/>**
> - **The number of bytes received becomes the acknowledgment number<br/>**
> - **The acknowledgment number is set to the *initial sequence number + 1* at the time of connection, and the number of bytes in the receive segment is added<br/>**
> 
> **<span style="color:black">Header Length</span>** 
**: The size of the TCP header is displayed<br/>**
> - **Just like the IP header, the length of the header without options is 20 bytes<br/><br/>**
>
> **<span style="color:black">Flags</span>** 
**: Control communication<br/>**
> - **Reserved: a part reserved for future expansion of the TCP protocol<br/>**
> - **Nonce: a value is used in a structure called ECN-nonce, and is used for packet congestion control with the following ECN-Echo<br/>**
> - **Congestion Window Reduced: is used to reduce the size of data sent once when the network is congested<br/>**
> - **Urgent: used with the IP option to embed urgent data into normal communication (It is not used for security reasons) (called urgent pointer flag)<br/>**
> - **Acknowledgment: is also called ACK flag, and when 'ON', the acknowledgment number is validated<br/>**
> - **Push: when it is 'ON', the push function that collects the data accumulated in the receive buffer until then and passes it to the program becomes effective (By collecting information and passing it on to the program, efficient communication can be achieved) (called PSH flag)<br/>**
> - **Reset: when it's ON, TCP communication is forcibly terminated. (Like a firewall, this can prevent a virus attack by adding the RST flag to the packet sent from the other party) (called RST flag)<br/>**
> - **Syn: is used to start communication (called the SYN flag)<br/>**
> - **Fin: is used as a communication termination means (called FIN flag)<br/>**
>
> **<span style="color:black">Window Size</span>** 
**: Represents a receive buffer for continuously receiving TCP packets (also called RWIN)<br/><br/>**
> **<span style="color:black">Checksum</span>** 
**: Check the contents of the TCP header and its segment<br/><br/>**
> **<span style="color:black">SEQ/ACK analysis</span>** 
**: Function that is added in header by expert is displayed in '[  ]'.<br/><br/>**


## [HTTP Protocol (**<span style="color:red">Application Layer</span>**)](#osi-7-layer)
![APPLICATION](/assets/img/nsad/wireshark_component/application.png "APPLICATION")
![APPLICATION_EX](/assets/img/nsad/wireshark_component/application_ex.png "APPLICATION_EX")


