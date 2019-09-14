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


# Q&A:

QUESTION:
- checkout : checkout như thế nào là pass, em đã thử checkout với commit hash cụ thể chưa, checkout bị conflict thì xử lý như thế nào
- branch : cách xem local branch ra sao , remote branch như thế nào , tạo mới branch remote/local, có nhất thiết branch remote là origin không, anh có thể làm sao chỉ pull code từ branch remote về local nhưng không push lên được, làm sao để push code lên 1 repo A branch Abr, sau đó code tự động đẩy lên repo B branch Bbr ?
- làm sao anh commit 1 file trong cả 100 file đang modify dở ?, anh không muốn push 1 file cố định tại mọi lần push thì làm thế nào( bỏ qua file đó ). ?
- Git log có ý nghĩa gì , em hiểu gì từ nó , có thể làm được gì với git log ?
- có mấy kiểu rebase, so sánh, và dùng nó trong trường hợp nào , dùng cách nào tiện , lợi hơn .
- merge : khi merge bị conflict thì xử lý như thế nào ?
- pull request / merge request hiểu như thế nào ?
---------------
ANSWER  
* Checkout như thế nào là pass: git checkout nhảy sang branch mới thành công. Khi checkout theo commit hash cụ thể, con trỏ sẽ nhảy sang branch state có chứa commit hash (Khi đó commit trên client và trên git server là giống nhau từ commit đến nội dung file. Sẽ có trường hợp checkout về commit giống nhau nhưng souce ko giống => cần reset source ở local branch và pull lại). Nếu GIT bị merge conflict:
  * Khi bị conflict thì cần phải sửa các conflict đó. Conflict không tránh được nhưng có thể làm giảm số lượng conflict xuống bằng các rebase thường xuyên 
  * có thể rollback lại state commit trước đó bằng **--amend**
  * Hoặc checkout theo mã hash trước khi bị conflict
* Xem branch local/remote: **git remote show origin**
  Không nhất thiết mọi branch remote là origin, origin chỉ là cái tên default, có thể xem/custom current remote bằng lệnh: **git remote -v** AND **git remote rename thuongpt11 origin**
  Nếu muốn chỉ pull code về mà không push code lên được, em nghĩ là nên set repo private thay vì public, và từ đó set quyền contributor, phần này liên quan permissions, **cần tìm hiểu thêm** phần settings của repo + team( phần này tốn xèng nên có thời gian phải nghịch git3 để tìm tương tự). Hiện tại vd git3 grant quyền develop cho devopssupport (nhiều lúc dự án grant nhầm quyền read access).
  **Push code lên một repo A, branch Abr; chuyển code sang repo B, branch Bbr: ** Đang ngâm link này nhưng chưa hiểu lắm:https://stackoverflow.com/questions/2428137/how-to-rebase-one-git-repository-onto-another-one/2428224#2428224
* commit 1 file trong 100 file: git add+ tên file ;add file vào danh sách chờ để thông báo sẽ commit file nào lên tiếp theo
  anh không muốn push 1 file cố định tại mọi lần push thì làm thế nào( bỏ qua file đó ). ? : chạy lệnh **git rm --cached tên_file_exclude** để .gitignore sẽ không theo dõi file này trong danh sách chờ(git add), sau đó thực hiện commit và push như thường
* Git log: một file lưu lại lịch sử chỉnh sửa, người chỉnh sửa đã note sửa gì, có các commit hash nữa. Git log show chỉ mặt điểm tên nên có lỗi thì sẽ trace và ping người chỉnh sửa nhanh hơn, đồng thời có thể rollback lại state ổn với mã hash.
* Rebase: em đang hiểu ở đây nó được sử dụng để backup một branch cũ, tạo mới 1 branch từ đó; kiểu lấy code để release với khách hàng/ phát triển chức năng mới. Các kiểu rebase, so sánh: Git Rebase Standard vs Git Rebase Interactive
  * Git Rebase Standard: các thông số đã đc set sẵn( for example an ID, a branch name, a tag, or a relative reference to HEAD), rebase nhanh hơn, thuận lợi nếu bê cả branch
  * Git Rebase Interactive: kiểu manual, chọn từng file để rebase, có thể set lại các thông số, kiểm soát quản lý chặt chẽ hơn
  * https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase
* Merge:
  Git status xem phần conflict, vào phần file source code bị conflict được đề cập ở HEAD chỉnh sửa, sau đó thực hiện git add và thực hiện git commit lại. 
* git pull = fetch + merge 
-----------------------
LESSION LEARN
* Rảnh quá là không tập trung được :))
* Đùa thôi nhưng em chưa thông não xong cơ chế GIT branching, với workflow của nó
* Cũng đẩy/get được vài file xàm xàm với GIT
* Chưa nghịch GIT command bao giờ nên mới vọc cũng hơi ngượng tay, tính ra thì được cái deadline thì có động lực hẳn, cơ mà lúc tìm hiểu đang thiếu mục tiêu hoàn thành, nên cũng hơi mông lung.
* Highlight recommended link from **cs50**: 
  https://www.youtube.com/watch?v=eulnSXkhE7I
  https://www.youtube.com/watch?v=dAHgwd2U0Jg