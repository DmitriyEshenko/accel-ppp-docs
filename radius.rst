[radius]
======

**verbose=0|1**

**interim-verbose=0|1**

**dictionary=/path/to/dictionary**

**server=address,secret[,auth-port=1812][,acct-port=1813][,req-limit=0][,fail-timeout=0,max-fail=0,][,weight=1][,backup]**
  By default is not defined.

  Specifies IP address, secret, ports of RADIUS server.

**nas-ip-address=x.x.x.x**
  By dafault is not defined.

  Specifies value to send to RADIUS server in *NAS-IP-Address* attribute and to be matched in DM/CoA requests. Also DM/CoA server will bind to that address.

**nas-identifier=identifier**
  By dafault is not defined.

  Specifies value to send to RADIUS server in NAS-Identifier attribute and to be matched in DM/CoA requests.

**gw-ip-address=x.x.x.x**
  By dafault is not defined.

  Specifies address to use as local address of ppp interfaces if *Framed-IP-Address* received from RADIUS server.

**bind=x.x.x.x**

**acct-interim-interval=n**
  By dafault is not defined.

  Specifies interval in seconds to send accounting information (may be overriden by radius *Acct-Interim-Interval* attribute)

**max-try=n**
  By default is ``max-try=3``

  Specifies number of tries to send Access-Request/Accounting-Request queries.

**timeout=n**
  By default is ``timeout=3``

  Timeout in seconds to wait response from RADIUS server.

**acct-timeout=n**
  By default is ``acct-timeout=3``

  Specifies timeout in seconds of accounting interim update, if request not received after this time , session will terminated. If ``acct-timeout=0`` then session keeps active.
  
**sid_in_auth=0|1**
  By default is not defined.
  
  Specifies should *accel-ppp* generate and send ``Acct-Session-Id`` on Access-Request packet. By default ``Acct-Session-Id`` sended on Accounting-Request packet.
  
**require-nas-identification=**

**acct-delay-time=n**

**attr-tunnel-type=name**

**dae-server=x.x.x.x:port,secret**
  By default is not defined.
  
  Specifies IP address, port to bind and secret for Dynamic Authorization Extension server (DM/CoA).This *ip address* must exist on any server interface.

**default-realm=0|1**
  By default is disabed: ``default-realm=0``

CoA
^^^
