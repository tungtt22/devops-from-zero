# Configuration Firewall
## 1. Common Command
### Enable/Disable firewall
```sh
$  systemctl disable firewalld
$  systemctl enable firewalld
```
### Use this command to find your active zone(s):
```sh
$  firewall-cmd --get-active-zones
```
### Reload the firewall for changes to take effect
```sh
$  firewall-cmd --reload
```
### To add ports, use the following command
```sh
$  firewall-cmd --zone=public --add-port=2888/tcp --permanent
```
### To add service, use the following command
```sh
$  firewall-cmd --permanent --zone=public --add-service=http 
$  firewall-cmd --permanent --zone=public --add-service=https 
```
### To view open ports, use the following command
```sh
$  firewall-cmd --list-ports
```
### To view service ports, use the following command
```sh
$  firewall-cmd --list-services
```
### To view all information, use the following command
```sh
$  firewall-cmd --list-all
```
### To stop firewall, use the following command
```sh
$  systemctl stop firewalld
```
### To start firewall, use the following command
```sh
$  systemctl start firewalld
```
### To restart ports, use the following command
```sh
$  systemctl restart firewalld
```
### To show status, use the following command
```sh
$  systemctl status firewalld
```
## 2. IpTable Command

### install epel repo
```sh
$  yum install epel-release
```
### install iptables service
```sh
$  yum install iptables service
```
###  stop firewalld servic
```sh
$  systemctl stop firewalld
```
### disable firewalld service on startup
```sh
$  systemctl disable firewalld
```
### start iptables service
```sh
$  systemctl start iptables
```
### enable iptables on startup
```sh
$  systemctl enable iptables
```
###  Editing your iptables config at /etc/sysconfig/iptables.
```sh
$  vi /etc/sysconfig/iptables
```
Example: ports 22 and 80 open:

    >   *filter
    >   :INPUT ACCEPT [0:0]
    >   :FORWARD ACCEPT [0:0]
    >   :OUTPUT ACCEPT [214:43782]
    >   -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
    >   -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
    >   -A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
    >   -A INPUT -i lo -j ACCEPT
    >   -A INPUT -j REJECT --reject-with icmp-port-unreachable
    >   COMMIT

###  Enable & Start iptables.
```sh
$  systemctl enable iptables
$  systemctl start iptables
```
### To restart & reload firewall
```sh
$  systemctl restart firewalld
$  firewall-cmd --reload
```