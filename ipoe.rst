.. _ipoe:

IPoE
----
Methot authenication users, control sessions and dilivery without any tunnel "called" as IPoE (IP over Ethernet).
Accel-ppp support L2 and L3 topologies and start sessions on DHCP Discover or unclacified packet.

Develop auxiliary kernel module for sessions start on unclacified packet and shared interfaces.
This module creates virtual interface, an analogue of ifb and used for sessions shaper and One-to-one NAT.

The difference between L2 and L3
L2 incoming packet will be checked for the mac address set at the session start, and outgoing packets will be sent straight to this mac address without additional ARP requests, which provides protection against IP/mac address spoofing.
In the case of L3, the outgoing packet will be routed according to the established routing rules.

IPoE configuration overview
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Section IPoE contain many flexible customization.

**[ipoe]**

**verbose=0|1**
    Writes more detailed logs (default=0)
    
**session-timeout=n**
    Define max sessions time in seconds. After this time session will be terminated. May redefine with radius attribute **Session-Timeout**
    
**shared=0|1**
    Specifies where interface is shared by multiple users (active by default=1). If used vlan-per-user need turn this to 0. Also may be define per-interface.
    
**unit-cache=n**
    Specifies number of interfaces to keep in cache. It means that don't destory interface after corresponding session is destoyed, instead place it to cache and use it later for new sessions repeatedly. Actial only if used shared interfaces.
    
**vlan-mon=[re:]name[,filter]**
    vlan-mon needs for automatiicaly crate vlans interfaces, more often on vlan-per-user schemas. Support regular expression (**re:**). Parameter specifies list of vlans or ranges of vlans to monitor for and may be in following form: vlan-mon=eth1,2,5,10,20-30
    
**vlan-timeout=n**
    Specifies time of vlan inactivity before it will be removed (seconds). By default is 60 seconds.
    
**vlan-name=pattern**
    By default **vlan-name=%I.%N**.
    
    Specifies pattern of vlan interface name. Pattern may contain following macros:
    
        %I: - name of patern interface.
        
        %N: - number of vlan.
        
        %P: - number of vlan of parent interface.
        
    Works with params interface and required regular expression.
  
**noauth=n**
    By default 0.
    
    Allows users to connect without authentication by radius or chap-secrets.For correct work it is necessary to use with ip-pool.

**ifcfg=0|1**
    By default active **ifcfg=1**.
    parameter specifies whether accel-ppp should add router IP address and route to client to interface or it is explicitly configured. 

 **proto=n**
    By default 3 - boot.
    
    Specifies number of protocol to be used for inserted routes. Works only with **ifcg=0**, when the routes create an accel-ppp, not a kernel. Also need exist gw ip address in the system on any of the interfaces, otherwise an error will be output to the accel-ppp.log
        debug: libnetlink: RTNETLINK answers: Invalid argument

 **check-mac-change=0|1**
