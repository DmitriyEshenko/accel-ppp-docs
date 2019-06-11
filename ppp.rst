[ppp]
======

The Point-to-Point Protocol (PPP) [1] provides a standard method for transporting multi-protocol datagrams over point-to-point links.  PPP also defines an extensible Link Control Protocol.
Section ``[ppp]`` consist common ppp prams for PPPoE/PPtP/L2TP/SSTP.

**verbose=0|1**
  Default value is ``verbose=0``

  Writes more detailed logs.

**min-mtu=n**
  Default value is ``min-mtu=100``
  
  Minimum acceptable MTU.
  If client will try to negotiate less then specified MTU then it will be NAKed or disconnected if rejects greater MTU.

**mtu=n**
  By default is not defined.
  
  MTU which will be negotiated if client's MRU will be not acceptable.
  
**mru=n**
  By default is not defined.

  Prefered MRU.

**accomp=allow|deny**
  By default is: ``accomp=deny``

  Address/Control compression negotiation.
  
  * ``allow`` - prefere in send and don't deny in receive directions.
  
  * ``deny`` - disable in both directions.

**pcomp=allow|deny|n**
  By default is: ``pcomp=deny``

  Protocol field compression negotiation. 

  * allow - prefere in send and don't deny in receive directions.

  * deny - disable in both directions.

**ccp=n**
  By default is enabled: ``ccp=1``

  For disable CCP(*Compression Control Protocol*) negotiation set ``ccp=0``

**ccp-max-configure=n**
  By default is: ``ccp-max-configure=3``
  
  **TODO**
  
**sid-case=upper|lower**
  By default is: ``sid-case=lower``

  Specifies in which case generate session identifier.
  
**check-ip=0|1**
  By default is: ``check-ip=0``

  Specifies whether accel-ppp should check if IP already assigned to other ppp interface.
  
**single-session=replace|deny**
  By default is not defined.

  Specifies whether accel-ppp should control sessions count. If this option is absent session count control is turned off. If this option is ``replace`` then accel-ppp will terminate first session when second is authorized. If this option is ``deny`` then accel-ppp will deny second session authorization.
