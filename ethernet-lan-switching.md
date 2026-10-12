# Ethernet Local Area Network Switching

Day 5 of CCNA 200-301 Course by Jeremy IT Lab

## Local Area Network

### What is it?

A network in a relatively small area which can only communicate between devices in the same area.

## Ethernet Frame

### Remind me, what does it consist of?

Ethernet frame exists on the layer 2 of TCP/IP model.
It has a packet encapsulated with an ethernet header and a trailer.

### We know what a packet is, now what about the header and trailer?

#### Header

Header consists of

1. Preamble, 7 bytes where each byte is 10101010, this allows device to synchronize receiver clocks
2. SFD (Start Frame Delimiter), 1 byte with value 10101011, which indicates the end of the preamble and the start of the rest of the frame
3. Destination, 6 bytes indicating the destination MAC address
4. Source, 6 bytes indicating the source MAC address
5. Type/Length, 2 bytes field

   If value is < 1500, it indicates the length of the packet.

   If it is > 1536, it indicates the type of the packet. Length is calculated with other methods.
   Example: IPv4 = 0x0800 = 2048, IPv6 = 0x86DD = 34525

#### Trailer

- Trailer consists of a "Frame Check Sequence" (FCS)
- It is 4 bytes in length
- It detects corrupted data by running a Cyclic Redundancy Check (CRC) algorithm over the received data

So total, the header and trailer is made of 26 bytes

### What is the minimum size of an ethernet frame?

It has a minimum size of 64 bytes

### What does those 64 bytes consist of?

- The preamble and SFD is usually not considered part of the frame, meaning header + trailer is only 18 bytes
- Minimum payload size is 46 bytes

### What if payload is less than 46 bytes?

Padding bytes are added, which are zero bytes until it is total 46 bytes

## MAC Address

### What is it?

A 6-byte globally unique physical address assigned to the device when it is made.

First 3 bytes: OUI (Organizationally Unique Identifier), it is assigned to the company making the device

Last 3 bytes: Unique identifier of the device

## Switch Mechanism

### Unicast Frame

A unicast frame is a frame with a single destined target.

An unknown unicast frame is a frame whose destined target is not known by the switch.

A known unicast frame is a frame whose destined target is known by the switch

### How does a frame reach its target?

- A switch holds a MAC address table

  | MAC   | Interface |
  | ----- | --------- |
  | .0001 | F0/1      |

- A switch learns MAC address dynamically through source MAC Address of a frame -> Dynamic Mac Address

  If a MAC address does not exist in the address table, the device who sends a frame gets its source MAC address stored with the source interface from

### What if the MAC address table does not contain the destined target (unknown unicast frame)?

A FLOOD HAPPENS!

Meaning the unknown unicast frame is sent through all interfaces except where it came from.

The device that has the same destined MAC address processes the frame normally. If the device wants to send a reply, a frame with switched source and destination MAC addresses gets sent to the switch through the interface. Then, the switch can register its MAC address, associating it with the interface.

The device with a different MAC address simply drops the frame.

### How long are the dynamic addresses stored in the table

If a dynamic MAC address is not used for 5 minutes, it is erased from the table.

## IP Addresses

### Where are IP address located inside a frame?

Inside the payload of the ethernet frame is the Internet Protocol (IP) packet

### What does it consist of?

It has a source IP address, destination IP Address, and source MAC address, with an unknown destination MAC address

### How does it find the destination MAC Address?

Using address resolution protocol (ARP)

## Address Resolution Protocol (ARP)

### What is it used for?

It is to discover Layer 2 address (MAC Address) using a known Layer 3 Address (IP Address)

### What messages does it consist of?

- ARP Request
- ARP Reply

### ARP Request

ARP Request has these fields:

| Field   | Value          |
| ------- | -------------- |
| Src IP  | 192.168.0.1    |
| Dst IP  | 192.168.0.3    |
| Src MAC | AAAA.AA00.0001 |
| Dst Mac | FFFF.FFFF.FFFF |

The MAC Address FFFF.FFFF.FFFF indicates that it is a broadcast MAC Address, which has the same mechanism as a flood; it sends to all interface except source interface until it reaches the target device that has the specified Dst IP

### ARP Reply

ARP Reply has these fields:

| Field   | Value          |
| ------- | -------------- |
| Src IP  | 192.168.0.3    |
| Dst IP  | 192.168.0.1    |
| Src Mac | AAAA.AA00.0003 |
| Dst MAC | AAAA.AA00.0001 |

The target knows the Dst MAC from the previous Src MAC, so it simply reverses the src and dst ip, and sets its own MAC Address in the Src MAC.

Since it only has one target, it is unicast, and the original sender will obtain the target's MAC Address.

### ARP Table

Each host device stores an ARP table which associates an IP Address with a MAC Address and notes if they are statically or dynamically alocated.

## Ping

### What is it for?

A network utility that is used to check if a device has connection to other device.

### What can it measure?

Round trip time, which is the time it takes to send a packet to the target and back

### Back? What do you mean

The messages used are:

- ICMP Echo Request
- ICMP Echo Reply

So it means the target sending the reply back

## Cisco IOS Commands

### Ping

`ping [address] size [size]`

Ex. `ping 192.168.0.3`, `ping 192.168.0.3 size 36`

### See ARP table

`show arp`

### Show MAC address tabel on switch

`show mac address-table`

### Clear all dynamic MAC address

`clear mac address-table dynamic`

### Clear specific dynamic MAC address

`clear mac address-table dynamic address [mac-address]`

### Clear specific dynamic MAC address from interface

`clear mac address-table dynamic interface [interface]`
