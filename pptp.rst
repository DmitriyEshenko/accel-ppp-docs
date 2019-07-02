[pptp]
=======

Configuration overview of PPtP module.
**verbose=0|1**
  By default is disabled.

  Specified will pptp module produce verbose logging.

**bind=x.x.x.x**

  If this option is given then pptp server will bind to specified IP address.

**port=n**

  If this option is given then pptp server will bind to specified port.

**echo-interval=n**

  If this option is given and greater then zero then pptp module will send echo-request every n seconds.

**echo-failure=n**

  Specifies maximum number of echo-requests may be sent without valid echo-reply, if exceeds connection will be terminated.

**timeout=n**

  Timeout waiting reply from client in seconds (default 5).

**mppe=deny|allow|prefer|require**

**ifname=ifname**
  By default is not defined.

  If this option is given ppp interface will be renamed using ifname as a template, ``ifname=pptp%d`` => pptp0.
  
.. admonition:: Note:
    
  Also interface may renamed if RADIUS server send attribute ``NAS-Port-Id`` with custom name. Length this value not be more 16 characters.
    
**ppp-max-mtu=n**
  By default ``ppp-max-mtu=1436``

  Set the maximun MTU value that can be negociated for PPP over PPTP sessions.
