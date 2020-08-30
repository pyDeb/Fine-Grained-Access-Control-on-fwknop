# Setup-fwknop
Fine-grained access control was my bachelor's final project. Unfortuantelty, I have lost the controller's source code. So, I decided to share a reliable and tested approach for setting up fwknop.
The complete story of fwknop can be found at https://www.cipherdyne.org/fwknop/. 
"fwknop stands for the "FireWall KNock OPerator", and implements an authorization scheme called Single Packet Authorization (SPA). This method of authorization is based around a default-drop packet filter (fwknop supports iptables and firewalld on Linux, ipfw on FreeBSD and Mac OS X, and PF on OpenBSD) and libpcap. SPA is essentially next generation port knocking (more on this below). The design decisions that guide the development of fwknop can be found in the blog post "Single Packet"

Fine-grained access in my project was done on elements, namely, **start and end time of connection, IP range of client, start and end date, week days at which the client is allowed to make connection, and operating system.**

To set up, clone the project and follow the instructions below. 

[root@sdp-controller:~]# apt update –y  
[root@sdp-controller:~]# apt install git mariadb-server nano screen –y  
[root@sdp-controller:~]# curl –sL https://rpm.nodesource.com/setup_9.x | bash -  
[root@sdp-controller:~]# apt –y install nodejs  
[root@sdp-controller:~]# git clone https://github.com/greenstatic/SDPcontroller.git  
[root@sdp-controller:~]# cd SDPcontroller/  
[root@sdp-controller:~]# npm install  
[root@sdp-controller:~]# systemctl enable mariadb
[root@sdp-controller:~]# sudo systemctl start mariadb

[root@sdp-controller:~]# sudo mysql –u root < ./setup/sdp.sql

[root@sdp-gateway:~]# yum update -y
[root@sdp-gateway:~]# yum groupinstall "Development Tools"
[root@sdp-gateway:~]# yum install -y openssl texinfo libtool autoconf git openssl-devel json-c json-c-devel libpcap libpcap-devel iptables-services screen nano
[root@sdp-gateway:~]# echo 1 > /proc/sys/net/ipv4/ip_forward
[root@sdp-gateway:~]# systemctl enable iptables
[root@sdp-gateway:~]# systemctl start iptables
[root@sdp-gateway:~]# git clone https://github.com/waverleylabs/fwknop
[root@sdp-gateway:~]# cd fwknop/
[root@sdp-gateway fwknop]# libtoolize --force
[root@sdp-gateway fwknop]# aclocal
[root@sdp-gateway fwknop]# autoheader
[root@sdp-gateway fwknop]# automake --force-missing --add-missing

[root@sdp-gateway fwknop]# autoconf
[root@sdp-gateway fwknop]#./configure --prefix=/usr --sysconfdir=/etc --disable-client --with-iptables=/sbin/iptables
[root@sdp-gateway fwknop]# make
[root@sdp-gateway fwknop]# sudo make install


root@osboxes: sudo apt-get install openssl libssl-dev libjson0 libjson0-dev libpcap-dev texinfo libtool autoconf git curl
root@osboxes: git clone https://github.com/waverleylabs/fwknop
root@osboxes: cd fwknop/
root@osboxes:/home/jessie/fwknop# libtoolize --force
root@osboxes:/home/jessie/fwknop# aclocal
root@osboxes:/home/jessie/fwknop# autoheader
root@osboxes:/home/jessie/fwknop# automake --force-missing --add-missing
root@osboxes:/home/jessie/fwknop# autoconf
root@osboxes:/home/jessie/fwknop# ./configure --prefix=/usr --sysconfdir=/etc --disable-server
root@osboxes:/home/jessie/fwknop# make
root@osboxes:/home/jessie/fwknop# sudo make install


[root@sdp-gateway:~]# cd /etc/pki/tls/
[root@sdp-gateway:~]# openssl genrsa -des3 -out rootCA.key 4096
[root@sdp-gateway:~]# openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.crt

[root@sdp-gateway:~]# openssl genrsa -out gateway.key 2048

[root@sdp-gateway:~]# openssl req -new -key gateway.key -out gateway.csr
[root@sdp-controller:~]# openssl genrsa -out controller.key 2048
[root@sdp-controller:~]# openssl req -new -key controller.key -out controller.csr

root@osboxes:/etc/pki/tls# openssl genrsa -out sadeghi.key 2048
root@osboxes:/etc/pki/tls# openssl req -new -key sadeghi.key -out sadeghi.csr
[root@sdp-gateway tls]# openssl x509 -req -in gateway.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out gateway.crt -days 500 -sha256

[root@sdp-controller:~]# openssl x509 -req -in controller.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out controller.crt -days 500 -sha256
root@osboxes:/etc/pki/tls# openssl x509 -req -in sadeghi.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out sadeghi.crt -days 500 -sha256

