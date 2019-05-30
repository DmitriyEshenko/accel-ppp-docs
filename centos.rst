Install on Centos
-----------------

For compile with modules **vlan_mon** and **ipoe** on centos need install vanilla linux kernel or kernel from elrepo. If that not needed, just set **-DBUILD_IPOE_DRIVER=FALSE** and **-DBUILD_VLAN_MON_DRIVER=FALSE** on cmake.

**Preparation**

Before compile and build package need satisfy some dependencies

* **rpm-build** - open-source system that manages the build process
* **cmake** - open-source system that manages the build process
* **gcc** - GNU Compiler Collection (GCC) is a compiler system
* **git** - version-control system for tracking changes, (need for downloading source code) 
* **pcre-devel** - source code of pcre lib, accel-ppp need it for use reg expression
* **openssl-devel** - source code of lib ssl, accel-ppp need it for use regular expression
* **lua-devel** - this need for create custom username (IPoE) from packet. Script write on lua language 

.. code-block:: sh

  yum -y install rpm-build cmake gcc git pcre-devel openssl-devel lua-devel
