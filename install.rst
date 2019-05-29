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

* **cmake** - open-source system that manages the build process
* **gcc** - GNU Compiler Collection (GCC) is a compiler system
* **linux-headers-`uname -r`** - source code of current installing linux kernel, need for build ipoe and vlan_mon modules. If you don`t need these modules, you may don`t install this 
* **git** - version-control system for tracking changes, (need for downloading source code) 
* **libpcre3-dev** - source code of pcre lib, accel-ppp need it for use reg expression
* **libssl-dev** - source code of pcre lib, accel-ppp need it for use regular expression
* **liblua5.1-0-dev** - this need for create custom username (IPoE) from packet. Script write on lua language 

.. code-block:: sh

  apt-get install -y build-essential cmake gcc linux-headers-`uname -r` git libpcre3-dev libssl-dev liblua5.1-0-dev

After install dependencies, download accel-ppp source code with git client, tree master . Master tree contain actual patches last release. 

.. code-block:: sh

  git clone https://github.com/xebd/accel-ppp.git accel-ppp-code

Create directory for build source code and go to this directory. 

.. code-block:: sh

  mkdir /opt/accel-ppp-code/build
  cd /opt/accel-ppp-code/build/

For building code need we can set next params:

* **-DBUILD_IPOE_DRIVER=TRUE** Include IPoE module.

This module need if you want use accel-ppp as shared interface.

* **-DBUILD_VLAN_MON_DRIVER=TRUE**

Include vlan monitoring module. If you want create vlan automatically on analyse IP headers with regular expression set on accel-ppp config file. (Available for IPoE and PPPoE)

* **-DKDIR=/usr/src/linux-headers-`uname -r`** sets path to Linux kernel source code. Need only for build IPOE, VLAN-MON.

* **-DCMAKE_INSTALL_PREFIX=/usr**
Path for install executable code. If you build DEB package, not recommended change this.
**-DCPACK_TYPE=Debian9**
This arguments for building DEB package. If used debian other version, set it. For example, if used debian 8 set **-DCPACK_TYPE=Debian8**
