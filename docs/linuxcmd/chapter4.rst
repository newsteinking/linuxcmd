chapter 4 AHMS
===================================

   Asset Health Management System



4.1 Basic JAR Creation
------------------------

Eclipse - Export - select source

4.1.1 Unsupported major.minor version 52.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

J2SE 8   = Version 52

J2SE 7   = Version 51

J2SE 6.0 = Version 50

J2SE 5.0 = Version 49

JDK  1.4 = Version 48

JDK  1.3 = Version 47

JDK  1.2 = Version 46

JDK  1.1 = Version 45


::




4.1.2 manual core dump
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    $echo c > /proc/sysrq-trigger   or ALT+SysRq+C

core dump 생성되는곳
/var/crash/xxx/vmcore


4.1.3 grub
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

커널 부팅 순서 변경하기

::

    $vi /boot/grub/grub.conf



