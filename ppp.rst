[ppp]
======

Section [ppp] consist common ppp prams for PPPoE/PPtP/L2TP/SSTP.

**verbose=0|1**
  Default value is ``verbose=0``

  Writes more detailed logs.

**min-mtu=n**
  Default value is ``min-mtu=100``
  
  Minimum acceptable MTU.
  If client will try to negotiate less then specified MTU then it will be NAKed or disconnected if rejects greater MTU.

**mtu=n**
  
  
  MTU which will be negotiated if client's MRU will be not acceptable.
  
**mru=n**
  Prefered MRU.

**accomp=allow|deny|n**
  Address/Control compression negotiation.
  
  * ``allow`` - prefere in send and don't deny in receive directions 
  * deny - disable in both directions, default behavior

**pcomp=allow|deny|n**
  Protocol field compression negotiation. 

  * allow - prefere in send and don't deny in receive directions 

  * deny - disable in both directions, default behavior

**ccp=n**
  Disable CCP negotiation if this parameter is zero.
