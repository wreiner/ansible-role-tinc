# Ansible Role: tinc

This role installs and configures tinc vpn.

## Mandatory variables

The netname block can occure multiple times. Depending on the role of the host
a few settings differ.

### Master node

```
tinc__client_settings:
  - netname: "vpn1"
    nodename: "somemaster"
    physical_address: "1.2.3.4"
    vpn_ip_address: "192.168.98.XX"
    netmask: "24"
    port: 443
    nexthop: "self"
    mode: "router"
    compression: 9
    autostart: "yes"
```

### Client node

```
tinc__client_settings:
  - netname: "vpn1"
    nodename: "netbox"
    vpn_ip_address: "192.168.98.XX"
    netmask: "24"
    port: 656
    nexthop: "vpn1server"
    mode: "router"
    compression: 9
    autostart: "no"
```

## Optional variables

If Hashicorp Vault is used it is possible to sync the hosts via Hashicorp Vault.
For this to work the Hashicorp Vault Credentials need to be provided as an approle.
To use the Vault sync set _tinc__hashivault_sync_ to _true_ and add the mountpoint of your secret via _tinc__hashivault_mountpoint_:

```
tinc__hashivault_sync: true
tinc__hashivault_mountpoint: ansible-hosts
```

## Helpers (deprecated)

The play in fetch-tinc-hosts.yml fetches all known hosts files from an existing master.
