chapter 2  Docker
===================================

   유용한 linux command 모음



2.1 CentOS 6.5 Install
------------------------
리눅스
자동 설치 스크립트

Docker는 리눅스 배포판 종류를 자동으로 인식하여 패키지를 설치해주는 스크립트를 제공합니다.

$ sudo wget -qO- https://get.docker.com/ | sh

get.docker.com 스크립트로 Docker를 설치하면 hello-world 이미지도 자동으로 설치됩니다.

hello-world 이미지는 사용하지 않을 것이므로 모두 삭제합니다.

$ sudo docker rm `sudo docker ps -aq`
$ sudo docker rmi hello-world

우분투

자동 설치 스크립트를 사용하지 않고 우분투에서 패키지로 직접 설치하는 방법입니다.

우분투 14.04 LTS 64비트를 기준으로 하겠습니다.

$ sudo apt-get update
$ sudo apt-get install docker.io
$ sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker

/usr/bin/docker.io 실행파일을 /usr/local/bin/docker로 링크해서 사용합니다.
RedHat Enterprise Linux, CentOS

자동 설치 스크립트를 사용하지 않고, 레드햇 엔터프라이즈 리눅스(RHEL)와 CentOS에서 패키지로 직접 설치하는 방법입니다. RHEL과 CentOS 패키지 저장소에는 docker-io가 없으므로 EPEL(Fedora Extra Packages For Enterprise Linux) 저장소를 사용할 수 있도록 설정합니다.

CentOS 6

$ sudo yum install http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
$ sudo yum install docker-io

AWS EC2에 설치되는 Amazon Linux(CentOS 기반)는 EPEL 저장소를 바로 사용할 수 있으므로 epel-release-6-8.noarch.rpm은 설치하지 않아도 됩니다.

CentOS 7에서는 docker 패키지를 설치하면 됩니다.

CentOS 7

$ sudo yum install docker

Docker 서비스 실행

$ sudo service docker start

부팅했을 때 자동으로 실행하기

$ sudo chkconfig docker on

Mac OS X

맥에서는 Boot2Docker를 이용하여 Docker를 사용할 수 있습니다.

https://github.com/boot2docker/osx-installer/releases13에서 Boot2Docker-1.x.x.pkg를 받은 뒤 설치합니다.

설치는 특별한 것이 없으므로 따로 설명하지 않겠습니다(내부적으로 VirtualBox가 함께 설치됩니다).

설치가 끝난 뒤에 응용 프로그램(Applications)에서 boot2docker를 실행합니다.

잠시 기다리면 자동으로 boot2docker.iso를 이용하여 가상 머신이 생성되고, 가상 머신에 접속됩니다.
윈도우

윈도우에서는 Boot2Docker를 이용하여 Docker를 사용할 수 있습니다.

https://github.com/boot2docker/windows-installer/releases51에서 docker-install.exe를 받은 뒤 설치합니다.


2.1.1 docker default directory 변경
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

예외적 조건들....

* docker default directory 변경


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

2.1.2 Kernel Upgrade 2.6->3.8
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


::

    yum install http://www.elrepo.org/elrepo-release-6-5.el6.elrepo.noarch.rpm
    yum --enablerepo=elrepo-kernel install kernel-ml


.
2.1.3 docker start error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



::

    usr/bin/docker: relocation error: /usr/bin/docker: symbol dm_task_get_info_with_deferred_remove,
    version Base not defined in file libdevmapper.so.1.02 with link time reference

.

::

    yum-config-manager --enable public_ol6_latest

    yum install device-mapper-event-libs


.
2.1.3 Build your own image from CentOS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



::

    yum install feboostrap
    febootstrap -i iputils -i vim-minimal -i iproute -i bash -i coreutils -i
    yum centos centos http://centos.mirror.iweb.ca/6.4/os/x86_64/ -u http://centos.mirror.iweb.ca/6.4/updates/x86_64/


and
::

    [root@banshee ~]# cd centos/
    [root@banshee centos]# tar -c . | docker import - centos


or ISO mount
::

    # mkdir rootfs
    # mount -o loop /path/to/iso rootfs
    # tar -C rootfs -c . | docker import - rich/mybase

using osirrox
::

    yum install xorriso
    osirrox -indev blahblah.iso -extract / /tmp/blahblah
    tar -C /tmp/blahblah -cf- . | docker import blahblah


* save docker images to tar

::

    docker save ubuntu > /tmp/ubuntu.tar


ubuntu.tar 를 풀어서 사이즈가 제일 큰 디렉토리의 layer.tar를 풀면 됨


2.1.2 CentOS 7.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



2.1.3 Ubuntu 14.04
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


2.1.4 CentOS 7.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2.1.5 CentOS 7.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~