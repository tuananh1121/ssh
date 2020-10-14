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




