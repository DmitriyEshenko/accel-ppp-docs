Configuration
=============

Accel-pppd reads options from configuration file, it usually located at ``/etc/accel-ppp.conf`` but may be redefine daemon  input arguments ``accel-pppd -c /path/to/accel-ppp.conf``

Configuration file consists of sections in form:

.. code-block:: sh

       [section1]
              name1=val1
              name2=val2
              name3

       [section2]
               ....


.. toctree::
    :maxdepth: 2
    :caption: Contents:
    :includehidden:
    
    modules.rst
    core.rst
    radius.rst
    ppp.rst
    pppoe.rst
    pptp.rst
    l2tp.rst
    ipoe.rst
    sstp.rst
    shaper.rst
