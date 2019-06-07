.. _ipoe:

[ipoe]
----
Methot authenication users, control sessions and dilivery without any tunnel "called" as IPoE (IP over Ethernet).
Accel-ppp support L2 and L3 topologies and start sessions on DHCP Discover or unclacified packet.

Develop auxiliary kernel module for sessions start on unclassified packet and shared interfaces.
This module creates virtual interface, an analogue of ifb and used for sessions shaper and One-to-one NAT.

The difference between L2 and L3
L2 incoming packet will be checked for the mac address set at the session start, and outgoing packets will be sent straight to this mac address without additional ARP requests, which provides protection against IP/mac address spoofing.
In the case of L3, the outgoing packet will be routed according to the established routing rules.

IPoE configuration overview
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Section IPoE contain many flexible customization.

**[ipoe]**

**verbose=0|1**
    Default value is ``verbose=0``

    Writes more detailed logs.

**lua-file=/path/to/file.lua**
     By default not defined.
     
     Needs only if used lua functions for create username from packet header information. Often used with DHCP Option 82. Look :ref:`lua_examples` for more information.

**username=ifname|lua:function**
    By default for DHCP sessions ``username=ifname``, for sessions start by unclassified packet (``start=UP``) ``username`` is client ip address.

    If ``username=ifname`` then interface name from which packet was arrived will be used as username.


    If ``username=lua:username`` then lua function with name ``username`` will be called to construct username from dhcp packet fields.
    Also may defined per-interface.

**password=username|csid|empty|<string>**
    By default ``password=username``
    Specifies how to generate password.
    
    If ``password=username`` then password will be same as username.

    If ``password=csid`` then password will be same as Calling-Station-Id.
    
    Also you can specify fixed password in ``<string>`` or leave empty.

**session-timeout=n**
     By default is disabled: ``session-timeout=0``

    Define max sessions time in seconds. After this time session will be terminated. May redefine with radius attribute **Session-Timeout**

**idle-timeout=n**
    By default is disabled ``idle-timeout=0`` 
    
    Specifies timeout in seconds to wait for any packets from client, after this time session will terminated if client don't send any packet. Often used with ``mode=L3``.

**lease-time=n**
    By default ``lease-time=600``

    Specifies lease time in seconds to be sent to DHCP client.

**max-lease-time=n**
    By default ``max-lease-time=660``

    Specifies max lease time in seconds, after this time session will be terminated if client won't renew it.

**renew-time=n**
    By default ``renew-time`` calculate as lease-time/2.

    Specifies lease renew time (option 58) in seconds to be sent to DHCP client.

**shared=0|1**
    By default is active ``shared=1``
    
    Specifies where interface is shared by multiple users. If used vlan-per-user need turn this to 0. Also may defined per-interface.
    
**unit-cache=n**
    By default is disabled: ``unit-cache=0``

    Specifies number of interfaces to keep in cache. It means that don't destory interface after corresponding session is destoyed, instead place it to cache and use it later for new sessions repeatedly. Actial only if used shared interfaces.
    
**vlan-mon=[re:]name[,filter]**
    vlan-mon needs for automatiicaly crate vlans interfaces, more often on vlan-per-user schemas. Support regular expression (**re:**). Parameter specifies list of vlans or ranges of vlans to monitor for and may be in following form: vlan-mon=eth1,2,5,10,20-30
    
**vlan-timeout=n**
    By default: ``vlan-timeout=60``.
    Specifies time on second of vlan inactivity before it will be removed.
    
**vlan-name=pattern**
    By default ``vlan-name=%I.%N``
    
    Specifies pattern of vlan interface name. Pattern may contain following macros:
    
        ``%I`` - name of patern interface.
        
        ``%N`` - number of vlan.
        
        ``%P`` - number of vlan of parent interface.
        
    Works with params interface and required regular expression.
  
**noauth=0|1**
    By default is disabled: ``noauth=0`` and used RADIUS or chap-secrets authentication.

    Allows users to connect without authentication by radius or chap-secrets. For correct work it is necessary to use with ip-pool.

**ifcfg=0|1**
    By default is active: ``ifcfg=1``

    Parameter specifies whether accel-ppp should add router IP address and route to client to interface or it is explicitly configured. Also may defined per-interface.

**proto=n**
    By default 3 - boot.
    
    Specifies number of protocol to be used for inserted routes. Works only with ``ifcg=0``, when the routes create an accel-ppp, not a kernel. Also need exist gw ip address in the system on any of the interfaces, otherwise an error will be output to the accel-ppp.log
.. admonition:: Log output:

    debug: libnetlink: RTNETLINK answers: Invalid argument

**check-mac-change=0|1**
    By default is active: ``check-mac-change=1``
    
    Terminate session when detects change of mac address of client.

**soft-terminate=0|1**
    By default is disabled: ``soft-terminat=0``

    When terminating sessions through ``cli`` or ``Radius Disconnect-Message``, the session will not be terminated immediately, but will be marked as finished and client will continue working, but next time renew lease the session will be terminated. Session will terminate immediately when expired `max-lease-time`. For manually terminate session immediately you may use cli command ``accel-cmd terminate <session selector> hard``

.. code-block:: sh

    accel-cmd terminate if ipoe0 hard
    
**l4-redirect-table=n**
     By default is disabled: ``l4-redirect-table=0``
     
     Specifies number of table. If L4-Redirect radius attribute is received and it's value is not 0 or '0' then accel-ppp will add following rule: ip rule add from <client_ip> table

**l4-redirect-ipset=<name>**
    By default not defined.
     
     Specifies name of ipset list. If L4-Redirect radius attribute is received and it's value is not 0 or '0' then accel-ppp will add client's ip to that ipset name.

**l4-redirect-on-reject=n**
    By default is disabled: ``l4-redirect-on-reject=0``

    Specified time in seconds for creating temporary sessions if radius rejects access and  'ip rule add from ip_addr table l4-redirect-table' rule will be created.

**l4-redirect-ip-pool=<pool name>**
    By default not defined.

    Allocates ip address from specified pool name if radius rejects access. Pool must be sets in section `[ippool]`

**agent-remote-id=<identifier>**
    By default not defined.

    If accel-ppp used as DHCP relay, than to DHCP requests will inserted Option 82 with agent-remote-id and agent-circuit-id with interface name from which received client request.

**local-net=x.x.x.x/mask**
    By default not defined.
    
    Specifies networks from which packets will be treated as unclassified. Need only for ``start=UP``. You may specify multiple local-net options. For example:

.. code-block:: sh

    local-net=100.64.0.0/24
    local-net=192.168.0.0/24
    local-net=172.16.0.0/24

**attr-dhcp-client-ip=<attribute>**
    By default not defined.

    Specified radius attribute which contains ip address for asign to client. Example with existing attribute:
    
.. code-block:: sh

    attr-dhcp-client-ip=DHCP-Client-IP-Address

.. admonition:: Note:

    If set custom attribute then need add its for both (radius server and accel-ppp) dictionaries.
    
**attr-dhcp-router-ip=<attribute>**
    By default not defined.

    Specified radius attribute which contains router ip address for asign to client. Example with existing attribute:
    
.. code-block:: sh

    attr-dhcp-router-ip=DHCP-Gateway-IP-Address
    
.. admonition:: Note:

    If set custom attribute then need add its for both (radius server and accel-ppp) dictionaries.

**attr-dhcp-mask=<attribute>**
    By default not defined.

    Specified radius attribute which contains netmask (CIDR) for asign to client. Example with existing attribute:

.. code-block:: sh

    attr-dhcp-mask=DHCP-Subnet-Mask

.. admonition:: Note:

    If set custom attribute then need add its for both (radius server and accel-ppp) dictionaries.

**attr-dhcp-lease-time=<attribute>**
    By default not defined.

    Specified radius attribute which contains lease time in seconds to be sent to DHCP client. This attribute has priority and may redefine value which sets in ``lease-time`` sets globally.

**attr-dhcp-renew-time=<attribute>**
    By default not defined.
    
    Specified radius attribute which contains lease renew time (option 58) in seconds to be sent to DHCP client. This attribute has priority and may redefine value which sets in ``renew-time`` sets globally.

**gw-ip-address=x.x.x.x/mask**
    By default not defined.
    
    Specifies address to be used as server ip address if radius can assign only client address. In such case if client address is matched network and mask then specified address and mask will be used. You can specify multiple such options.
    For example:

.. code-block:: sh

    gw-ip-address=100.64.0.1/24
    gw-ip-address=192.168.0.1/24
    gw-ip-address=172.16.0.0/24

****attr-dhcp-opt82=<attribute>**
    By default not defined.

    Specifies radius attribute which will contain option 82 from DHCP packet header in binary and send to radius server.
    Example:

.. code-block:: sh

    attr-dhcp-opt82=DHCP-Option82
    
.. admonition:: Note:

    Need add custom attribute in both radius and accel-ppp dictionaries. Example:

    ``ATTRIBUTE       DHCP-Option82             245 octets``
    
    

**attr-dhcp-opt82-remote-id=<attribute>**
    By default not defined.


**attr-dhcp-opt82-circuit-id=<attribute>**
    By default not defined.
    
