[![YANG via sysrepo](https://img.shields.io/badge/YANG-via_sysrepo-blue.svg)](yang/sysrepo-dnsmasq%402016-01-22.yang)
# dnsmasq-sysrepo - NETCONF enabled fork of dnsmasq

Fork of dnsmasq that uses sysrepo to store its configuration, which makes it remotely manageble via NETCONF.

The purpose of this project is to demonstrate how [sysrepo](https://github.com/sysrepo/sysrepo/blob/master/INSTALL.md) & [Netopeer 2](https://github.com/CESNET/Netopeer2) can be used to make an existing Linux application remotely manageable via NECTONF in a few hours. 

## Integration
Only following features of dnsmasq have been integrated with sysrepo so far:
* username & groupname dnsmasq will run as,
* dns-server: enabling/disabling the server, configuring the port that DNS serevr is bound to,
* dhcp-server: enabling/disabling the server, configuring list of DHCP pools and their lease-time.

See the [YANG model](yang/sysrepo-dnsmasq%402016-01-22.yang) or [full diff of the integration](https://github.com/sysrepo/dnsmasq-sysrepo/compare/a92c41eda58624056242f0c3a71c1efb7bba91b5...master) for more  information.

## Demo
Asciinema-recored demo of this integration is available here: http://www.sysrepo.org/dnsmasq-demo

## Installation
To use this integration, follow hese steps:

1) [Install sysrepo](https://github.com/sysrepo/sysrepo/blob/master/INSTALL.md).

2) Build & install dnsmasq (`make && make install`).

3) Initialize dnsmasq YANG model in sysrepo:
```
sysrepoctl --init --module=sysrepo-dnsmasq
```

4) Import initial dnsmasq configuration into startup datastore:
```
sysrepocfg --import=yang/dnsmasq.xml --datastore=startup sysrepo-dnsmasq
```

Note: Due to the limitiations of this integration, dnsmasq needs to be always running under root priviledges. The settings related to this are already part of the intial configuration imported in step 4).
