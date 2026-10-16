# Switch Interface

Day 9 of CCNA 200-301 Course by Jeremy IT Lab

## Switch interface

### How are their state without configuration?

- Connected interfaces on a switch automatically have status and protocol 'up' when `show ip interface brief`.

- Called the `up/up state`

### How to get more information on interfaces?

Use `show interfaces status`

- Vlan: 1/trunk
- Duplex:
  - a-full: automatically negotiating a full duplex connection with the connected interface
  - auto: set automatic, but doesnt have a connection yet
- Speed:
  - a-100: automatically negotiate the highest speed with the connected device
- Type: the speeds the interfaces can operate

### How do we configure interface speed and duplex?

1. Enter interface configuration mode for the given interface, e.g. `f0/1`
2. Use `speed ?` to see available speeds and `speed <value>` to set speed
3. Use `duplex ?` to see available duplex modes and `duplex <value>` to set speed

### How do we configure multiple interfaces at once?

Use `interface range`, it can be multiple interfaces separated by commas.

Example: `interface range f0/5 - 12`, `interface range f0/5 - 6, f0/9 - 12`

### What does duplex even mean?

- Half duplex: a device **cannot** send and receive data at the same time.
- Full duplex: a device **can** send and receive data at the same time.

### Negotiate? with what? Speed/Duplex Autonegotiation

Devices advertise their capabilities to neighbor device and negotiate the best speed and duplex settings.

Best duplex settings = full

Best speed = highest speed