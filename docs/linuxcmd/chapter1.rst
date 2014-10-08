linux command
===================================

   유용한 linux command 모음


0. CentOS
------------------------

0.1 Old CentOS Image & Source
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    $ http://vault.centos.org


1. Basic
------------------------

1.1 Directory Size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  디렉토리 사이즈를 보여준다.

::

    $ du -hs  [directory name]


1.2 manual core dump
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    $echo c > /proc/sysrq-trigger   or ALT+SysRq+C

core dump 생성되는곳
/var/crash/xxx/vmcore


1.3 grub
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

커널 부팅 순서 변경하기

::

    $vi /boot/grub/grub.conf







1.3 crash -linux core dump analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    $echo c > /proc/sysrq-trigger   or ALT+SysRq+C




1.3 Directory Size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



1.4 Directory Size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



1.5 Directory Size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



1.6 Directory Size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


2. Package Install
--------------------------------

2.1  kernel debug info
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

커널 디버깅 정보를 인스톨한다.

::

    $yum --enablerepo=debug install kernel-debuginfo-'uname -r'


/usr/lib/debug/lib/modules/'uname -r'/vmlinux


2.2  ELREPO  add
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

커널 디버깅 정보를 인스톨한다.


To install ELRepo for RHEL-7, SL-7 or CentOS-7:
::

    $rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm (external link)

To make use of our mirror system, please also install yum-plugin-fastestmirror.

To install ELRepo for RHEL-6, SL-6 or CentOS-6:

::

    rpm -Uvh http://www.elrepo.org/elrepo-release-6-6.el6.elrepo.noarch.rpm (external link)

To make use of our mirror system, please also install yum-plugin-fastestmirror.

To install ELRepo for RHEL-5, SL-5 or CentOS-5:

::

    rpm -Uvh http://www.elrepo.org/elrepo-release-5-5.el5.elrepo.noarch.rpm (external link)


2.1  kernel debug info
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

커널 디버깅 정보를 인스톨한다.

::

    $yum --enablerepo=debug install kernel-debuginfo-'uname -r'





/usr/lib/debug/lib/modules/'uname -r'/vmlinux
