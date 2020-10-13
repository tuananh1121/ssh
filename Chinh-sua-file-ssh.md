# Chỉnh sửa file cấu hình SSH
Để chỉnh sửa file cấu hình ssh, ta sử dụng lệnh sau
```
vi /etc/ssh/sshd_config
:set nu
```
![](/image/port1.png)

## 1. Đổi port SSH

![](/image/port2.png)

* Dịch vụ SSH mặc định hoạt động trên port `22` . Vì là port phổ biến , rất dễ bị kẻ xấu thực hiện các hoạt động dò tìm mật khẩu tự động đăng nhập SSH vào hệ thống
* Để điều chỉnh port mặc định , xuống dòng 17 Port, chỉ định port mới , đồng thời bỏ dấu `#` ở đầu dòng

## 2. Giới hạn IP lắng nghe ssh
![](/image/port3.png)

* Nếu hệ thống có nhiều hơn 1 địa chỉ IP thì tốt nhất nên chỉ định rõ địa chỉ IP nào sẽ lắng nghe port SSH . Thực hiện sửa đổi ở dòng `19 ListenAddress` , đồng thời bỏ dấu # ở đầu dòng ( 0.0.0.0 có nghĩa là mọi IP đều lắng nghe SSH )

## 3. Timeout khi user đăng nhập không thành công

![](/image/port4.png)

* Khi 1 user đăng nhập SSH , nếu không chỉ định thông tin user từ đầu thì sẽ hiện ra 1 prompt yêu cầu nhập thông tin user . Sau đó là phần nhập mật khẩu nếu user đó đăng nhập bằng mật khẩu . Ta sẽ quy định thời gian 1 kết nối SSH đợi cho hoạt động đăng nhập user thành công , nếu sau khoảng thời gian này không đăng nhập được thì ngắt kết nối.
* Thay đổi tùy chọn này ở dòng `37 LoginGraceTime`( mặc định đã được cấu hình là 2 phút )

## 4. Không cho user `root` đăng nhập

![](/image/port5.png)

* Để tăng tính bảo mật cho hệ thống, bạn không nên cho đăng nhập bằng user root.
* Khi muốn sử dụng quyền root thì chỉ cần tạo user rồi cấp quyền sudo cho user đó.
* Để ngăn không cho ssh bằng tài khoản `root`. Tìm đến dòng `38 PermitRootLogin`, sửa `yes` thành `no` đồng thời bỏ dấu `#` ở đầu dòng

## 5. Chế độ "Strict Mode"

![](/image/port6.png)

* Ta sẽ chỉ định dịch vụ SSH phải kiểm tra thông tin quyền của thư mục `$HomeUser` , thư mục `.ssh` và file `authorized_keys` chứa key SSH nếu dùng SSH key.
* Nếu không sử dụng chế độ này ( `no` ) thì SSH sẽ không kiểm tra cấu hình các quyền khi đăng nhập vào Server -> Ép người quản trị phải cấu hình đúng các phân quyền ( permissions ) cho các thư mục / key dùng để đăng nhập SSH
* Thay đổi tùy chọn này ở dòng `39 StrictModes` (mặc định để yes)

## 6. Thiết lập số lần đăng nhập sai tối đa

![](/image/port7.png)

* Nếu đăng nhập sai số lần quy định sẽ ngắt kết nối của Client .
* Thay đổi tùy chọn này ở dòng `40 MaxAuthTries`( mặc định là 6 )

## 7. Số phiên đăng nhập SSH tối đa

![](/image/port8.png)

* Thay đổi giá trị tại dòng `41 MaxSessions `(mặc định là 10)

## 8. Sử dụng chứng thực bằng SSH key , thay vì mật khẩu

* Mặc định , mỗi VPS/Cloud Server sẽ đăng nhập vào bằng user root hoặc user thường . Tuy nhiên việc sử dụng mật khẩu có 2 nguy cơ lớn là :
   * Mất toàn bộ hệ thống nếu để lộ mật khẩu
   * Hacker có thể dùng phương thức tấn công BruteForce để dò ra mật khẩu
* Vì vậy nên dùng SSH Key để đăng nhập vào Server cũng như sử dụng nó để xác thực các kết nối từ bên ngoài vào cho an toàn hơn . Đồng thời , nếu có thể nên tắt cấu hình chứng thực mật khẩu.
* Thực hiện thay đổi ở dòng `43 PubkeyAuthentication` và `65 PasswordAuthentication`
![](/image/port9.png)
![](/image/port10.png)

## 9. Tắt log Last login

![](/image/port11.png)

* Để tắt log đăng nhập lần cuối, ta chỉnh sửa dòng `106 PrintLastLog` (mặc định là yes) đổi thành `no`

## 10. Cấu hình thời gian ngắt kết nối SSH khi user không hoạt động

![](/image/port12.png)

* Có thể quy định thời gian timeout mà 1 kết nối SSH đến Server Linux không nhận được bất kỳ hoạt động tương tác nào trên Terminal SSH . Lúc này nếu quá thời gian quy định thì SSH Server sẽ tự ngắt kết nối từ các user không tương tác.
* Thực hiện thay đổi ở dòng `112 ClientAliveInterval` và `113 ClientAliveCountMax`, đồng thời bỏ dấu # ở đầu dòng

## 11. Giới hạn User/Group sử dụng cho SSH

* Mặc định SSH Server cho phép tất cả các user local đăng nhập qua SSH . Nhưng đôi khi cần chặn không cho đăng nhập với 1 số user nhất định hoặc 1 nhóm cụ thể
* Để cho phép user hoặc group được đăng nhập SSH , thực hiện thêm vào 1 số dòng sau vào cuối file
```
AllowUsers user_name1 user_name2
AllowGroups group_name1 group_name2
```
* Để không cho phép user hoặc group được đăng nhập SSH , thực hiện thêm vào 1 số dòng sau vào cuối file
```
DenyUsers user_name1 user_name2
DenyGroups group_name1 group_name2
```

## 12. Khởi động lại dịch vụ SSH

```
systemctl restart sshd
systemctl enable sshd
```






