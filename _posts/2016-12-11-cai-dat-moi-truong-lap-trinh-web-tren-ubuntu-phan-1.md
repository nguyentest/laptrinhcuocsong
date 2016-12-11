---
layout: post
title: Cài đặt môi trường lập trình web trên ubuntu - Phần 1
category: Linux - ubuntu
thumbnail: ubuntu-php.jpg
---
Bạn là web developer trên ngôn ngữ php và muốn sử dụng ubuntu trong công việc của mình. Ubuntu hoàn toàn có đủ khả năng và hỗ trợ tốt công việc của bạn. Trong bài viết này mình sẽ giới thiệu cách thiết lập môi trường cho lập trình viên web trên ubuntu.

### Bước 1: Cài đặt MySql và Apache:

Đầu tiên chúng ta sẽ cài MySql:

```
sudo apt-get install mysql-server mysql-client
```

Trong quá trình cài đặt, bạn phải điền mật khẩu root của MySql.

Tiếp theo chúng ta sẽ cài Apache:

```
sudo apt-get install apache2
```

Và cài mod php5 cho nó:

```
sudo apt-get install php5 libapache2-mod-php5
```

Đến đây thì bạn đã có thể truy cập localhost bằng trình duyệt được rồi. Tiếp theo chúng ta sẽ cài các gói hỗ trợ liên quan, trong đó có gói php5-mysql để php có thể làm việc với MySql:

```
sudo apt-get install php5-mysql php5-curl php5-gd php5-idn php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-ming php5-ps php5-pspell php5-recode php5-snmp php5-sqlite php5-tidy php5-xmlrpc php5-xsl
```

Các gói này là các gói cơ bản nhất mà các ứng dụng web thường dùng, có thể bạn sẽ không cần một vài gói trong số này, bạn có thể bỏ nó đi tùy theo nhu cầu sử dụng. Sau đó khởi động lại appache:

```
sudo /etc/init.d/apache2 restart
```

### Bước 2: Tùy chỉnh thư mục root của apache

Khi cài đặt xong, thư mục root của apache mặc định nằm ở /var/www/html mà mình thì lại không thích thư mục này lắm, mình muốn nó ở www luôn cho tiện. Mình lần lượt chạy các câu lệnh sau:

Bật mod rewrite:

```
sudo a2enmod rewrite
```

Mở file config của apache bằng gedit:

```
sudo gedit /etc/apache2/sites-available/000-default.conf
```

Gedit hiện ra, mình sửa DocumentRoot lại thành

```
DocumentRoot /var/www
```

Và thêm đoạn này vào giữa cặp thẻ <VirtualHost>

```
<Directory /var/www/>
  Options Indexes FollowSymLinks MultiViews
  # changed from None to FileInfo
  AllowOverride All
  Order allow,deny
  allow from all
</Directory>
```

Khởi động lại apache lần nữa để thay đổi có hiệu lực. Thực ra bạn có thể đặt Document Root ở bất kỳ đâu bạn muốn, miễn là bạn cảm thấy tiện lợi khi làm việc là được.

### Bước 3: Cấp quyền cho thư mục làm việc

Cài đặt xong, bạn hăm hở mở code editor và lưu file vào thư mục /var/www nhưng không thể lưu được, bạn phải chmod lại thư mục đó để có thể thoải mái tạo, sửa, xóa file trong thư mục này:

```
sudo chmod username /var/www
```

Trong đó username là user của bạn (khi cài đặt ubuntu)

Trong phần tiếp theo, mình sẽ hướng dẫn các bạn cài đặt và thiết lập các phần mềm liên quan như sublime text để viết code, mysql workbench để quản lý cơ sở dữ liệu, cài đặt gimp và photoshop để xử lý ảnh, cắt giao diện và các thứ lặt vặt khác như svn, git, ftp, less ... Tóm lại là tất tần tật mọi thứ để có thể lập trình web được trên ubuntu.

Chúc các bạn thành công.
