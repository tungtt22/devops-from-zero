# 1. Git là gì
Git là một trong những Hệ thống Quản lý Phiên bản Phân tán
Trên Git, có thể lưu trạng thái của file khi có nhu cầu dưới dạng lịch sử cập nhật. Vì thế, có thể đưa file đã chỉnh sửa một lần về trạng thái cũ hay có thể hiển thị sự khác biệt ở nơi chỉnh sửa.
Để ghi lại việc thêm/ thay đổi file hay thư mục vào repository thì sẽ thực hiện thao tác gọi là Commit. Khi thực hiện commit có yêu cầu nhập giải thích commit (commit message). Vì commit message là bắt buộc nên nếu để trống mà thực hiện thì commit sẽ thất bại.
# 2. Workflow 

![Workflow](Workflow.png)

# 3. Các lệnh cơ bản 

**3.1 Config tool**
$ git conffig --global user.name "name"
$ git config --global user.email "email"
**3.2 Repositories**
$ git init [prj-name]
$ git clone [url]
**3.3 Changes**
$ git status
$ git diff
$ git add [file]
$ git diff --staged
$ git reset [file]
$ git commit -m "[mess]"
**3.4 group changes**
$ git branch : show tất cả các branch trong repo
$ git branch [branch-name] : tạo branch mới
$ git checkout [branch name] chuyển qua branch khác 
$ git merge [branch] combines branch cũ  và branch hiện tại
$ git branch -d [branch name] : xoá branch
**3.5 Refactor**
$ git rm [file] xoá file
$ git rm --cached [file] : xoá file khỏi version control nhưng giữ tại local
$ git rm [file-original] [file-rename] đổi tên file
**.6 History**
$ git log : xem history của branch hiện tại
$ git log --flow [file] list các version của file
$ git dif [first-branch]...[second-branch] show nội dung diff giữa 2 branch
$ git show [commit] show sự thay đổi nội dung commit
**3.7 Synchronize**
$ git fetch [bookmark] download all history từ repo bookmark
$ git merge [bookmark]/[branch] combines bookmark's branch vào branch của local
$ git push [alias] [branch] upload all local branch commit to git
$ git pull 
**3.8 Redo commits**
$ git reset [commit] undoes tất cả các commit sau khi [commit]
$ git reset --hard [commit] huỷ tất cả history và quay lại [commit]

