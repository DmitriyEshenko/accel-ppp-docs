[chap-secrets]
==============

*Chap-secret* is the module of authentication which works with user authentication data and other data (username, password, ip address, speed etc.) stored as local file. Currently *accel-ppp* may works only with one of the authentication method, chap-secrets or RADIUS. RADIUS has more priority if set in ``[modules]`` section. Reomve or *#comment* ``radius`` from section ``[modules]`` if you want use ``chap-secrets``. Example:

.. code-block:: sh

    [modules]
    chap-secrets
    #radius

Configuration
-------------


Chap-secrets file example
-------------------------

.. code-block:: sh

    #client     server      secret 	    ip-address 	    speed
    user001	    *	        password1	100.64.100.1	20240/10240
    user002     *	        passowrd2	*	            10240/10240
