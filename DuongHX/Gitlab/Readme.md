# Gitlab.

## Cài đặt và cấu hình những dependencies cần thiết.

```
sudo apt-get update
sudo apt-get install -y curl openssh-server ca-certificates
```

## Thêm gói cài đặt gitlab và cài đặt gói.

```
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
```

- Tiến hành cài đặt gitlab.
```
sudo apt-get install gitlab-ee
```

- Ta cũng có thể sửa đổi cấu hình gitlab trong file /etc/gitlab/gitlab.rb.

- Truy cập vào gitlab.
![gitlab](images/gitlab-home.png)

