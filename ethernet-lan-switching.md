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

Meaning the unknown unicast frame is sent through all interfaces except the source interface.

The device that has the same destined MAC address processes the frame normally. If the device wants to send a reply, a frame with switched source and destination MAC addresses gets sent to the switch through the interface. Then, the switch can register its MAC address, associating it with the interface.

The device with a different MAC address simply drops the frame.

### How long are the dynamic addresses stored in the table

If a dynamic MAC address is not used for 5 minutes, it is erased from the table.
