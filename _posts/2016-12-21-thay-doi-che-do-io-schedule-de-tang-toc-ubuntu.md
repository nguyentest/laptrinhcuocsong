---
layout: post
title: Thay đổi chế độ đọc ghi lên đĩa cứng (io scheduling) để tăng tốc ubuntu
category: Linux - ubuntu
thumbnail: ubuntu-php.jpg
related_posts:
 - title: 
   link: http://laptrinhcuocsong.com/cai-dat-moi-truong-lap-trinh-web-tren-ubuntu-phan-2.html
 - title: 
   link: http://laptrinhcuocsong.com/cai-dat-moi-truong-lap-trinh-web-tren-ubuntu-phan-1.html
 - title: 
   link: http://laptrinhcuocsong.com/lap-trinh-tren-ubuntu-cac-phan-mem-web-developer-can-cai-dat.html
---

IO scheduling cách thức mà hệ điều hành quyết định thứ tự các khối lệnh vào/ra sẽ được chuyển đến bộ nhớ lưu trữ. Mặc định ubuntu 14.04 sử dụng chế độ deadline, đây không phải là chế độ đạt tốc độ cao nhất mà ổ cứng hỗ trợ, tuy nhiên chúng ta có thể thay đổi chế độ này để đạt hiệu quả cao nhất cho ubuntu.

Xét về tốc độ và hiệu suất làm việc trên ubuntu thì chúng ta có thể sắp xếp các chế độ như sau: bfq > cfq > deadline > noop

Các bạn có thể tìm hiểu thêm về các chế đô io schedule [tại đây](https://tinhte.vn/threads/cpu-governor-i-o-scheduler-la-gi-va-chung-anh-huong-nhu-the-nao-den-thiet-bi-android.2082989/#post-37408151)

Nói tóm lại lý thuyết thì rất lằng nhằng, giờ chúng ta làm thực tế luôn, để kiểm tra máy tính đang sử dụng chế độ io scheduling nào ta dùng lệnh:

```
cat /sys/block/sda/queue/scheduler
```
![chế độ io schedule](images/ubuntu-deadline.png)

Như bạn thấy, máy mình hỗ trợ 3 chế độ là noop, deadline và cfq, tuy nhiên hiện tại đang sử dụng [deadline] vì có 2 dấu đóng mở ngoặc vuông ở hai bên.

Bây giờ chúng ta sẽ chuyển lên chế độ cfq để đạt tốc độ đọc ghi nhanh hơn, đầu tiên mở file cấu hình của grub bằng lệnh:

```
sudo gedit /etc/default/grub
```

Gedit hiện ra, các bạn tìm dòng:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

Và thêm **elevator=cfq** vào như thế này:

![sửa chế độ io schedule](images/deadline-to-cfq.png)

Sau khi chỉnh sửa file cấu hình của grub, chúng ta sẽ update lại grub:

```
sudo update-grub
```

Khởi động lại máy và kiểm tra lại lần nữa, bây giờ chế độ io schedule đã được chuyển thành cfq với tốc độ đọc ghi cao hơn hẳn. Khi ở chế độ này độ trễ khi mở ứng dụng và tốc độ copy file đã được cải thiện một cách đáng kể.

![sửa chế độ io schedule](images/io-scheduler-before.png)

![sửa chế độ io schedule](images/io-scheduler-affter.png)

Chúc các bạn thành công!

