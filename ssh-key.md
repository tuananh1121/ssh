# SSH Keypair
## Tạo khóa trên server
### Thực hiện cấu hình trên server
Tạo 1 cặp ssh key bằng câu lệnh sau:
```
# ssh-keygen -t rsa
```
![](/image/key1.png)

Nhập vào nơi lưu key hoặc enter để tự động lưu vào file mặc định, bấm enter.

![](/image/key2.png)

Vị trí 1: Nhập vào chuỗi mật khẩu để tăng tính bảo mật. Có thể sử dụng mật khẩu này để đăng nhập nếu không có mật khẩu của user.

Vị trí 2: Nhập lại mật khẩu vừa nhập ở trên.

![](/image/key3.png)

Key sau khi đã tạo xong

* Phân quyền cho cặp key
```
mv /root/.ssh/id_rsa.pub /root/.ssh/authorized_keys

chmod 600 /root/.ssh/authorized_keys

chmod 700 .ssh
```

Khởi động lại dịch vụ ssh
```
# systemctl restart sshd
```

### Cấu hình trên Client Window
**Load key với MobaXterm**

Trên MobaXterm, click vào tab `Tools`

![](/image/key4.png)

Sau khi click vào `tools` ta chọn `MobaKeyGen`

* Chọn file private key
![](/image/key5.png)

* Chọn đường dẫn đến file copy key từ server đã lưu ở phần trên. Sau đó sẽ có 1 của sổ hiện ra như bên dưới, nhập vào mật khẩu Passphrase sau đó chọn Ok để tiếp tục.

![](/image/key6.png)

* Như vậy ta đã load xong. Tiếp tục chọn `Save private key` để lưu lại `private key`, sau này dùng cho việc ssh.

![](/image/key7.png)

* Để kiểm tra, ta cần sử dụng key và ssh vào server. Hãy làm theo các bước sau :

![](/image/key8.png)

Ta sẽ ssh vào bằng user thuctap, sau khi nhập vào user ta sẽ không xác thực bằng mật khẩu của user đó mà sẽ sử dụng mật khẩu của Passphrase key.

![](/image/key9.png)

Sau khi nhập mật khẩu, ta sẽ login được vào bằng user và thao tác như bình thường.

![](/image/key10.png)

## Tạo khóa trên Client Window
### 1.Window
Đầu tiên ta vào MobaXterm Chọn `tools` và click vào `MobaKeyGen`

![](/image/key4.png)

Tiếp theo ta tiến hành việc tạo key

![](/image/key11.png)

![](/image/key12.png)

* Copy toàn bộ nội dung trong ô “Public key for pasting into OpenSSH authorized_keys file:” và lưu lại dưới tên authorized_keys rồi gửi lên Server. Đây là Public Key dành riêng cho OpenSSH

![](/image/key13.png)

* Nhập passphrase và chọn Save Private key. Việc tạo bộ khóa hoàn tất.

![](/image/key14.png)

* Tiếp theo ta đăng nhập và tạo một phiên ssh mới 

![](/image/key15.png)

### 2. Trên linux

Ta thực hiện các lệnh sau
```
# mkdir .ssh
# chmod 700 .ssh
# cat > authorized_keys ( Tạo file authorized_keys và copy key vừa tạo vào file này)
# chmod 600 /root/.ssh/authorized_keys
```
Sửa file `/etc/ssh/sshd_config` tìm đến dòng 65 sửa `yes` thành `no` để không cho đăng nhập bằng mật khẩu,chỉ cho phép đăng nhập bằng key

![](/image/key16.png)

Khởi động lại dịch vụ SSH
```
systemctl restart sshd
```






