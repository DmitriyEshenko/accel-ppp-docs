[log]
=====









logs rotation
^^^^^^^^^^^^^

For rotation logs can be used system logrotate utility. Needs create file ``/etc/logrotate.d/accel-ppp`` and put next:

.. code-block:: sh
 
  /var/log/accel-ppp/*.log {
    missingok
    sharedscripts
    postrotate
      test -r /var/run/accel-pppd.pid && kill -HUP `cat /var/run/accel-pppd.pid`
    endscript
  }

.. admonition:: Note:

  For correct work *logrotate* utility, need ``accel-pppd`` will run with ``-p /var/run/accel-pppd.pid`` arg.
  
.. admonition:: Warn:

  If accel-ppp run with gdb (GNU debugger) for find bugs, you need disable logs rotation, because it will makes to daemon crash.
