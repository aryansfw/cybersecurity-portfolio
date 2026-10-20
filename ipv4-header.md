# IPv4 Header

Day 10 of CCNA 200-301 course by Jeremy IT Lab

## What is it?

It is the header appended to a segment/datagram.

![ipv4 header](./images/ipv4-header.png)

## Version

4 byte indicating the version of IP.

## Internet Header Length (IHL)

Identifies the length of the header in 4 byte increments.

Example: if value is 1010 (10) --> 10 \* 4-bytes = 40-bytes

Minimum: 5 -> 20 bytes, Maximum: 15 -> 60 bytes

## Differentiated Services Code Point (DSCP)

Length: 6 bits

It is for Quality of Service (QoS).

Used to identify which traffic should receive priority treatment.

## Explicit Congestion Notification

Length: 2 bits

Provides end-to-end encryption notification of network congestion without dropping packets.

An optional feature which requires infrastructure that supports it.

## Total Length

16 bit indicating the total lenght of the header. It has a maximum length of 65535 (2^16).

## Identification

A 16 bit field indicated which group fragmented packets belong to. Fragmented packet that belong to the same unit have the same value for this field.

Packets become fragmented if size is larger than Maximum Transmission Unit (MTU), which is 1500 bytes.

Fragments are reassembled by receiving hosts.

## Flags

3 bits

Bit 0: reserved 0
Bit 1: Don't Fragment (DF bit), it is a flag which indicates a packet should be fragmented or not
Bit 2: More Fragments (MF bit), 1 if there are more fragments in the packet, set 0 if packet is last fragmetn

## Fragment Offset

13 bit field which indicates the order of the fragmented packet. This is so packets that arrive out of order can still be reassembled to form the complete packet.

## Time To Live (TTL)

8 bit section which indicates how long the packet lives.

- A router drops packet with TTL 0, so it prevents infinite loop
- Indicates how many hops the packet goes through, with each router it visits decreases TTL by 1
- Recommended default TTL is 64

## Protocol

8 bit field which indicates the protocol of the packet.

- 6: TCP
- 17: UDP
- 1: ICMP
- 89: OSPF (dynamic routing protocol)

## Header Checksum

- 16 bit field which is used to check for errors
- When router receives packet, it calculates checksum of the header then compares it to this value
- If they do not match, the router drops the packet
- IP relies on the encapsulated protocol to detect checksum in the encapsulated data, with TCP and UDP having their own checksum fields

## Source and Destination IP Address

Both 32 bits in length.

- Source: IPv4 address of the sender of the packet
- Destination: IPv4 address of the receiver of the packet

## Options

Length is 0 - 320 bits.

- If IHL field is greater than 5, options are present
