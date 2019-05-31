.. _elrepo_kernel_inst:

Install kernel from elrepo
==========================

At first need enable ELRepo Repository. To set up ELRepo repository, you need to import its official GPG key and then install ELRepo RPM as follows.

.. code-block:: sh
  
  rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
  rpm -Uvh https://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm

Install kernel-ml and kernel-ml-devel
  
.. code-block:: sh

  yum install kernel-mlyum --enablerepo=elrepo-kernel install -y kernel-ml kernel-ml-devel

To show installed kernels run command:

.. code-block:: sh

  awk -F\' '$1=="menuentry " {print $2}' /etc/grub2.cfg
  
Snd set installed kernel as default for grub2 bootloader:

.. code-block:: sh

  grub2-set-default 0
  
Reboot system and check kernel version

.. code-block:: sh
  uname -r
  
Now you can continue install accel-ppp with modules **vlan_mon** and **ipoe**
