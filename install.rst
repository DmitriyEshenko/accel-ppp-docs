Install
=======

.. toctree::
    :maxdepth: 2
    :caption: Contents:
    :includehidden:
    
    ansible.rst
    debian.rst
    centos.rst

Install on Debian
-----------------
Preparation
^^^^^^^^^^^

Before compile and build package need satisfy some dependencies
* cmake - open-source system that manages the build process

* gcc - GNU Compiler Collection (GCC) is a compiler system

* linux-headers-`uname -r` - source code of current installing linux kernel, need for build ipoe and vlan_mon modules. If you don`t need these modules, you may don`t install this 
* git - version-control system for tracking changes, (need for downloading source code) 
* libpcre3-dev - source code of pcre lib, accel-ppp need it for use reg expression
* libssl-dev - source code of pcre lib, accel-ppp need it for use regular expression
* liblua5.1-0-dev - this need for create custom username (IPoE) from packet. Script write on lua language 

.. code-block:: sh

  apt-get install -y build-essential cmake gcc linux-headers-`uname -r` git libpcre3-dev libssl-dev liblua5.1-0-dev

