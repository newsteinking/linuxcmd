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


* Python Devel Tools
yum install python-pip python-devel

yum install openssl


/docker-registry-demo/registry/docker-registry/
python setuup.py install


Install via pip:

$ pip install boto

Install from source:

$ git clone git://github.com/boto/boto.git
$ cd boto
$ python setup.py install

pip install boto


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

* local repository push
docker push xx.xx.xx.xx:5000/centos

* local repository search

::

    docker search localhost:5000/centos
    docker search 10.3.0.77:5000/centos



.

2.1.4 Docker bash alias
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#Docker
#Remove non-tagged images
function docker-rmi-none() {
    docker rmi $(docker images | grep none | awk '{print $3}');
}

#Remove all containers
function docker-rm-all() {
    docker rm $(docker ps -aq)
}

#Docker run image ($1) with default (bash) or specific command
function dr() {
    cmd="bash"

    [ $# -eq 2 ] && cmd=$2
    echo "docker run -it --rm $1 $cmd"
    docker run --name tmp$(( $(docker ps | wc -l) - 1))  -it --rm $1 $cmd
}

#Load saved Docker image (from full path or default dir)
function dl() {
    local path=$1
    [[ "${path}" =~ ^.*/.*$ ]] || path="${HOME}/devel/brew/"${path}

    docker load -i ${path}
}

#Docker exec $cmd (defaul: bash) in $container (default: first container in docker ps)
function de() {
    local cmd=bash
    local container=$1
    [ -z "$1" ] && container=$(docker ps | tail -1 | awk '{print $1}')
    [ "$container" == "CONTAINER" ] && >&2 echo "No running container" && return 0
    [ $# -ge 2 ] && shift && cmd=$@
    docker exec -it $container $cmd
}

#Get IP of $container (default: first container in docker ps)
function di() {
    local container=$1
    [ -z "$1" ] && container=$(docker ps | tail -1 | awk '{print $1}')
    [ "$container" == "CONTAINER" ] && >&2 echo "No running container" && return 0
    docker inspect $container | jq -r .[0].NetworkSettings.IPAddress
}
*(none) 이미지만 지우기
docker rmi $(docker images -f dangling=true | awk '{ print $3 }' | grep -v IMAGE)

*컨테이너 한번에 지우기

$ sudo docker rm $(docker ps -a -q)

*이미지 한번에 지우기

$ sudo docker rmi -f $(docker images -q)




2.1.5 gunicorn error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

yum erase python-pip

yum install xz-libs

# Let's download the installation file using wget:
wget --no-check-certificate https://pypi.python.org/packages/source/s/setuptools/setuptools-1.4.2.tar.gz

# Extract the files from the archive:
tar -xvf setuptools-1.4.2.tar.gz

# Enter the extracted directory:
cd setuptools-1.4.2

# Install setuptools using the Python we've installed (2.7.6)
python2.7 setup.py install

wget https://pypi.python.org/packages/source/p/pip/pip-1.2.1.tar.gz

@annmoon-linux ~]# tar xvfz pip-1.2.1.tar.gz
[root@annmoon-linux ~]# cd pip-1.2.1
[root@annmoon-linux ~]# python setup.py install

*install gunicorn
pip install gunicorn

2.1.6 make a private registry
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
참고 :https://blog.codecentric.de/en/2014/02/docker-registry-run-private-docker-image-repository/

https://github.com/lukaspustina/docker-registry-demo

make base
make registry
make start-registry

* error
W: Failed to fetch http://archive.ubuntu.com/ubuntu/dists/trusty/InRelease

vi /etc/default/docker

DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4"

* docker remote error
::

    FATA[0002] Error: Invalid registry endpoint https://10.3.0.115:5000/v1/: Get https://10.3.0.115:5000/v1/_ping: EOF.
    If this private registry supports only HTTP or HTTPS with an unknown CA certificate,
    please add `--insecure-registry 10.3.0.115:5000` to the daemon's arguments. In the case of HTTPS,
    if you have access to the registry's CA certificate, no need for the flag; simply place the CA
    certificate at /etc/docker/certs.d/10.3.0.115:5000/ca.crt



이럴경우
모든 접속 서버에도 /etc/sysconfig/docker
아래 --insecure-registry 를 집어 넣어야 한다.


other_args=" -g /data/docker -p /var/run/docker.pid --insecure-registry 10.3.0.115:5000 "


*make registry error

/docker-registry-demo/registry/docker-registry
에서
python setup.py install

docker-registry-demo/registry/docker-registry/requirements
pip install -r main.txt


SWIG/_m2crypto.i:30: Error: Unable to find 'openssl/opensslv.h'

yum install openssl-devel



* proxy error
 requirements.insert(0, 'argparse==1.2.1')

/docker-registry-demo/registry/Dockerfile
/docker-registry-demo/registry/docker-registry/Dockerfile

모두에 proxy를 설정한다.
/Dockerfile

ENV http_proxy 'http://10.3.0.172:8080'
ENV https_proxy 'http://10.3.0.172:8080'
ENV HTTP_PROXY 'http://10.3.0.172:8080'
ENV HTTPS_PROXY 'http://10.3.0.172:8080'
RUN export http_proxy=$HTTP_PROXY
RUN export https_proxy=$HTTPS_PROXY


* pip error

::

    File "/usr/lib/python2.7/dist-packages/requests/utils.py", line 636, in except_on_missing_scheme
    raise MissingSchema('Proxy URLs must have explicit schemes.')
    MissingSchema: Proxy URLs must have explicit schemes.




* pin reinstall
[root@annmoon-linux ~]# wget https://pypi.python.org/packages/source/p/pip/pip-1.2.1.tar.gz
[root@annmoon-linux ~]# tar xvfz pip-1.2.1.tar.gz
[root@annmoon-linux ~]# cd pip-1.2.1
[root@annmoon-linux ~]# python setup.py install


pip install --proxy http://user:password@proxyserver:port TwitterApi

pip install --proxy="user:password@server:port" packagename
pip install --proxy="sean:news2816@10.3.0.172:8080"

python setup.py install



*도커 레지스트리에 푸시(Push)하기

이미지를 도커 레지스트리에 넣기 위해서는 이미지에 적당한 이름을 붙여줄 필요가 있습니다. docker tag 명령어로
이미지에 새로운 이름을 부여

::

    docker tag nacyot/hello_docker 0.0.0.0:5000/hello_docker

    docker tag centos:5 10.3.0.115:5000/centos:5
    docker tag ubuntu:latest  10.3.0.115:5000/ubuntu:latest


    docker push 10.3.0.115:5000/centos:5

    docker push 10.3.0.77:5000/centos:5

Pushing tag for rev [861c710fef70] on {http://10.3.0.115:5000/v1/repositories/centos/tags/5}

.

* remote 가져오기

docker pull 10.3.0.115:5000/registry



* docker search http proxy setting

vi /etc/sysconfig/docker
아래 라인 추가

##sean
export HTTP_PROXY=http://10.3.0.172:8080
export HTTPS_PROXY=http://10.3.0.172:8080

* dockerfile http proxy

ENV http_proxy 'http://user:password@proxy-host:proxy-port'
ENV https_proxy 'http://user:password@proxy-host:proxy-port'
ENV HTTP_PROXY 'http://user:password@proxy-host:proxy-port'
ENV HTTPS_PROXY 'http://user:password@proxy-host:proxy-port'
샘플
ENV http_proxy 'http://10.3.0.172:8080'
ENV https_proxy 'http://10.3.0.172:8080'
ENV HTTP_PROXY 'http://10.3.0.172:8080'
ENV HTTPS_PROXY 'http://10.3.0.172:8080'




* remote search

curl -X GET http://10.3.0.115:5000/v1/search?q=registry
curl -X GET http://10.3.0.115:5000/v1/search



docker search 10.3.0.115:5000/library


2.1.7 기본 인증

/etc/hosts

127.0.0.1       localhost
127.0.1.1       ubuntu
<레지스트리 서버 IP 주소>    registry.example.com


openssl genrsa -out server.key 2048

openssl req -new -key server.key -out server.csr


openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

$ sudo cp server.crt /etc/pki/ca-trust/source/anchors/
$ sudo update-ca-trust enable
$ sudo update-ca-trust extract

client에도 server.crt 를 복사하여 3가지 실행

yum install httpd-tools

...continue


2.1.2 CentOS 7.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



2.1.3 Ubuntu 14.04
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


2.1.4 CentOS 7.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2.1.5 CentOS 7.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~