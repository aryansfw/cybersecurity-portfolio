# Cisco ISO CLI

Day 4 of CCNA 200-301 course by Jeremy IT Lab

## How do connect to CLI?

- On a cisco switch there is a usb mini B or RJ45 connector with a label "console"
- We connect using a rollover cable:
  ![rollover cable pins](./images/rollover-cable-pins.png)
- On our computer, we can connect using [puTTy](https://www.putty.org) with a "Serial" connection type

## CLI Modes

### User EXEC Mode

#### How to access?

- Default mode
- Use `exit` during privileged exec mode

#### How do we identify this mode?

Identified with a '>' sign after hostname, ex. `Router>`.

#### What can we do?

This mode is only for viewing, and we cannot make any configuration changes.

### Privileged EXEC Mode

#### How to enable this mode?

- Use `enable` during user exec mode
- Use `exit` during global configuration mode
- Use command `do` during global configuration mode without changing modes

#### How we identify?

Identified with '#' sign after hostname, ex. `Router#`

#### What can we do?

This mode provides complete access to view the device's configuration and system functions, but still unable to change configurations

### Global Configuration Mode

#### How to access

With `configure terminal` or `conf t` during privileged exec mode

#### How we identify?

When there is '(config)' after hostname, ex. `Router(config)`

#### What can we do

We can set the password using `enable password` which will be used when turning on privileged exec mode

## Configuration Files

### What is running-config?

The current active config file on the device, commands update this config

### What is startup-config

Configuration file that loads when restarting the device

### Saving config on to startup-config

The current running-config will be copied on to startup-config through these commands:

```
Router#write

Router#write memory

Router#copy running-config startup-config
```

## Passwords and Encryption

### How to set password?

`enable password`, default will be unencrypted

### How to set secret?

`enable secret`, uses MD5. Secret will automatically be used as password

### Encrypt password using cisco's encryption

`service password-encryption`

### How to cancel using encryption?

`no`

Rules:

1. Enabling `service password-encryption`:

- Current passwords will be encrypted.
- Future passwords will be encrypted.
- The `enable secret` will not be affected.

2. If you disable `service password-encryption`:

- Current passwords will not be decrypted.
- Future passwords will not be encrypted.
- The `enable secret` will not be affected.
