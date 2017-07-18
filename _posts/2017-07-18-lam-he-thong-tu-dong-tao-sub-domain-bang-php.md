---
layout: post
title: Làm hệ thống tạo sub-domain tự động theo username bằng php
thumbnail: sub-domain.png
category: Chuyện lập trình
related_posts:
 - title: Viết tính năng tự động nâng cấp phiên bản cho code PHP (PHP auto-upgrade system)
   link: http://laptrinhcuocsong.com/viet-tinh-nang-tu-dong-cap-nhat-phien-ban-code-php.html
 - title: Test website trên thiết bị di động như thế nào?
   link: http://laptrinhcuocsong.com/test-website-tren-thiet-bi-di-dong-nhu-the-nao.html
 - title: Tổng hợp tất tần tật những công cụ cần thiết cho web developer
   link: http://laptrinhcuocsong.com/tong-hop-nhung-cong-cu-can-thiet-cho-web-developer.html
---

Chắc hẳn bạn thấy rất nhiều trang web cung cấp cho người dùng những url như thế này: username.domain.com trong đó username là do người dùng tự chọn. Những sub-domain kiểu này trông rất thân thiện và chuyên nghiệp, rất tuyệt vời phải không? Trong bài viết này, chúng ta sẽ làm nó.

Nghe thì có vẻ phức tạp thế thôi chứ nguyên tắc thì đơn giản cực kỳ, chúng ta sẽ cấu hình để tất cả sub-domain sẽ chạy qua một wildcard DNS record. Cụ thể là trong trang quản trị domain, mình sẽ tạo một DNS record như thế này:

```javascript
*.domain.com
```


Khi đã cấu hình xong, thì tất cả sub-domain sẽ đều trỏ về root của webserver, mở trình duyệt web lên, gõ thử vài sub linh tinh:

```javascript
abc.domain.com
xyz.domain.com
nguyendepzai.domain.com 
...
```

Tất cả đều hiện trang index.php

Đến đây thì nhiệm vụ cực kỳ đơn giản là tách được cái sub kia ra để lấy username của người dùng, chúng ta có thể dùng htaccess như sau:

```javascript
RewriteCond %{HTTP_HOST} ^(^.*)\.domain.com
RewriteRule (.*)  index.php?username=%1
```

Sau đó lấy $username = $_GET['username'] hoặc có một cách khác đó là lấy trực tiếp từ $_SERVER["REQUEST_URI"] như sau:

```javascript
$url = $_SERVER["REQUEST_URI"];
$username = str_replace(".domain.com","",$url);
```

Với thủ thuật rất đơn giản này, bạn đã có thể cho người dùng đăng ký sub-domain của riêng họ một cách rất chuyên nghiệp và mang lại sự tin tưởng cho website của bạn. Chúc các bạn thành công.
