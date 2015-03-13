chapter 3 Docker2
===================================

   유용한 linux command 모음



3.1 Basic
------------------------

3.1.1 Directory Size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  디렉토리 사이즈를 보여준다.

::

    $ du -hs  [directory name]


3.1.2 manual core dump
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    $echo c > /proc/sysrq-trigger   or ALT+SysRq+C

core dump 생성되는곳
/var/crash/xxx/vmcore


3.1.3 grub
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

커널 부팅 순서 변경하기

::

    $vi /boot/grub/grub.conf



