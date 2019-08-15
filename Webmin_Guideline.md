# Login with “root” account
# Set static IP
### Turn on ONBOOT="yes" for ifcfg-enp0s3
```sh
cd /etc/sysconfig/network-scripts/
vi ifcfg-enp0s3
```
#### Add below information to ifcfg-enp0s3
    TYPE="Ethernet"
    PROXY_METHOD="none"
    BROWSER_ONLY="no"
    BOOTPROTO="dhcp"
    DEFROUTE="yes"
    IPV4_FAILURE_FATAL="no"
    IPV6INIT="yes"
    IPV6_AUTOCONF="yes"
    IPV6_DEFROUTE="yes"
    IPV6_FAILURE_FATAL="no"
    IPV6_ADDR_GEN_MODE="stable-privacy"
    NAME="enp0s3"
    UUID="16d106ff-09ad-4f23-bc9a-47bce11162df"
    DEVICE="enp0s3"
    ONBOOT="yes"
### Turn on ONBOOT=yes for ifcfg-enp0s8
```sh
vi /etc/sysconfig/network-scripts/ifcfg-enp0s8
```
#### Add below information to ifcfg-enp0s8
    BOOTPROTO=none
    ONBOOT=yes
    IPADDR=192.168.56.141 (IP)
    PREFIX=24

### Restart network

```sh
systemctl restart network
```
# Tạo file webmin.repo tại thư mục  /etc/yum.repos.d/
```sh
vi /etc/yum.repos.d/webmin.repo
```
#### Add below information to webmin.repo
    [Webmin]
    name=Webmin Distribution Neutral 
    #baseurl=http://download.webmin.com/download/yum
    mirrorlist=http://download.webmin.com/download/yum/mirrorlist
    enabled=1

# Import PGP Key của webmin
	rpm --import http://www.webmin.com/jcameron-key.asc
# Cài đặt Webmin
```sh
yum -y update
yum install wget
# Download & install the RPM version of webmin
wget http://prdownloads.sourceforge.net/webadmin/webmin-1.831-1.noarch.rpm
yum -y install perl perl-Net-SSLeay openssl perl-IO-Tty perl-Encode-Detect
yum install webmin
```
# Tắt Firewall & Selinux
```sh
# Add port 10000 into firewall
sudo firewall-cmd --zone=public --add-port=10000/tcp –permanent
```
```sh
# Add http /https
firewall-cmd --zone=public --add-service=http
firewall-cmd --zone=public --add-service=https
```
# Turn off selinux
```sh
vi /etc/selinux/config ( Set SELINUX=disabled)
reboot
```
# Turn on firewall
```sh
systemctl restart firewalld
```	
# Turn on webmin
```sh
/etc/rc.d/init.d/webmin stop
systemctl start webmin
```
# Check admin service
Go to access link [Webmin in web https://192.168.56.141:10000](https://192.168.56.141:10000/) 