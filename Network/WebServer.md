# 1. Nginx
**Khái niệm**
Là 1 webserver

Được phát triển nhằm mục đích tối uuw việc sử dụng ram nhưng phục vụ được đồng thời nhiều kết nối

* Tính năng thông thường
    * Reverse proxy với caching
    * IPv6
    * Cân bằng tải
    * FastCGI hỗ trợ với caching
    * Chuyển hướng truy cập
    * Xử lý file tĩnh, file index và auton-indexing
    * TLS/SSL với SNI
    * Hỗ trợ nhúng Perl, Lua ...
    * Hỗ trợ webSocket
    * Giới hạn kết nối đồng thời từ 1 IP
    * Rewrite URL

**Cài đặt Nginx (trên linux-Centos)**

-# yum update

-# yum install nginx

-# systemctl enable nginx

-# systemctl start nginx

-# systemctl stop nginx

-# systemctl restart nginx

-# systemctl status nginx: Kiểm tra trạng thái Nginx

(http://10.211.55.3)

# 2. Apache
Tên chính thức là Apache HTTP Server - đây là một phần mềm web server miễn phí có mã nguồn mở. 

Các yêu cầu được gửi tới máy chủ sử dụng dưới phương thức HTTP. Khi bạn sử dụng trình duyệt này, bạn chỉ cần nhập địa chỉ IP hoặc URL và nhấn ENTER. Sau đó, máy sẽ tiếp nhận địa chỉ IP hoặc URL mà bạn đã nhập vào. Chức năng này có được là do cài đặt trên web server.

Apache Web Server chạy trên chính phần mềm của mình chứ không phải là server vật lý. Với nhiệm vụ chủ yếu là thiết lập kết nối, liên kết giữa server và browser rồi chuyển file giữa chúng (cấu trúc hai chiều client - server). Ngoài ra, Apache  - một phần mềm đa nền tảng được hoạt động khá mượt với cả server Unix và Windows. 

**Cài đặt Apache (trên linux-Centos)**

-# yum install httpd

-# systemctl start httpd

-# chkconfig httpd