modules
=======

Section [modules] containes list of modules to load

* **log_file** - logging target which logs messages to files. It support per-session/per-user features.
* **log_syslog** - logging target which logs messages to syslog.
* **log_tcp** - logging target which logs messages over TCP/IP.
* **log_pgsql** - logging target which logs messages to PostgreSQL.
* **pptp** - PPTP controlling connection handling module.
* **pppoe** - PPPoE discovery stage handling module.
* **ipoe** - DHCP and unclassified packet connection handling module.
* **l2tp** - L2TP controlling connection handling module.
* **sstp** -  SSTP controlling connection handling module.
* **auth_pap** - PAP authentication module.
* **auth_chap** - CHAP (md5) authentication module.
* **auth_mschap_v1** -Microsoft CHAP (version 1) authentication module.
* **auth_mschap_v2** - Microsoft CHAP (version 2) authentication module.
* **radius** - RADIUS interaction module.
* **chap-secrets** - module authentication from file.
* **shaper** - this module controls shaper.
* **ippool** - IPv4 address assigning module.
* **ipv6_nd** - IPv6 Neighbor Discovery module.
* **ipv6_dhcp** - IPv6 DHCP module.
* **ipv6pool** - IPv6 address assigning module.
* **sigchld** - Helper module to manage child processes, required by pppd_compat.
* **pppd_compat** - this module starts pppd compatible ip-up/ip-down scripts and ip-change to handle RADIUS CoA request.
* **connlimit** - this module limits connection rate from single source.

.. admonition:: Note:

   Can’t change with reload, for apply need daemon restart with drop active sessions.
