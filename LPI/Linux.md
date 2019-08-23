# 1. Cấu trúc hệ điều hành
* Hệ điều hành
    * Kernel (Nhân) là phần chứa các module, thư viện để quản lý, giao tiếp với phần cứng và phần mềm
    * Shel: là một chương trình để thực thi các command 
    * Applications: các ứng dụng, tiện ích mà người dùng setup trên server
* Cấu trúc file
    * /bin: chứa các file binary của các tập lệnh
    * /sbin: tương tự như /bin, lệnh chỉ được dùng bởi admin-root
    * /boot: chứa các thư viện cần thiết trong qúa trình khởi động
    * /dev: chứa thông tin các file thiết bị
    * /etc: chứa fle cấu hình hệ thống và ứng dụng
    * /lib: chứa thư viện chia sẻ được dùng bởi các tiến trình, các lệnh boot, lệnh hệ thống
    * /lib64: tương tự /lib (dành cho 64bit)
    * /opt: dành riêng cho các tiện ích chương trình cài đặt
    * /media: là thư mục có vai trò là đích đến của mount point
    * /run
    * /root: thư mục home của user root
    * /home: thư mục chưa các thư mục home của các user được tạo ra
    * /sys
    * /srv
    * /mnt
    * /proc: lưu thông tin về tình trạng của hệ thống
* Đường dẫn:
    * tuyệt đối: bắt đầu bằng "/"
    * tương đối: không bắt đầu bằng "/"
    * đặc biệt: ".." thư mục cha, "." thư mục hiện tại
# 2. Các lệnh cơ bản
* Kiểm tra performance
    * free
    * cat /proc/cpuinfo
    * uname -a
    * cat /tec/redhat-release
    * df -h
    * ifconfig
* Quản lý file/folder
    * ls options path : liệt kê nội dung folder
    * cd path : chuyển thư mục
    * pwd: kiểm tra thư mục hiện tại
    * cp options source dest : copy file
    * mv options source dest: đổi tên/di chuyển folder/file
    * mkdir options dir : tạo folder
    * rmdir options dir : xoá folder
    * rm options file : xoá file/folder
* Hệ thống
    * shutdown options time wall
    * reboot : khởi động lại server
    * init number 
    * date
*  User/Group management
    * useradd/groupadd
    * usermod/groupmod
    * userdel/groupdel
* Permission
    * chmod
    * chown
    * chgrp
* File, search
    * vi file  
    * pipe: command 1 | command 2
    * cat 
    * cut options file
    * grep options 'string' file
    * find 
* Network
    * ifconfig
    * ping
    * telnet
    * curl
* Install software
    * gzip/tar -cvf/ tar -xvf/tar -cjf file : nén file
    * gzip -d/gunzip/tar -czf/tar -xzf/tar -xjf file : giải nén file
    * rpm -options <tênphầnmềm> cài đặt
    * yum options <tên/nhómphầnmềm>
    * ./configure –option
    * make & make install
    