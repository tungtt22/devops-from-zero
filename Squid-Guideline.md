# Introduction
* Squid Proxy is an open source caching proxy for the web. It supports many protocols such as HTTP, HTTPS, FTP and more. It improves the response time and reduces bandwidth by caching and reusing the frequently accessed web pages and files

# Installing Squid

* Before installing any packages, it is recommended to update the system and packages using the following command.
```sh
$  yum -y update
```
### Install epel-release package
```sh
$  yum -y install epel-release
```
### Install Squid
```sh
$  yum -y install squid
```
### Once you install Squid, you can start the program immediately using the following command
```sh
$  systemctl start squid
```

### To automatically start Squid at boot time you can run the following command.
```sh
$  systemctl enable squid
```
### To view the status of Squid service, run the following command.
```sh
$  systemctl status squid
```
## Add port 3128 and restart Firewall
```sh
$  firewall-cmd --zone=public --add-port=3128/tcp --permanent
$  firewall-cmd --permanent --zone=public --add-service=squid
$  systemctl restart firewalld
$  firewall-cmd --reload
```
# Common Command
## Check version 
```sh
$  squid -v
```
## You can check the error logs of Squid using the following command.
```sh
$  tail -f /var/log/squid/access.log
```
## Verify if the squid proxy processes are started.
```sh
$  ps -ef | grep squid
```
## You can also verify if the squid proxy is listening on the port 3128.
```sh
$  ss -nlp | grep squid | grep 3128
```
# Configuring Squid
* Squid can be easily configured by editing the global configuration file /etc/squid/squid.conf
* Can edit configuration file with vi command
```sh
$  vi /etc/squid/squid.conf
```
![Configuration File](/images/squid-conf.PNG "Squid Configuration File")

## Allow Websites

## Blocking Websites
  
