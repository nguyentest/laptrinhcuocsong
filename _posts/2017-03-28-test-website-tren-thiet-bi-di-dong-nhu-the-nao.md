---
layout: post
title: Test website trên thiết bị di động như thế nào?
thumbnail: mobile.png
category: Chuyện lập trình
related_posts:
 - title: Các bước tạo một wireframe tuyệt vời
   link: http://laptrinhcuocsong.com/cac-buoc-tao-mot-wireframe-tuyet-voi.html
 - title: Lập trình viên cần học những gì ?
   link: http://laptrinhcuocsong.com/lap-trinh-vien-can-hoc-nhung-gi.html
 - title: Lập trình viên PHP đứng đầy đường
   link: http://laptrinhcuocsong.com/lap-trinh-vien-php-dung-day-duong.html
---
Cùng với sự phát triển của các thiết bị di động, lượng người sử dụng smartphone và máy tính bảng để truy cập internet ngày càng tăng. Do đó việc test một website trên thiết bị di động trước khi xuất bản nó là rất quan trọng và cần thiết.

Có nhiều cách để làm việc này, tuy nhiên không có một phương pháp nào hoàn hảo cả, mỗi cách có ưu và nhược điểm riêng. Trên thế giới có hàng tỉ thiết bị đang được kết nối internet, hàng triệu loại điện thoại và máy tính bảng có thể truy cập website của bạn. Dưới đây là 5 cách test website trên thiết bị di động được sắp xếp từ tốt nhất đến dễ dàng thực hiện nhất.

![thiết bị di động](images/thiet-bi-di-dong.png)

## 1. Test trên thiết bị thật

Đây là cách tốt nhất khi website được kiểm tra trên thiết bị thật, sờ nắm được, bởi có rất nhiều yếu tố không thể có được bằng các phần mềm giả lập.

Trong điều kiện lý tưởng, trang web sẽ được test trên mọi thiết bị mà nó được xem. Tuy nhiên điều này là không thực tế, mỗi dự án đều có giới hạn về ngân sách nhất định, mà nếu có tất cả các thiết bị, bạn cũng không có đủ thời gian để test hết chúng.  Chúng ta phải chấp nhận rằng, website tương thích với "tất cả" các thiết bị là điều không thể. Tuy nhiên với sự ra đời của tiêu chuẩn thiết kế web w3c, các website đã tương thích với hầu hết các thiết bị thông dụng. Nếu bạn đang tham gia một dự án phục vụ lượng người dùng lớn, thì hãy test trên nhiều thiết bị nhất có thể.

## 2. Test trên phần mềm giả lập

Phương pháp này chủ yếu để test sự tương thích với các trình duyệt web mặc định của hệ điều hành, mặc dù không thể thay thế cho thiết bị vật lý, test website trên phần mềm giả lập vẫn là phương pháp cho hiệu quả khá tốt. Trải nghiệm người dùng trên phần mềm giả lập vẫn chưa hoàn toàn giống như trên thiết bị thật với nhiều yếu tố biến đổi như: tốc độ mạng, mật độ điểm ảnh, kích thước điểm chạm, độ dài ngón tay, phần cứng thiết bị...

May mắn thay, android và iOS là hai hệ điều hành di động phổ biến, khi bài test vượt qua 2 hệ điều hành phổ biến này, bạn có thể yên tâm rằng website của chúng ta đã tương thích với đa số thiết bị trên thế giới. Trình giả lập iOS có sẵn trong Xcode và trình giả lập android đã có trong bộ android sdk, ngoài ra còn vài trình giả lập khác như genymotion hay bluestack miễn phí luôn sẵn sàng để các lập trình viên tải về và sử dụng.

## 3. Test trên BrowserStack

Có một dịch vụ khá hay tên là [BrowserStack](https://www.browserstack.com), trang web này cung cấp cho chúng ta bộ giả lập nhiều thiết bị ngay trên nền web mà không cần phải cài đặt bất kỳ phần mềm nào trên máy tính của mình. Có rất nhiều thiết bị "ảo" cho bạn lựa chọn, từ các thiết bị android, ios, windows phone và cả máy tính chạy Mac với nhiều phiên bản khác nhau. Tin buồn đây là dịch vụ trả phí, với phiên bản miễn phí bạn chỉ được test trong vòng 20 phút, tuy nhiên đây là dịch vụ khá hay dành cho bạn test website cá nhân hoặc cho các dự án có nguồn kinh phí hạn hẹp.

## 4. Sử dụng chrome developer tool

Có lẽ đây là phương pháp cổ điển và kém hiệu quả nhất mà các chúng ta thường sử dụng. Các web developer kiểm tra bằng cách kéo tăng giảm kích thước trình duyệt trên máy tính và cầu nguyện rằng nó sẽ tương thích với các trình duyệt phổ biến. Điều này rất tốt và đáng khuyến khích, thực hiện nhanh và đơn giản, tuy nhiên nên nhớ rằng đây chưa gọi là "test", có rất nhiều thiết bị trong thế giới thực với hàng tỉ cấu hình khác nhau, chưa kể có hàng loạt trình duyệt không chính thống của bên thứ ba như: dolphin, next browser, uc browser, maxthon... làm cho việc tương thích càng khó khăn hơn.

## Còn bạn? Bạn dùng cách nào để test?

Trên đây vẫn chưa phải là danh sách tất cả các phương pháp để kiểm tra website trên thiết bị di động, có thể vẫn còn có phương pháp nào đó mà mình bỏ lỡ. Bạn thường dùng công cụ nào để test? hãy comment bên dưới để mọi người cùng biết, bởi vấn đề tương thích với các thiết bị di động là vấn đề gây đau đầu của hầu hết lập trình viên website.
