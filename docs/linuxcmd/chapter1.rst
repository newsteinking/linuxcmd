linux command
===================================

   유용한 linux command 모음



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



1.4 crash 사용법
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    sys - 시스템의 일반적인 정보를 출력해 준다.
    bt - Backtrace 명령. 스택의 내용들을 순차적으로 출력해준다.
    ps - Process list 출력.
    free - Memory 및 스왑 상태 출력.
    mount - 마운트 상태 출력
    irq - 각 장치의 ( irq ) 상태를 출력.
    kmem - 메모리 상태 출력 ( kmalloc, valloc 등 메모리 할당 상태도 보여줌 )
    log - dmesg 의 내용을 출력.
    mod - 로딩된 모듈 리스트 출력.
    net - Network 상태 출력.
    runq - 실행중인 task 리스트 출력.
    task - 작업목록 출력.
    rd - 메모리 번지수에 대한 상세정보 출력.
    foreach - 모든 task, process 등 디버깅 정보에 대한 상세한 출력이 가능함.
    set - 설정된 주소 및 PID 등을 기본 컨텍스트로 설정.
    struct - 구조화된 메모리 내부의 변수들을 출력해 준다.
    files - task 가 열고있는 파일디스크립터들을 출력해준다.


1.5 Directory Size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



1.6 Directory Size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



1.7 Directory Size
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



2.3  CentOS Desktop & X windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

서버용 CentOS에 Desktop 과 X window 시스템을 인스톨 한다.

::

    $yum -groupinstall "Desktop" "Desktop Platform" "X window system" "Fonts"


2.4  CentOS Development
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CentOS 기본 개발 빌드 환경 인스톨이다.

::

    $yum install gcc
    $yum groupinstall "Development Tools"
    $yum install ncurses-devel
    $yum install libncurses5-dev
    $yum install python-dev

