[chap-secrets]
==============

Currently *accel-ppp* may works only with one of the authentication method, chap-secrets or RADIUS. RADIUS has more priority if set in ``[modules]`` section. Reomve or *#comment* ``radius`` from section ``[modules]`` if you want use``chap-secrets``. Example:

.. code-block:: sh

    [modules]
    chap-secrets
    #radius

Configuration
-------------
