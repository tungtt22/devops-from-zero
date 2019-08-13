# About Nginx
* Nginx is a high performance web server software. It is a much more flexible and lightweight program than Apache HTTP Server.
* Nginx pronounced engine x is a free, open-source, high-performance HTTP and reverse proxy server responsible for handling the load of some of the largest sites on the Internet
# Installing Nginx on CentOS
Follow the steps below to install Nginx on your CentOS server:
## 1. Install EPEL repository
 Nginx packages are available in the EPEL repositories. If you don’t have EPEL repository already installed you can do it by typing
 ```sh
$  sudo yum install epel-release
```
## 2. Install Nginx by typing the following yum command
 ```sh
$  sudo yum install nginx
```
If this is the first time you are installing a package from the EPEL repository, yum may prompt you to import the EPEL GPG key:

> Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
> 
> Importing GPG key 0x352C64E5:
> 
> Userid     : "Fedora EPEL (7) <epel@fedoraproject.org>"
> 
> Fingerprint: 91e9 7d7c 4a5e 96f1 7f3e 888f 6a2f aea2 352c 64e5

> Package    : epel-release-7-9.noarch (@extras)

> From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7

> Is this ok [y/N]:
**> If that’s the case, type y and hit Enter.**

## 3. Work with firewall

- If your server is protected by a firewall you need to open both HTTP (80) and HTTPS (443) ports.

- Use the following commands to open the necessary ports:
 ```sh
$  sudo firewall-cmd --permanent --zone=public --add-service=http
$  sudo firewall-cmd --permanent --zone=public --add-service=https
$  sudo firewall-cmd --zone=public --add-port=443/tcp –permanent 
$  sudo firewall-cmd --zone=public --add-port=80/tcp –permanent 
$  sudo firewall-cmd --reload
```
## 4. Enable and Start the Nginx service
```sh
$  sudo systemctl enable nginx
$  sudo systemctl start nginx
```
* Check the status of the Nginx service with the following command:
```sh
$  sudo systemctl status nginx
```
*The output should look something like this:*

* nginx.service - The nginx HTTP and reverse proxy server
    >  Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
    >  Active: active (running) since Mon 2018-03-12 16:12:48 UTC; 2s ago

    >  Process: 1677 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)

    >  Process: 1675 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)

    >  Process: 1673 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
* Main PID: 1680 (nginx)
    >  CGroup: /system.slice/nginx.service

    >          ├─1680 nginx: master process /usr/sbin/nginx    
    >          └─1681 nginx: worker process
## 5. To verify your Nginx installation, open http://YOUR_IP in your browser
![Welcome Nginx](nginx-screenshot.jpg "Welcome Nginx")

# Manage the Nginx Service with systemctl
## 1. To stop the Nginx service, run:
```sh
$  sudo systemctl stop nginx
```
## 2. To start it again, type:
```sh
$  sudo systemctl start nginx
```
## 3. To restart the Nginx service:
```sh
$  sudo systemctl restart nginx
```
## 4. Reload the Nginx service 
```sh
$  sudo systemctl reload nginx
```
## 5. Enable/ disable the Nginx service
```sh
$  sudo systemctl disable nginx
$  sudo systemctl enable  nginx
```
# Nginx Configuration File’s Structure and Best Practices
* All Nginx configuration files are located in the ***/etc/nginx/*** directory.
* The main Nginx configuration file is ***/etc/nginx/nginx.conf***
* Nginx log files (**access.log** and **error.log**) are located in the */var/log/nginx/* directory. It is recommended to have a different access and error log files for each server block.
* You can set your domain document root directory to any location you want. The most common locations for webroot include:
    >     /home/<user_name>/<site_name>
    >     /var/www/<site_name>
    >     /var/www/html/<site_name>
    >     /opt/<site_name>
    >     /usr/share/nginx/html

### Configuration with ***/etc/nginx/nginx.conf***
* Lines preceded by a # character are comments and not interpreted by NGINX
* Lines containing directives must end with a ;
### The http Block: ontains directives for handling web traffic
```sh
http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
```
### Server Blocks
```sh
server {
    listen         80 default_server;
    listen         [::]:80 default_server;
    server_name    example.com www.example.com;
    root           /var/www/example.com;
    index          index.html;
    try_files $uri /index.html;
}
```

### Listening Ports

```sh
server {
    listen 8080;
}
```
