.. _shaper:

[shaper]
========
Accel-ppp support many ways customisation rate-limit. Also limiting clients bandwidths sometimes called as QoS (Quality of Service), but QoS has more possibilities. For enable rate-liniter, we can sets ``shaper`` in section ``[modules]``.

**attr=name**
  By default: ``attr=Filter-Id``.
  
  Specifies which radius attribute contains rate information. RADIUS server can transmit ``Filter-Id=1000``, means 1000Kbit both up-stream and down-stream rate or ``Filter-Id=2000/3000``, means 2000Kbit down-stream rate and 3000Kbit up-stream rate.

**attr-up=name**
  By default is not defined.
  
  Specifies which radius attribute contains rate information for **upstream**. Often used if needs separate *upstream* and *downstream* attributes.

**attr-down=name**
  By default is not defined.

  Specifies which radius attribute contains rate information for **downstream**. Often used if needs separate *upstream* and *downstream* attributes.

**burst-factor=n**
  By default is not defined.
  
  Burst will be calculated as rate multiply burst-factor. Common ``burst-factor`` for upstream calculated as ``burst-factor*10``.

**up-burst-factor=n**
  By default is ``up-burst-factor=1``
  
  Specifies burst factor for **upstream**.

**down-burst-factor=n**
  By default is ``down-burst-factor=0.1``

  Specifies burst factor for **downstream**.

**latency=n**
  By default is ``latency=0.05``

  Specifies latency (in milliseconds) parameter of tbf qdisc. **(Need explain datails)**

**mpu=n**
  By default is ``mpu=0``

  Specifies mpu parameter of tbf qdisc and policer. **(Need explain datails)**

**r2q=n**
  By default is ``r2q=10``

  Specifies r2q parameter of root htb qdisc. **(Need explain details)**



Examples
--------

Fiter-Id
^^^^^^^^

Cisco AV-pairs
^^^^^^^^^^^^^^

Mikrotik
^^^^^^^^
