Ansible: WireGuard VPN Server
============================

Ansible role to set up a WireGuard VPN server.

Limitations
-----------

- Right now, the set-up is **IPv4 only**.

Role Variables
--------------

```yaml
# CIDR of the WireGuard server interface
# Multiple addresses can be comma-separated
# Default: 192.168.100.1/24
wireguard_server_address: 192.168.100.1/24

# WireGuard server UDP port
# Default: 51820
wireguard_server_port: 51820

# WireGuard server private key
wireguard_server_private_key: 0KUlRv8g...aCpGQ=

# List of peers
# Each peer must have a public key and allowed addresses
# `address` contains the comma-separated list of CIDR allowed
wireguard_server_peers:
  - address: 192.168.100.2/32
    public_key: D7m9Yw+1TD...y/ij4=
```

Example Playbook
----------------

Example of how to configure and use the role:

```yaml
- hosts: all
  become: true
  roles:
    - role: lkiesow.wireguard_server
      wireguard_server_private_key: 0KUlRv8g...aCpGQ=
      wireguard_server_peers:
        - address: 192.168.100.2/32
          public_key: D7m9Yw+1TD...y/ij4=
        - address: 192.168.100.3/32
          public_key: sffeYw+1TD...y/ij4=
```

WireGuard Keys
--------------

Generate WireGuard private/public keys by running:

```
❯ wg genkey
❯ wg pubkey
```
