Recommendations
===============

MTU
---

If used vlan-per-user often required 802.1ad standard also called as QinQ or Q-in-Q, then need to set MTU on main interface and S-VLAN, because adding to headed one more field.
Interface which using QinQ usualy consist of <interface_name>.<S-VLAN>.<C-VLAN>.
S-VLAN (Service VLAN) is TAG which wrap C-VLAN (Customer VLAN).

As example: 

.. code-block:: sh

  MTU
             1514
               |   1514
               |   |   1500
               |   |   |
            eth0.2001.101
               |   |   |
               |   |   C-VLAN
               |   S-VLAN
               Interface
   
Set up MTU on interface eth0 and interface with S-VLAN

.. code-block:: sh

  ip link set eth0 mtu 1514
  ip link set eth0.2001 mtu 1514
 
Increase ARP cache size
-----------------------------

If accel-ppp used as DHCP BRAS important to increase ARP cache size. Edit /etc/sysctl.conf and add next:

.. code-block:: sh

  net.ipv4.neigh.default.gc_thresh1 = 4096
  net.ipv4.neigh.default.gc_thresh2 = 8192
  net.ipv4.neigh.default.gc_thresh3 = 12288
  net.ipv6.neigh.default.gc_thresh1 = 4096
  net.ipv6.neigh.default.gc_thresh2 = 8192
  net.ipv6.neigh.default.gc_thresh3 = 12288

  And apply ``sysctl -p`` or after reboot server this params will be applied
