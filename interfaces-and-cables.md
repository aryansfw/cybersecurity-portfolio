# Interfaces and Cables

Day 2 of CCNA 200-301 Course by Jeremy IT Lab

# Ethernet

## What is an ethernet?

Ethernet is a collection of network standards or protocols

## Why are standards/network protocols important?

International standards enable consistent and working communication between network devices.

## How can network devices be connected with a cable?

Cables can connect to network devices via a RJ-45 (Registered Jack) connector

## In what form is data sent through these cables?

```
 0 1 0 0 1 1 1 0 <-- byte
 ^
 |
bit
```

So a byte is a group of 8 bits.

Data transfer speed is measured in bits per second not bytes per second.

## Ethernet standards

Standards are defined in the IEEE 802.3 standard in 1983 (Institute of electrical and electronic engineers)

| Speed    | Common Name      | IEEE Standard | Informal Name | Maximum Length |
| -------- | ---------------- | ------------- | ------------- | -------------- |
| 10 Mbps  | Ethernet         | 802.3i        | 10BASE-T      | 100 m          |
| 100 Mbps | Fast Ethernet    | 802.3u        | 100BASE-T     | 100 m          |
| 1 Gbps   | Gigabit Ethernet | 802.3ab       | 1000BASE-T    | 100 m          |
| 10 Gbps  | 10 Gig Ethernet  | 802.3an       | 10GBASE-T     | 100 m          |

# UTP Cables

## What is a UTP Cable?

UTP (Unshielded Twisted Pair) is a copper cable consisting of 4 twisted wire pairs.

## Why are the pairs twisted?

Pairs are twisted to reduce electromagnetic interference (EMI)

## How do they relate with RJ-45 connectors?

Connectors have 8 pins which can be connected with the UTP cable based on the ethernet speed.

| Speed      | Pairs | Pins/Wires |
| ---------- | ----- | ---------- |
| 10BASE-T   | 2     | 4          |
| 100BASE-T  | 2     | 4          |
| 1000BASE-T | 4     | 8          |
| 10GBASE-T  | 4     | 8          |

## 10BASE-T and 1000BASE-T Connections

### Which pins are used in 10BASE-T and 1000BASE-T?

| Device Type | Transmit (Tx) Pins | Receive (Rx) Pins |
| ----------- | ------------------ | ----------------- |
| Router      | 1 and 2            | 3 and 6           |
| Firewall    | 1 and 2            | 3 and 6           |
| PC          | 1 and 2            | 3 and 6           |
| Switch      | 3 and 6            | 1 and 2           |

### Different transmit and receive pins example

Uses a **straight-through cable**, meaning same connector ends.

```
PC                     Switch
Tx 1 --------------- 1 Rx
Tx 2 --------------- 2 Rx
Rx 3 --------------- 3 Tx
   4                 4
   5                 5
Rx 6 --------------- 6 Tx
   7                 7
   8                 8
```

### Same transmit and receive pins example

Uses a **cross-over cable**, meaning different connector ends.

```
PC                     Router
Tx 1 --\ /------------ 1 Tx
Tx 2 ---X--\   /------ 2 Tx
Rx 3 --/ \--\-/------- 3 Rx
   4         X         4
   5        / \        5
Rx 6 ------/   \------ 6 Rx
   7                   7
   8                   8
```
### Sounds annoying, how to automate?

Modern devices have Auto-MDIX ports, which automatically detect and set Tx and Rx pin connections.

Using same transmit and receive pins example after using Auto-MDIX

```
PC                     Switch (Auto-NDIX)
Tx 1 --------------- 1 Rx => Tx
Tx 2 --------------- 2 Rx => Tx
Rx 3 --------------- 3 Tx => Rx
   4                 4
   5                 5
Rx 6 --------------- 6 Tx => Rx
   7                 7
   8                 8
```

## 1000BASE-T and 10GBASE-T Connections

### How do send data so fast?

Each pair is **bi-directionnal**, meaning data can be transmitted and received on the same pair.

```
PC                Switch
1 --------------- 1
2 --------------- 2
3 --------------- 3
4 --------------- 4
5 --------------- 5
6 --------------- 6
7 --------------- 7
8 --------------- 8
```