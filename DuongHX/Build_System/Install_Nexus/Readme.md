# Cài đặt (Ubuntu) :stars:

## Mục lục :book:

1. [Cài đặt java](#install-env)
2. [Cài đặt nexus](#install-nexus)
    - [Thư mục ứng dụng](#application)
    - [Thư mục dữ liệu](#data)
    - [Chạy nexus](#run-nexus)
3. [Chạy Nexus as Service](#run-as-service)
    - [Tạo một người dùng mới](#new-user)
    - [Chạy service với systemd](#systemd)

---

<a id="install-env"></a>

## Cài đặt java. :gear:

- Nexus Repository Manager yêu cầu một  Java 8 Runtime Environment(JRE).  
- Trước khi tiến hành cài đặt java cần tiến hành cập nhật các gói từ kho: ```sudo apt update```
- Tiếp đó tiến hành cài đặt java ```sudo apt install openjdk-8-jre-headless```
- Để xác nhận phiên bản java đã cài đặt chạy lệnh:
```java -version```
- Trong trường hợp không có đường dẫn cụ thể cần cập nhật cấu hình cho một phiên bản JDK hoặc JRE cụ thể. Để cài đặt một đường dẫn java cụ thể ta mở file ```bin/nexus``` trong thư mục cài đặt của nexus và thêm đường dẫn đến vị trí của java vào dòng ```INSTALL4J_JAVA_HOME_OVERRIDE```.
- Ví dụ: ```INSTALL4J_JAVA_HOME_OVERRIDE=/usr/lib/jvm/openjdk-8``` 

---

<a id="install-nexus"></a>

## Cài đặt nexus. :wrench:

- Để download Nexus truy cập vào trang [sonatype](https://help.sonatype.com/repomanager3/download)
- Chọn link download phù hợp với hệ điều hành tương ứng. Vì ở đây sử dụng ubuntu nên ta tiến hành tải Nexus về với lệnh ***wget :*** ```wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz``` trong thư mục ```opt``` (trên các máy unix thư mục ***opt*** thường được sử dụng để cài đặt các ứng dụng).
- Tiến hành giải nén với lệnh ***tar :*** ```tar -zxvf latest-unix.tar.gz``` ta được 2 thư mục đó là ***nexus-3.18.1-01*** (Do phiên bản mới nhất hiện tại là 3.18.1-01) và ***sonatype-work*** một thư mục ứng dụng và một thư mục lưu dữ liệu.

<a id="application"></a>

### Thư mục ứng dụng (thư mục cài đặt)

  - Thư mục này bao gồm ứng dụng ***Nexus Repository Management*** và các thành phần cần thiết như thư viện Java và những file cấu hình. Tên của thư mục này mặc định thường là ```nexus-{version-number}``` và nó thường được gọi là ```$install-dir``` trong bất kỳ đoạn code nào.

  - Thành phần của một thư mục cài đặt của nexus như sau:
    - ```install4j```
    - ```NOTICE.txt```
    - ```OSS-LICENSE.txt```
    - ```PRO-LICENSE.txt```
    - ```bin```
    - ```deploy```
    - ```etc```
    - ```lib```
    - ```public```
    - ```system```

- Trong đó:
  - ***OSS-LICENSE.txt, PRO-LINCENSE.txt and NOTICE.txt*** là những file mà bao gồm chi tiết pháp lý về mặt giấy phép và thông báo bản quyền.
  - ***bin*** thư mục này bao gồm những dòng lệnh liên quan đến việc chạy nexus và những file config liên quan đến việc chạy nó.
  - ***etc*** thư mục bao gồm những tệp cấu hình.
  - ***lib*** thư mục này chứa những thư viện nhị phân liên quan đến Apache karaf.
  - ***public*** thư mục này bao gồm những tài nguyên mở của nexus.
  - ***system*** thư mục bao gồm tất cả những thành phần và plugin cấu tạo nên nexus.

<a id="data"></a>

### Thư mục dữ liệu

  - Thư mục dữ liệu bao gồm tất cả các kho chứa, thành phần và các dữ liệu khác mà được lưu trữ và quản lý bởi ***repository manage***. Thông thường thư mục dữ liệu được lưu trữ ở: ```../sonatype-work/nexus3``` và nó thường được gọi là ```$data-dir``` trong bất kỳ đoạn code nào.
  - Thư mục dữ liệu bao gồm những thư mục con mà bao gồm những thành phần, kho chứa, cấu hình và các dữ liệu khác.
  - Những thư mục con bao gồm:
    - ```Blobs``` : Là thư mục mẹ của tất cả các hệ thống tệp dựa trên blob stores cái mà không được định nghĩa với đường dẫn tuyệt đối.
    Ví dụ, mặc định blob store thường ở trong ```../sonatype-work/nexus3/blobs/default```.
    - ```cache``` : Thư mục này bao gồm thông tin về bộ nhớ hiện tại của Karaf bundles.
    - ```db``` : Thư mục này bao gồm cơ sở dữ liệu OrientDB là bộ lưu trữ chính cho repository quản lý siêu dữ liệu(metadata).
    - ```elasticsearch``` : Thư mục này chứa trạng thái cấu hình hiện tại của elasticsearch về cơ bản elasticsearch là một công cụ tìm kiếm dựa trên nền tảng Apache Lucene.
    - ```etc``` : Thư mục này chứa cấu hình thời điểm chạy và tùy chỉnh trình quản lý kho lưu trữ.
    - ```health-check``` : Thư mục này bao gồm những bộ nhớ về báo cáo nhận được từ tính năng ```Repository Health Check```.
    - ```keystores``` : Thư mục này chứa những key đươc tạo tự động để  có thể xác định trình quản lý kho lưu trữ.
    - ```log``` : Thư mục này bao gồm một số tệp log để ghi lại về các khía cạnh khác nhau của trình quản lý kho lưu trữ hiện tại này.
    - ```tmp``` : Thư mục này được sử dụng để lưu trữ tạm thời.

<a id="run-nexus"></a>

### Chạy nexus

- Để chạy nexus chuyển đến thư mục /opt/nexus-3.18.1-01/bin rồi chạy lệnh ```./nexus run``` để chạy nexus, để có thể tắt trình quản lý kho lưu trữ khi đang chạy ta có thể sử dụng tổ hợp phím ```CTR C```.
- Ngoài ra thay vì run ta còn có thể chạy nexus với các lệnh ```start```, ```stop```, ```restart```, ```force-reload```, ```status``` tương ứng với bắt đầu, dừng, khởi động lại, bắt buộc tải lại hay trạng thái của nexus.
- Sau nexus bắt đầu chạy ta có thể truy cập thông qua giao diện người dùng bằng cách vào địa chỉ ```http://<server_host>:<port>``` ví dụ ```http://localhost:8081/```.
![image](images/nexus-home.png)
- Để có đầy đủ quyền truy cập thì cần phải dùng đến tài khoản admin khi lần đầu đăng nhập ta sẽ thấy thông báo nơi chứa mật khẩu tài khoản admin như sau:
![image](images/first-login.png)

---

<a id="run-as-service"></a>

## Chạy nexus as service. :running_man:

<a id="new-user"></a>

### Tạo người dùng mới

- Ta có thể cài đặt cho nexus để chạy như một service bằng systemd.
- Tạo một người dùng và trao đủ quyền để nó có thể chạy nexus service tiến hành tạo một user tên nexus: ```sudo adduser nexus``` cài không password cho user này.
- Chạy lệnh ```sudo visudo``` để sửa sudo file để có thể thay đổi những người dùng hay nhóm nào được phép chạy sudo. Thêm dòng sau vào và lưu lại ```nexus ALL=(ALL) NOPASSWD: ALL``` tức là user nexus có thể nhận được quyền root.
- Thay đổi quyền sở hữu các file của nexus với lệnh:

```
sudo chown -R nexus:nexus /opt/nexus-3.18.1-01
sudo chown -R nexus:nexus /opt/sonatype-work 
```

- Trong file ```opt/nexus-3.18.1-01/bin/nexus.rc```  ở đây ta chọn user nexus để chạy service sửa dòng ```run_as_user="nexus"``` 

<a id="systemd"></a>

### Chạy service với systemd

- Sau đó tạo một file service là một unit file với ***systemd*** là ```nexus.service``` trong thư mục ```etc/systemd/system``` file này sẽ định nghĩa làm sao để start, stop... service đó .
- Về cơ bản ***systemd*** là một nhóm các chương trình đặc biệt sẽ quản lý, vận hành và theo dõi các tiến trình khác hoạt động.
- Tất cả các chương trình được quản lý bởi systemd đều được quản lý dưới dạng ```deamon``` hay ```background``` và được cấu hình thành một file configuration được gọi là unit file.
- Sao đó chèn nội dung sau vào file service:

```
[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
ExecStart=$installdir/bin/nexus start
ExecStop=$installdir/bin/nexus stop
User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target
```

- Trong đó:
  - ***Unit, Service, Install*** là các section chính.
  - ***Unit***: Thường được đặt ở đầu bởi vì nó cung cấp tổng quan về unit này.
    - ***Description*** : Được sử dụng để mô tả tên và chức năng cơ bản của unit này.Sẽ tốt hơn nếu để một cái gì đó ngắn, đặc biệt và có nhiều ý nghĩa.
    - ***After*** : Ở đây giá trị là ```network.target``` để có thể chắc chắn rằng unit này sẽ được dừng trước khi tắt mạng nếu mà hệ thống tắt. Điều này cho phép các service sẽ chấm dứt sạch kết nối trước khi ngừng hoạt động thay vì đột ngột mất kết nối khiến cho các kết nối đang diễn ra ở trạng thái không xác định. Khi thêm ```After``` thì unit này chỉ bắt đầu sau khi các unit được chỉ định trong ```After``` được khởi động.
  - ***Service***: Được sử dụng để cung cấp cấu hình mà áp dụng cho service này.
    - ***Type***: Cấu hình loại khởi động process của unit có ảnh hưởng đến chức năng của ExecStart. Với ```forking``` tiến trình mà bắt đầu với ```ExecStart``` sẽ tạo ra một tiến trình con và thay thế trở thành tiến trình chính của service vì tiến trình cha mẹ sẽ thoát khi khởi động hoàn tất. Điều này cho ***systemd*** biết rằng quá trình này vẫn chạy mặc dù cha mẹ đã thoát
    - ***LimitNOFILE***: Mỗi tiến trình trên linux đều có một số giới hạn liên quan đến nó, chẳng hạn như số tệp tối đa mà nó có thể mở đồng thời. Để tăng giới hạn mở file ta sử dụng ```LimitNOFILE```
    - ***ExecStart***: Chỉ định một lệnh hoặc tập lệnh được thực thi khi unit khởi động.
    - ***ExecStop***: Chỉ định một lệnh hoặc tập lệnh được thực thi khi unit dừng.
    - ***User***: Chỉ định một người dùng để chạy service.
    - ***Restart***: Khi bật tùy chọn này với ```on-abort``` thì service sẽ chỉ được khởi động lại nếu tiến trình bị thoát mà không phải là do lệnh ```systemctl``` thực hiện (clean exit status)
  - ***Install***: Được sử dụng để xác định hành vi hoặc các tùy chọn của một unit nếu nó được bật hoặc tắt.
    - ***WantedBy***: là cách phổ biến nhất để xác định làm thế nào một đơn vị cần được kích hoạt với ```multi-user.target``` một mục có tên là ```multi-user.target.wants``` sẽ được tạo trong ```/etc/systemd/system``` và trong mục này sẽ có một liên kết tượng trưng (symbolic link) đến unit này.

- Lưu lại file trên và chạy các lệnh sau để khởi động nexus.

```
systemctl daemon-reload
systemctl enable nexus.service
systemctl start nexus.service
```

- Trong đó:
  - ***daemon-reload*** để load lại các service.
  - ***enable*** dùng để  service khởi động cùng với hệ thống.
  - ***start*** là để chạy service.
