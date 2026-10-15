# Internet Protocol (IPv4)

## IPv4 Header

THe IPv4 header contains a lot of data, including source and destination IP Address

## IP Address

### How many bits is in an IP address?

It is 32 bits in length (8 bytes).

### What does an IP address consist of?

4 octets, meaning 8 bits.

### How is it represented?

Binary: 11000000101010000000000111111110 (32 bits)

Dotted Decimal: 192.168.1.254

Network Prefix: /24

### What is the network prefix?

The network prefix is used to identify which part of the IP address represents network or end host

/24 means first 24 bits are the network, and last 8 bits are end hosts

/16 means first 16 bits are the network, and last 16 bits are end hosts

/8 means first 8 bits are the network, and last 24 bits are end hosts

### Address Classes

| Class | First octet | First octet numeric range | Prefix Length | Note                    |
| ----- | ----------- | ------------------------- | ------------- | ----------------------- |
| A     | `0xxxxxxx`  | 0–127                     | /8            | Loopback address        |
| B     | `10xxxxxx`  | 128–191                   | /16           |                         |
| C     | `110xxxxx`  | 192–223                   | /24           |                         |
| D     | `1110xxxx`  | 224–239                   |               | Multicast address       |
| E     | `1111xxxx`  | 240–255                   |               | Reserved (experimental) |

### Netmask

Netmasks are another way of indicating prefix length because some devices do not support slash notation

| Class | Prefix Length | Netmask       |
| ----- | ------------- | ------------- |
| A     | /8            | 255.0.0.0     |
| B     | /16           | 255.255.0.0   |
| C     | /24           | 255.255.255.0 |

### How to identify a network address?

If the host portions are all 0. The network address cannot be assigned to a host

### How to identify broadcast address?

If the host portions are all 1. The broadcast address cannot be assigned to a host

### How to know maximum amount of hosts?

through the network prefix --> /8 = 24 bits worth of hosts --> 2^24 = 16,777,216

Because network and broadcast address take up two ip addresses, maximum is 2^x - 2 so that would be 16,777,214

### How to identify first and last usable address

Set last bit to 1

10.0.0.0/8

`00000000 00000000 00000000 > 00000000 00000000 00000001`

## IPv4 Addressing

### How can we see the status?

On a cisco IOS router, we can use command `show ip interface brief`

- Method = Method of setting up the interface
- Status = Layer 1 status (up/down)
- Protocol = Layer 2 status (up/down)

### How do we activate interface configuration mode?

As Global Configuration Mode: `interface gigabitethernet 0/0`, `interface g0/0`

### What can we do as interface configuration mode?

- Set IP Address: `ip address <ip> <subnet mask>`
- Enable interface: `no shutdown`, because shutdown command is ran default in a cisco router
- Set description: `description`

### How do we show information about interface?

`show interfaces <interface>`

with description: `show interfaces description`