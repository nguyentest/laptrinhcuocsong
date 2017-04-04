---
layout: post
title: Hướng dẫn giải whiteHat warGame - web security bài 1 đến bài 4
thumbnail: hacker-whitehat.png
category: Chuyện bên lề
related_posts:
 - title: Lập trình viên cần học những gì ?
   link: http://laptrinhcuocsong.com/lap-trinh-vien-can-hoc-nhung-gi.html
 - title: Trả lời câu hỏi của bạn đọc
   link: http://laptrinhcuocsong.com/tra-loi-cau-hoi-ban-doc.html
 - title: Xem video này bạn sẽ muốn ngồi vào bàn và lập trình ngay lập tức
   link: http://laptrinhcuocsong.com/xem-video-nay-ban-se-muon-ngoi-vao-va-lap-trinh-ngay-lap-tuc.html
---
WhiteHat WarGame là trang web hacking test của diễn đàn hacker mũ trắng Việt Nam (do lão Quảng BKAV tạo ra :) được thiết kế dạng capture the flag (cướp cờ) với nhiều cấp độ từ dễ đến khó. Rất hữu ích cho các bạn mới tìm hiểu về lĩnh vực bảo mật thông tin. Trong bài viết này mình sẽ hướng dẫn các bạn giải từ bài 1 đến bài 4 của web security challenge.


Bạn có thể xem tất cả các thử thách tại đây: [https://wargame.whitehat.vn/Challenges/List/2](https://wargame.whitehat.vn/Challenges/List/2)

## Bài 1:

Đây có thể là level cơ bản nhất nên rất dễ dàng tìm ra, cờ được giấu ở mã ẩn của code HTML bình thường. Chỉ cần view source ra là sẽ thấy, copy nó và nộp bài là xong

![white hat hacking](images/whitehat-wargame-1.jpg)

## Bài 2:

Bài này view source ra bạn sẽ không thấy cờ đâu. Nhưng để ý một chút, ở dòng cuối cùng thẻ html ẩn có nội dung như sau: “You can find it, but search engines can not”. Mình đã loay hoay thử đổi user-agent của http header để gửi lên, nhưng không được. Cuối cùng nhớ đến mình làm SEO thường hay chặn google bot không cho nó lục lọi các file bí mật trên host. Nên thử xem robots.txt của nó xem sao.

Kết quả:

![white hat hacking](images/whitehat-wargame-2.jpg)


Quá tốt, việc còn lại chỉ là xem file /protected/s3cr37.txt và cờ đã hiện ra :)

## Bài 3:

Bài này có nâng cao hơn một chút, nó chỉ hiện một trang đăng nhập, khi view source ra bạn sẽ thấy ở dưới cùng có “test/test”. mình đã thử đăng nhập bằng tài khoản “test” và mật khẩu “test”, nó chấp nhận, nhưng vào trong thì chỉ hiện “You are not admin.” mà chả thấy cờ đâu :( mình đã đăng nhập, nhưng mình không có quyền admin, như vậy thử thách là phải trở thành admin. Nguyên tắc của một ứng dụng web an toàn là “mọi thứ lưu trên client đều có thể bị sửa đổi”, mình thử xem cookie của nó thì thế này:

![white hat hacking](images/whitehat-wargame-3.jpg)


Việc còn lại là sửa cookie của nó và F5. Bạn có thể sử dụng extension có tên là Edit This Cookie để sửa, copy cờ và đi nộp bài

## Bài 4:

Ở bài này nó chỉ hiện một ô nhập mật khẩu trống trơn và vô tình :) khi view source ra mình nhận được một đoạn mã javascript loằng ngoằng như thế này:

![white hat hacking](images/whitehat-wargame-4.jpg)

Đây là một đoạn javascript đã được mã hóa obfuscator, may mà hồi xưa mình hay tìm cách mã hóa code php để khỏi bị xóa bản quyền khi share code nên biết cái này. Sau khi tìm một vài công cụ decode nó, mình đã có code javascript thô:

![white hat hacking](images/whitehat-wargame-5.jpg)

Như các bạn thấy, dòng 1 đến 9 có nhiệm vụ tạo ra mật khẩu, mình chỉ việc tạo một file html mới, copy dòng 1 đến 9 vào, thêm `console.log(correct)` rồi chạy là có được mật khẩu: `egonsrtyzfdsrty`

Đến đây thì thằng bạn gọi mình đi uống bia, đúng lúc đang thèm. Hi vọng các bạn cảm thấy thú vị khi đọc bài viết này, các bài tiếp theo mình sẽ đăng bài giải trong các post kế tiếp.