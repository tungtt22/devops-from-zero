# 1. DNS

**1.1 Khái niệm **

DNS (Domain Name System) Là hệ thống phân giải tên miền, cho phép thiết lập tương ứng giữa địa chỉ IP và tên miền

# 2. Squid proxy
**Khái niệm**

Squid là một proxy server, khả năng của squid là tiết kiệm băng thông (bandwidth), cải tiến việc bảo mật, tăng tốc độ truy cập web cho người sử dụng.

**Install**

$  yum -y install squid

###### Start squid

$  systemctl start squid

###### Auto start squid 

$  systemctl enable squid

###### Check status squid 

$  systemctl status squid

###### Add port 3128 and restart Firewall

$  firewall-cmd --zone=public --add-port=3128/tcp --permanent

$  firewall-cmd --permanent --zone=public --add-service=squid

$  systemctl restart firewalld

$  firewall-cmd --reload

**Common Command**

###### Check version

$  squid -v

###### Kiểm tra error log 

$  tail -f /var/log/squid/access.log

###### Chek=ck tiến trình squid

$  ps -ef | grep squid

###### Check proxy có đang listening pỏt 3128Y

$  ss -nlp | grep squid | grep 3128