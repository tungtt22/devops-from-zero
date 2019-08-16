# NETWORK LAYERS
## 1. OSI with 7 layers
* Physical
* Data Link
* Network
* Transport
* Session
* Presentation
* Application
  
## 2. DoD with 4 layers
* Based on OSI model
* The DoD (or tcp/ip) model has 4 layers
* Network access (combine layer1 & layer2)
* internet 
* host-to-host (tcp/udp/gateway)
* application
  
| OSI Model     |     DoD Model   |               protocol          |   devices/apps  |
| -----------   |     ----------- |    -----------------------------|   -----------   |
| layer 5.6,7 | application | dns, dhcp, ntp, snmp, https, ftp, ssh, telnet, http, pop3..other   | web server, mail server, browser, mail client...|
| layer 4     | host-to-host| tcp, udp| gateway| 
| layer 3     | internet | ip, icmp, igmp    |router, firewall layer 3 switch| 
| layer 2     | network access|arp (mac), rarp | browser, mail client...| bridge, layer 2 switch |
| layer 1 | network access|ethernet, token ring | hub |

# TYPE OF CAST IN NETWORKING
## unicast
* A *unicast* communication orginates from one computer and is destined for exactly one other computer ( or host)
  
![unicast model](/images/unicast.jpg "unicast")  

## multicast
* A *multicast* is destined for a group (of computers)

![multicast model](/images/multicast.jpg "multicast") 

## broadcast
* A *broadcast* is meant for everyone
  
![broadcast model](/images/broadcast.jpg "broadcast") 

* **layer 2 broadcast** is received by all networking cards on the same segments
* **layer 3 broadcast** is received by all hosts in same ip subnet

## anycast
* The *root name servers*  of the internet use **anycast**. Any **anycast** signal goes the (geographically) nearest of a well defined group.
![anycast model](/images/anycast.jpg "anycast") 

# TYPE OF NETWORK
## Local area network (LAN)
* A LAN is local network
* LAN can contain multiple smaller LAN's
* This can be one room, or one floor, or even one big buidling

![LAN](/images/lan.jpg "LAN")

## MAN ( Metropolitan Area Network)
* Inbetween a LAN and a WAN
* A man can use fddi or ethernet or other protocols for connectivity

## WAN ( Wide Area Network)
* A network with a lot of distance the computers ( for hosts)
* A wan does not use ethernet, but protocols like fddi, frame relay, ATM or X.25
* WAN is also used for large surface area network like the internet

![WAN](/images/wan.jpg "WAN")

## PAN ( Personal Area Network) - WPAN (Wireless Personal Area Network)
* Your home network is called a pan. A wireless pan is a wpan

# Internet - Intranet - Extranet

## internet 
* The internet is a global network

## intranet
* An intranet is a private tcp/ip network
* An intranet uses the same protocols as the internet, but is only accessible to people with one organization
## extranet
* An extranet is similar to an intranet, but some trust organization (partners/clients/ suppliers..)

# INTERFACE CONFIGURATION






# SSH CLINET & SERVER
* The secure shell or ssh is a collection of tools using a secure protocol for communications with remote Linux computers
# About ssh
## 1. Secure shell
* Avoid using **telnet**, **rlogin** and **rsh** to remotely connect to your servers.(These old protocol do not encrypt the login session)
* The ssh protocol is secure in two ways. Firstly the connection is **encrypted** and secondly the connection is **authenticated** both ways
* An ssh connection always start with a cryptographic handshake, followed by **encryption** of the transport layer using a symmetric cypher. In other words, the tunnel is encrypted before you start typing anything
* Then **authentication** takes place (using user id/password or public/private key) and communication can begin over the encrypted connection
* The ssh **protocol** will remember the server it connected to (and warn you in case somethig suspicious happened)
* The **openssh** package is maintained by the **OpenBSD** people and is distributed with a lot of operating system

## 2. /etc/ssh
* Configuraion of ssh client and server is done in the **/etc/ssh/** directory
## 3. ssh protocol versions
* The ssh protocol has two version ( 1 and 2). Avoid using version 1 anywhere, since it contains some know vulnerabilities
* You can control the protocol version via /etv/ssh/ssh_config for the client side and /etc/ssh/sshd_config for the openssh-server daemon

## 4. public and priavte keys
* The ssh protocol uses the well know system of **public and private keys**. The below explanation is succunct, more information can be found on wikipedia.
[https://en.wikipedia.org/wiki/Public-key_cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) 
 
## 5. rsa and dsa algorithms 
* https://en.wikipedia.org/wiki/RSA_(cryptosystem)
* https://en.wikipedia.org/wiki/Digital_Signature_Algorithm