# Fine-Grained-Access-Control-on-fwknop
This is an enhanced version of the software fwknop. It was my bachelor's final project. I have put the whole instruction for setting up fwknop, however, this is an implementation of fine-grained access control on fwknop. 
The complete story of fwknop can be found at https://www.cipherdyne.org/fwknop/. 
"fwknop stands for the "FireWall KNock OPerator", and implements an authorization scheme called Single Packet Authorization (SPA). This method of authorization is based around a default-drop packet filter (fwknop supports iptables and firewalld on Linux, ipfw on FreeBSD and Mac OS X, and PF on OpenBSD) and libpcap. SPA is essentially next generation port knocking (more on this below). The design decisions that guide the development of fwknop can be found in the blog post "Single Packet"

Fine-grained access in this project is done on elements, namely, **start and end time of connection, IP range of client, start and end date, week days at which the client is allowed to make connection, and operating system.**

To set up, clone the project and follow the instructions below. But first, I have demonstrated some screenshots of how the project works. 

In this picture you see that one of the gateway interfaces has been assigned two IP addresses

![An interface of two addresses on gateway](https://github.com/pyDeb/Fine-Grained-Access-Control-on-fwknop/blob/master/screenshots/1.png)


Running "ifconfig" on client side

![](https://github.com/pyDeb/Fine-Grained-Access-Control-on-fwknop/blob/master/screenshots/2.png)


Running "ifconfig" on server side

![](https://github.com/pyDeb/Fine-Grained-Access-Control-on-fwknop/blob/master/screenshots/3.png)


Server is listening on port 80

![](https://github.com/pyDeb/Fine-Grained-Access-Control-on-fwknop/blob/master/screenshots/4.png)

All ports are closed on gateway

![All ports are closed on gateway](https://github.com/pyDeb/Fine-Grained-Access-Control-on-fwknop/blob/master/screenshots/5.png)

Even client cannot recieve ping responses from the gateway

![](https://github.com/pyDeb/Fine-Grained-Access-Control-on-fwknop/blob/master/screenshots/6.png)


Port 50000 on which the gateway is connected to the controller is not accessible for the client

![](https://github.com/pyDeb/Fine-Grained-Access-Control-on-fwknop/blob/master/screenshots/7.png)




![](https://github.com/pyDeb/Fine-Grained-Access-Control-on-fwknop/blob/master/screenshots/8.png)
