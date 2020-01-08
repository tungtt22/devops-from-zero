# Backup và restore gitlab

## Mục lục :book:

- [Backup timestamp](#timestamp)
- [Tạo một backup trên hệ thống gitlab](#backup)
- [Lưu trữ file config](#store)
- [Các tùy chọn backup](#option)
  - [Backup strategy option](#strategy)
  - [Backup file name](#filename)
  - [Rsyncable](#rsyncable)
  - [Loại bỏ một số mục không thực hiện backup](#exclude)
- [Tải file backup lên một kho lưu trữ từ xa](#upload)
  - [Sử dụng Amazon S3 cho việc lưu trữ backup](#amazon)
  - [Cấu hình cron để chạy backup daily](#cron)
- [Restore gitlab](#restore)

<a id="timestamp"></a>

## Backup timestamp

---

- Từ bản Gitlab 9.2 thì timestamp format được thay đổi từ EPOCH_YYYY_MM_DD sang EPOCH_YYYY_MM_DD_GitLab_version.

- Ví dụ :1493107454_2018_04_25 sẽ thành 1493107454_2018_04_25_10.6.4-ce.

- Thư mục lưu trữ mặc định sẽ được lưu trong **backup_path** được chỉ định trong ``config/gitlab.yml`` đối với gitlab cài đặt qua source còn đối với omnibus gitlab ta có thể sửa đổi trong ``/etc/gitlab/gitlab.rb``. Tên file sẽ là [TIMESTAMP]_gitlab_backup.tar, trong đó **TIMESTAMP** sẽ chỉ ra khi nào thì file backup này được tạo và cộng thêm phiên bản gitlab vào sau. Timestamp là cần thiết khi ta restore gitlab và backup lại nhiều lần.

- Ví dụ: 1493107454_2018_04_25_10.6.4-ce_gitlab_backup.tar ta thêm phiên bản gitlab vào sau 1493107454_2018_04_25_10.6.4-ce.

<a id="backup"></a>

## Tạo một backup trên hệ thống gitlab

---

- Ta có thể backup:
  - db (database)
  - uploads (attachments)
  - repositories (Git repositories data)
  - builds (CI/CD job output log)
  - artifacts (CI/CD job artifacts)
  - lfs (lfs object)
  - registry (Container Registry images)
  - pages (page content)

- Tiến hành tạo một bản backup trước khi update ```sudo gitlab-backup create``` (với gitlab từ phiên bản 12.1 ta sử dụng lệnh ```gitlab-rake gitlab:backup:create```) mặc định dữ liệu backup sẽ được lưu trong thư mục **/var/opt/gitlab/backups**

<a id="store"></a>

## Lưu trữ <i>config file</i>

---

- Ta có thể backup lại những config từ đây
- Với Omnibus gitlab file config thường là:
  - ``/etc/gitlab/gitlab-secrets.json``
  - ``/etc/gitlab/gitlab.rb``
- Với gitlab cài đặt từ source:
  - ``/home/git/gitlab/config/secrets.yml``
  - ``/home/git/gitlab/config/gitlab.yml``

<a id="option"></a>

## Các tùy chọn backup

<a id="strategy"></a>

### Tùy chọn <i>backup strategy</i>

---

- Cái cách backup dữ liệu mặc định là truyền dữ liệu từ các từ các vị trí lưu trữ dữ liệu tương ứng để backup sử dụng linux command như tar và gzip để nén lại.

- Khi sử dụng lệnh **tar** để đọc dữ liệu có thể xảy ra lỗi ***file changed as we read it*** có thể xảy ra nếu dữ liệu thay đổi và nó có thể khiến cho tiến trình backup đang chạy bị fail.

- Để khắc phục được điều này, trong Gitlab bản 8.17 đã giới thiệu một cơ chế backup gọi là copy. Cơ chế này có nghĩa là nó sẽ sao chép dữ liệu ra một vị trí tạm thời nào đó sau đó mới chạy lệnh **tar** và **gzip** để tránh cho việc backup bị lỗi.

- Có một tác dụng phụ đó là việc backup có thể tốn thêm bộ nhớ, tiến trình backup này sẽ xóa sạch các file ở thư mục tạm thời để tránh ở mỗi giai đoạn để tránh cho vấn đề xảy ra.

- Để sử dụng <i>copy strategy</i> ta thêm vào lệnh như sau: ```sudo gitlab-backup create STRATEGY=copy```

<a id="filename"></a>

### Backup filename

---

- Thông thường như phần backup timestamp backup file sẽ được lưu dưới dạng timestamp + gitlab version tuy nhiên ta có thể ghi đè phần [TIMESTAMP] như sau: ```sudo gitlab-backup create BACKUP=dump```
- Kết quả file backup sẽ đổi thành **dump_gitlab_backup.tar**. Tùy chọn này sẽ hữu ích khi hệ thống sử dụng rsync và incremental backup tốc độ truyền sẽ nhanh hơn.

<a id="rsyncable"></a>

### Rsyncable

---

- Để đảm bảo việc lưu trữ được thực hiện bằng rsync, sử dụng tùy chọn ```GZIP_RSYNCABLE=yes``` điều này sẽ cài đặt ```--rsyncable``` sang gzip. Và sẽ hữu ích khi kết hợp với backup filename như ở trên
- ```sudo gitlab-backup create BACKUP=dump GZIP_RSYNCABLE=yes```

<a id="exclude"></a>

### Loại bỏ một số mục không thực hiện backup

---

- Ta có thể chọn những mục mà ta không muốn backup:
  - db (database)
  - uploads (attachments)
  - repositories (Git repositories data)
  - builds (CI job output logs)
  - artifacts (CI job artifacts)
  - lfs (LFS objects)
  - registry (Container Registry images)
  - pages (Pages content)

- ```sudo gitlab-backup create SKIP=db,uploads``` với lệnh này ta sẽ skip không backup db và mục uploads.

<a id="upload"></a>

## Tải file backup lên một kho lưu trữ từ xa

---

- Bắt đầu từ bản gitlab 7.4 thì ta có thể khiến cho backup script tải lên file backup mà nó tạo ra(file tar). Gitlab sử dụng **Fog library** của ruby cho việc thực hiện upload.

<a id="amazon"></a>

### Sử dụng Amazon S3 cho việc upload backup

---

- Amazon S3 hay còn gọi là Amazon Simple Storage Service là một dịch vụ lưu trữ đơn giản cung cấp bởi Amazon Web Services cung cấp lưu trữ đối tượng.

- Đầu tiên ta tiến hành tạo một [access key](https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html)

- Thêm vào file config như sau:

```bash
gitlab_rails['backup_upload_connection'] = {
  'provider' => 'AWS',
  'region' => 'eu-west-1',
  'aws_access_key_id' => 'AKIAKIAKI',
  'aws_secret_access_key' => 'secret123'
  # If using an IAM Profile, don't configure aws_access_key_id & aws_secret_access_key
  # 'use_iam_profile' => true
}
gitlab_rails['backup_upload_remote_directory'] = 'my.s3.bucket'
```

- Cài đặt các thông tin để tạo kết nối tới AWS như ví dụ trên ta chỉ việc thay đổi region thích hợp và điền thông tin về access key ta đã tạo trên gitlab

<a id="cron"></a>

### Cấu hình cron để chạy backup daily

---

- Việc đặt lịch để sao lưu sẽ không backup lại config file

- Tiến hành cấu hình thời gian để giữ một file backup vào ```/etc/gitlab/gitlab.rb``` ở ví dụ dưới đây đã cài đặt cho thời gian để giữ backup file cũ là 7 ngày

```rb
## Limit backup lifetime to 7 days - 604800 seconds
gitlab_rails['backup_keep_time'] = 604800
```

- Tiến hành reconfig gitlab để những thay đổi có hiệu quả ```sudo gitlab-ctl reconfigure```

- Để lên lịch cho việc sao lưu định kỳ các repositories và các gitlab metadata ta phải sử dụng root user

```sh
sudo su -
crontab -e
```

- Với ```crontab -e``` sẽ cho phép ta sửa crontab hiện tại, sử dung trình chỉnh sửa đã được chỉ định trong biến môi trường.

- Tiến hành đặt lịch để backup mỗi ngày

- ```0 2 * * * /opt/gitlab/bin/gitlab-backup create CRON=1``` thực hiện backup mỗi ngày vào lúc 2 giờ sáng với **CRON=1** thì sẽ không hiển thị output khi chạy lệnh nếu không có lỗi nào xảy ra và giảm thiệu việc cron spam

<a id="restore"></a>

## Restore gitlab

---

- Sau khi backup thì ta có thể tiến hành khôi phục lại từ file backup

- Tất nhiên việc restore cần chuẩn bị trước một số việc như:
  - Chạy ```sudo gitlab-ctl reconfigure``` ít nhất một lần
  - Gitlab phải đang chạy, sử dụng ```sudo gitlab-ctl start```

- Phải đảm bảo rằng file backup (tar file) đã ở trong thư mục backup. Mặc định thư mục backup là ```/var/opt/gitlab/backups``` và nó cần được sở hữu bởi một user là **git**

```sh
sudo cp 11493107454_2018_04_25_10.6.4-ce_gitlab_backup.tar /var/opt/gitlab/backups/
sudo chown git.git /var/opt/gitlab/backups/11493107454_2018_04_25_10.6.4-ce_gitlab_backup.tar
```

- Dừng các tiến trình được kết nối với cơ sở dữ liệu như *unicorn* và *sidekiq*

```b
sudo gitlab-ctl stop unicorn
sudo gitlab-ctl stop sidekiq
```

- Sau đó tiến hành kiểm tra hai tiến trình đã được stop hay chưa ```sudo gitlab-ctl status```

- Sau đó để khôi phục lại backup chỉ định timestamp mà ta muốn backup

```b
# This command will overwrite the contents of your GitLab database!
sudo gitlab-backup restore BACKUP=1493107454_2018_04_25_10.6.4-ce
```

- Đối với bản gitlab 12.1 và các phiên bản trước đó sử dụng ```gitlab-rake gitlab:backup:restore```

- Đối với các bản gitlab từ 12.2 và mới hơn ta có thể sử dụng ```gitlab-backup restore```

- Tiếp theo tiến hành khôi phục lại ```/etc/gitlab/gitlab-secrets.json``` nếu cần thiết bởi vì file này chứa các khóa mã hóa cơ sở dữ liệu(database encryption key), các biến CI/CD, và các biến cho việc xác thực 2 bước (two-factor authentication) nếu ta không khôi phục tệp mã hóa này cùng với việc sao dữ liệu ứng dụng thì người dùng kích hoạt xác thực 2 bước hoặc Gitlab Runner mất quyền truy cập vào gitlab server.

- Sau khi thực hiện khôi phục xong restart và kiểm tra lại gitlab

```b
sudo gitlab-ctl reconfigure
sudo gitlab-ctl restart
sudo gitlab-rake gitlab:check SANITIZE=true
```

- Nếu có sự không phù hợp giữa gitlab version và backup file thì câu lệnh restore ở trên sẽ xảy ra lỗi ta tiến hành cài đặt phiên bản phù hợp và thử khôi phục lại
