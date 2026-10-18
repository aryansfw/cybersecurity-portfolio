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
  Uses CSMA/CD to detect and avoid collisions
- Full duplex: a device **can** send and receive data at the same time.

### Negotiate? with what? Speed/Duplex Autonegotiation

Devices advertise their capabilities to neighbor device and negotiate the best speed and duplex settings.

Best duplex settings = full

Best speed = highest speed

### If autonegotiation is disabled?

Try to sense speed, if it fails the it will automatically set speed to the slowest

Duplex there are rules:

- Speed is 10 or 100 mbps -> half duplex
- Speed is > 1000 Mbps -> full duplex

### How we see interface errors?

Error counters are available through `show interfaces <interface id>`

Name of errors:
- Runts: Frames smaller than minimum frame size (64 bytes)
- Giants: Frames larger than maximum frame size (1518)
- CRC: Frames that fail CRC check
- Frame: Incorrect format
- Input errors: total various counters errors
- Output errors: frames that failed to send