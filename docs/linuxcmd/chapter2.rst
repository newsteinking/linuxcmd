chapter 2  Docker
===================================

   유용한 linux command 모음



2.1 Basic Install
------------------------

2.1.1 CentOS 6.5
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


* docker default directory 변경
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In CentOS 6.5

::

    service docker stop
    mkdir /data/docker  (new directory)
    vi /etc/sysconfig/docker

add following line

::

    other_args=" -g /data/docker -p /var/run/docker.pid"

then save the file and start docker again

::

    service docker start


and will make repository file in /data/docker

* Kernel Upgrade 2.6->3.8
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    yum install http://www.elrepo.org/elrepo-release-6-5.el6.elrepo.noarch.rpm
    yum --enablerepo=elrepo-kernel install kernel-ml

* docker default directory 변경
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


* docker default directory 변경
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


* docker default directory 변경
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~












2.1.2 CentOS 7.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



2.1.3 Ubuntu 14.04
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


2.1.4 CentOS 7.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2.1.5 CentOS 7.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~