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
 
