# tinc

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

## Helpers

The play in fetch-tinc-hosts.yml fetches all known hosts files from an existing
master.
