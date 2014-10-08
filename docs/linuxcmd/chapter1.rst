linux command
===================================

   유용한 linux command 모음





1. Directory Size
------------------------

  디렉토리 사이즈를 보여준다.

::

    $ du -hs  [directory name]




2. Set crashkernel in grub.conf
--------------------------------

일단 패키지가 인스톨된후 /boot/grub/grub.conf 파일을 수정한다.

::

    $crashkernel=auto  nmi_watchdog=1


만약 메모리가 2G보다 작으면
    crashkernel=128M nmi_watchdog=1

만약 메로리가 2G보다 크다면
    crashkernel=auto  nmi_watchdog=1




