# 1. GIT ,GITHUB là gì?
* **GIT**
  * Là một hệ thống quản lý phiên bản phân tán [Distributed Version Control Systems (DVCSs)](https://en.wikipedia.org/wiki/Distributed_version_control) 
  * GIT lưu lại trạng thái file, lịch sử chỉnh sửa(vd: mã commit, người chỉnh sửa),và có thể reset file về phiên bản mong muốn sử dụng; Ngoài ra, những người dùng trong cùng team có thể quản lý, update source code một cách nhanh nhất khi pull về
* **GITHUB**
  * GitHub là service UI cung cấp kho lưu trữ mã nguồn Git dựa trên nền web cho các dự án phát triển phần mềm. GitHub hiện nay đang hỗ trợ 2 phiên bản: miễn phí và có phí cho người dùng. 
# 2. Các khái niệm liên quan
* **Repository**: Được hiểu như kho làm việc, quản lý,lưu trữ source code. Có 2 loại repo là :remote và local. Khi người dùng muốn sharing source code, họ thực hiện action push
  * Remote repository thường được chia sẻ công khai/ một nhóm người nhất định; và nó được đặt ở site server chuyên dụng. 
  * Local repository: lưu trữ cá nhân, thường là một người sử dụng
* **Branch**: Là workspace của dự án, các branch phân chia độc lập với nhau để phát triển các tính năng. Trong 1 repo có thể có nhiều branch, sự thay đổi source code trên từng branch không ảnh hưởng đến những branch khác. Branch local có thể liên kết với branch remote hoặc không;các branch có thể kết hợp với nhau bằng merge hoặc rebase. Trong trường hợp không mong muốn khi merge, có thể xảy ra conflict source. 
* **Log**: đây là một kho chứa commit, lưu trữ tất cả thông tin lịch sử commit
* **Merge** : gộp nhánh các công việc bị tách ra trước đây thành một snapshot mới <img src="https://git-scm.com/figures/18333fig0328-tn.png " height=300px width=600px /> 
* **Rebase** :sử dụng tất cả các thay đổi được commit ở một nhánh và "chạy lại" (replay) chúng trên một nhánh khác.
* **Conflict:** xảy ra khi có hai thay đổi trên cùng một dòng code, và máy tính không thể quyết định nên giữ cái nào. Phần HEAD sẽ show ra sự khác biệt giữa hai lần thay đổi để người dùng tự quyết định.
* **Checkout**: Để chuyển con trỏ sang một branch đang tồn tại (change workspace)

# 3. Thực hành với GIT
* Cài đặt GIT
* Common command: [GIT cheat sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)
# 4. References
* https://cs50.harvard.edu/beyond/2019/winter/lectures/#afternoon-git-and-github-sass
* https://git-scm.com
* https://github.com/fsoftdocs/Thuctap-SDS