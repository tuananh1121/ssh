# Log SSH
Xem log ssh ta dùng lệnh
```
# cat /var/log/secure | egrep -i ssh
hoặc 
# tail /var/log/secure | egrep -i ssh
```
![](/image/log1.png)

Theo dõi và đọc log ta dùng lệnh 
```
# tail -f /var/log/secure
```

* Trường hợp đăng nhập trực tiếp 
![](/image/log2.png)

Trong trường hợp này khi ta đăng nhập trực tiếp thì sẽ thấy có 2 log.

* Trường hợp đăng nhập gián tiếp
![](/image/log3.png)

Trong trường hợp này khi ta đăng nhập gián tiếp thì sẽ thấy có 1 log.
