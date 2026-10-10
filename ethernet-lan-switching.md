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

## MAC Address

### What is it?

A 6-byte globally unique physical address assigned to the device when it is made.

First 3 bytes: OUI (Organizationally Unique Identifier), it is assigned to the company making the device

Last 3 bytes: Unique identifier of the device
