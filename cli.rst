.. _cli_configuration:

[cli]
=====

Configuration overview of the command line interface.

**verbose=1|2**
  By default ``verbose=1``

  If ``verbose=1`` then cli module will log IP address of each connection. 
  
  If ``verbose=2`` then cli module will also log passed commands.

**tcp=host:port**
  By default is not defined.
  
  Defines on which IP address and port the TCP module will listen for incoming connections. When host is empty, the TCP module listens on all local interfaces. It isn't loaded if this option isn't defined.

**telnet=host:port**
  By default is not defined.

  Defines on which IP address and port the Telnet module will listen for incoming connections. When host is empty, the Telnet module listens on all local interfaces. It isn't loaded if this option isn't defined.

**password=passwd**
  By default is not defined.

  Defines the password to be used by the TCP and Telnet modules for authenticating clients. No authentication is performed if this option isn't defined.
  
**prompt=prompt**
  By default ``prompt=accel-ppp``

  Defines the prompt string used by the Telnet module.

**history-file=filename**
  By default ``history-file=/var/lib/accel-ppp/history``

  Defines the file used by the Telnet module for loading and storing its command history.

**sessions-columns=column_list**
  By default ``sessions-columns=ifname,username,calling-sid,ip,rate-limit,type,comp,state,uptime``

  Defines the default set of columns to be displayed by the ``show sessions`` command. Invalid column names are silently discarded. All possible params:
  
  * ifname
  * username
  * calling-sid
  * called-sid
  * sid 
  * ip 
  * ip6
  * ip6-dp
  * rate-limit
  * type
  * comp
  * state
  * uptime
  * uptime-raw
  * rx-bytes
  * tx-bytes
  * rx-bytes-raw
  * tx-bytes-raw
  * rx-pkts
  * tx-pkts
  * netns
