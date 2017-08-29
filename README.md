# Ubuntu Development Environment Setup
Installation instructions for the following stack:
* [node.js] - A Lightweight Javascript Backend
* [npm] - Package Manager for JavaScript
* [git] - Source Control
* [java_8] - Java
* [docker] - Containerisation
* [docker-compose] - Container orchestration
* [gradle] - For Builds

Sections have also been added to configure their use behind a home/corporate proxy.

### Prerequisites
These instructions have been written for use with Linux Mint 18. Although I imagine they would work with equivalent other Ubuntu based distros. 

### PROXY CONFIG: apt-get
```sh
## /etc/apt/apt.conf
$ Acquire::http::proxy http://PROXY:PORT/;
$ Acquire::https::proxy "http://PROXY:PORT/";
```
### Install GIT
```sh
$ sudo apt-get install git git-gui gitk meld
```
### Install Java 8
```sh
$ sudo -E add-apt-repository ppa:webupd8team/java
$ sudo apt-get update -y
$ sudo apt-get install oracle-java8-installer oracle-java8-set-default
```
### Install Docker
```sh
$ sudo apt-get install -y -q apt-transport-https ca-certificates
$ sudo -E apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
$ sudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-xenial main'
$ sudo apt-get update && sudo apt-key update && sudo apt-get upgrade -y
$ sudo apt-get install docker-engine
$ sudo gpasswd -a ${USER} docker
$ # NOTE: Successful Install can be verified with docker --version
```
### PROXY CONFIG: Docker
```sh
$ ## /etc/systemd/system/docker.service.d/http-proxy.conf
$ [Service]
$ Environment="HTTP_PROXY=http://10.210.195.1:8080/"
$ Environment="HTTPS_PROXY=http://10.210.195.1:8080/"
$ Environment="NO_PROXY=localhost,127.0.0.0/8,10.20.2.139"
## Verify with docker info/ systemctl status docker.service && docker pull hello-world
```
### Install docker-compose
```sh
$ sudo -E curl -o /usr/local/bin/docker-compose -L https://github.com/docker/compose/releases/download/1.11.1/docker-compose-$(uname -s)-$(uname -m);
$ sudo chmod +x /usr/local/bin/docker-compose;
```
### Install Gradle
```sh
$ sudo -E wget https://services.gradle.org/distributions/gradle-3.4-bin.zip
$ sudo unzip gradle-3.4-bin.zip -d /opt
## ~/.bashrc
export GRADLE_HOME=/opt/gradle-3.4
export PATH=${GRADLE_HOME}/bin:${PATH}
```
### Install Node and NPM
```sh
$ sudo apt-get install python-software-properties
$ curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
$ sudo apt-get install nodejs
## verify with node -v && npm --version
```
### Setting a global npm proxy
```sh
## ~/.npmrc
proxy=http://PROXY:PORT
https-proxy=http://PROXY:PORT
```
### Setting a global typings proxy
```sh
## ~/.typingsrc
proxy=http://PROXY:PORT
https-proxy=http://PROXY:PORT
```

   [npm]: <https://www.npmjs.com/>
   [node.js]: <http://nodejs.org>
   [git]: <https://github.com/>
   [java_8]: <http://www.oracle.com/technetwork/java/javase/overview/java8-2100321.html>
   [docker]: <https://www.docker.com/>
   [docker-compose]: <https://docs.docker.com/compose/>
   [gradle]: <https://gradle.org/>