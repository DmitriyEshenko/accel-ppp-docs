Install on Centos
-----------------

For compile with modules vlan_mon and ipoe on centos need install vanilla linux kernel or kernel from elrepo. If that not needed, just set **-DBUILD_IPOE_DRIVER=FALSE** and **-DBUILD_VLAN_MON_DRIVER=FALSE** on cmake.

**Preparation**
