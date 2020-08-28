# Fine-Grained-Access-Control-on-fwknop
This is an enhanced version of the software fwknop. It was my bachelor's final project. I have put the whole instruction for setting up fwknop, however, this is an implementation of fine-grained access control on fwknop. 
The complete story of fwknop can be found at https://www.cipherdyne.org/fwknop/. 
"fwknop stands for the "FireWall KNock OPerator", and implements an authorization scheme called Single Packet Authorization (SPA). This method of authorization is based around a default-drop packet filter (fwknop supports iptables and firewalld on Linux, ipfw on FreeBSD and Mac OS X, and PF on OpenBSD) and libpcap. SPA is essentially next generation port knocking (more on this below). The design decisions that guide the development of fwknop can be found in the blog post "Single Packet"

Fine-grained access in this project is done on elements, namely, **start and end time of connection, IP range of client, start and end date, week days at which the client is allowed to make connection, and operating system.**

To set up, clone the project and follow the instructions below. But first, I have demonstrated some screenshots of how the project works. 


