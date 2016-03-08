Demo Quagga Configurations
==========================
Version: Cumulus Linux 2.5.5


Description
-----------
This Github repository contains the configuration files necessary for setting
up Layer 3 routing on a CLOS topology using Cumulus Linux and Quagga. Eight
protocols are included:

 * OSPF Numbered
 * OSPF Unnumbered
 * BGP Numbered
 * BGP Unnumbered
 * OSPF Numbered with IPv6
 * OSPF Unnumbered with IPv6
 * BGP Numbered with IPv6
 * BGP Unnumbered with IPv6

To use this repository, copy the interfaces file to `/etc/network/` and the
Quagga.conf and daemons file to `/etc/quagga/` on each device and reboot. A
helper script is provided to simplify this (this assumes you have a server
named oob-mgmt-server connected to all of your devices via eth0 that's running
apache or nginx).

    cd /var/www
    git clone https://github.com/cumulusnetworks/cldemo-config-quagga
    python pushconfig.py bgp-unnumbered server01,server02,leaf01,leaf02,spine01,spine02


Topology
--------
                     +--------------+  +--------------+
                     | spine01      |  | spine02      |
                     |              |  |              |
                     +--------------+  +--------------+
                    swp1-4 ||||                |||| swp1-4
             +---------------------------------+|||
             |             ||||+----------------+|+----------------+
             |             |||+---------------------------------+  |
          +----------------+|+----------------+  |              |  |
    swp51 |  | swp52  swp51 |  | swp52  swp51 |  | swp52  swp51 |  | swp52
    +--------------+  +--------------+  +--------------+  +--------------+
    | leaf01       |  | leaf02       |  | leaf03       |  | leaf04       |
    |              |  |              |  |              |  |              |
    +--------------+  +--------------+  +--------------+  +--------------+
      swp1 |            swp2 |            swp1 |            swp2 |
           |                 |                 |                 |
      eth1 |            eth2 |            eth1 |            eth2 |
    +--------------+  +--------------+  +--------------+  +--------------+
    | server01     |  | server02     |  | server03     |  | server04     |
    |              |  |              |  |              |  |              |
    +--------------+  +--------------+  +--------------+  +--------------+
