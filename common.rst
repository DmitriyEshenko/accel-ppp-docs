[common]
========

Contains common params for all connection types


**single-session=replace|deny**
  By default is not defined.

  Specifies whether accel-ppp should control sessions count. If this option is absent session count control is turned off. If this option is ``replace`` then accel-ppp will terminate first session when second is authorized. If this option is ``deny`` then accel-ppp will deny second session authorization.
  
**sid-case=upper|lower**
  By default is ``sid-case=lower``

  Specifies in which case generate session identifier.

**sid-source=urandom|seq**
  By default ``sid-source=urandom``
  
  Specifies method assign session id.
  
  * ``urandom`` - assign session id by random method
  * ``seq Assign`` - assign session id by sequence method

**seq-file=path**
  By default is ``seq-file=var/lib/accel-ppp/seq``
  Path to file for sessions sequence number. Start sequence number may be set there (default /var/lib/accel-ppp/seq).

**max-sessions=n**
  By default is disabled ``max-sessions=0``
  
  Specifies maximum sessions which server may processed 
 
