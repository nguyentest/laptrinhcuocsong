---
layout: post
title: Học làm hacker
thumbnail: hacker.png
category: Chuyện bên lề
related_posts:
 - title: Tôi đã hack Chợ Tốt như thế nào
   link: http://laptrinhcuocsong.com/toi-da-hack-cho-tot-nhu-the-nao.html
 - title: Lập trình viên cần học những gì ?
   link: http://laptrinhcuocsong.com/lap-trinh-vien-can-hoc-nhung-gi.html
 - title: Thất vọng sự trở lại của hiệp hội hacker Việt Nam - HVA
   link: http://laptrinhcuocsong.com/that-vong-su-tro-lai-cua-hiep-hoi-hacker-viet-nam-hva.html
---

Để trở thành hacker cần phải học gì, cần có những hiểu biết cơ bản gì, hack như thế nào?  Thật sự nó quá khó để trả lời, ngay cả nếu hỏi một hacker chuyên nghiệp, vì họ không có chuyên môn sư phạm, một câu trả lời không thể giúp bạn trở thành hacker , nó là cả một quá trình tích lũy kinh nghiệm. Để không bị chửi hay ném đá, bài viết này mình chỉ chia sẻ và trả lời câu hỏi "Làm thế nào để hack một website" , câu hỏi mà mình nhận được quá nhiều sau khi đăng bài viết "[tôi đã hack Chợ Tốt như thế nào?](http://laptrinhcuocsong.com/toi-da-hack-cho-tot-nhu-the-nao.html)".

![hacker](images/hacking-banner.jpg)

Trước hết phải xác định rằng bạn không phải đang đọc bài viết của một hacker, mà chỉ là một thằng coder quèn bỏ học đại học lang thang code dạo, cá kiếm ít cơm cháo sống qua ngày. Mình hoàn toàn không học về bảo mật thông tin, cũng không kiếm tiền ở lĩnh vực này, chỉ chịu khó tìm tòi nghiên cứu, thi thoảng check những lỗi rất-thông-thường của các website và báo lỗi cho họ. Điển hình là báo lỗi cho Chợ Tốt, VietnamWorks, và hệ thống quản trị thông tin hành chính tỉnh X phát triển bởi VNPT...

Họ thương thì cho ít tiền cafe, không thì mình cũng rất vui vì giúp được một chút gì đó cho họ, cho người dùng, cho ai đó mà mình không biết nữa. Cái mình nhận được từ những ngày nghiên cứu, nghịch ngợm "như một hacker" là một góc nhìn rất mới lạ, thú vị, giúp ích rất nhiều cho công việc lập trình của mình.

## Hacker phải biết lập trình

Mình nói thật, không biết lập trình thì bỏ đi, không có hack hiếc gì cả, before you break the rules you have to learn the rules, trước khi làm gì đó với một website, bạn phải biết website nó hoạt động như thế nào, được tạo ra như thế nào. Trước khi tán con bé hàng xóm, cũng phải biết nó thích gì, hay đi đâu, nó có hay xem porn không, nhà có giàu không... Hãy học lập trình thật tốt, bạn sẽ tự biết hack một cách rất tự nhiên thôi.

> Tôi không biết lập trình, tôi chỉ muốn thử hack một cái gì đó, để thử cảm giác được làm hacker có được không?

Có, cho vui thì được, hiện có rất nhiều tools, hướng dẫn trên Google để bạn có thể tự mình hack, để đặt avatar mặt nạ anonymous cho ngầu để tán gái, chỉ cần bạn có một đam mê khám phá và tinh thần học hỏi. Nhưng dù gì thì gì, hack vẫn là một hành động phạm tội, và bạn sẽ không tiến xa được với cách tiếp cận này đâu. Mình đã gặp rất nhiều bạn sky's vì xem nhiều phim hacker mà sinh ra ảo tưởng, hừng hực trên con đường "nghiên cứu bảo mật" mà thất vọng, chán nản bất mãn với đời, các bạn đừng như thế nhé :)

## Làm thế nào để hack một website?

Lảm nhảm khá nhiều mới đến chủ đề chính, chúng ta sẽ tìm hiểu cách một website bị hack như thế nào. Tất nhiên đây chỉ là dưới góc độ cá nhân, vì như ở trên đã nói, mình chỉ là dạng tay mơ, không phải các bước của một hacker chuyên nghiệp, để các bạn đọc chơi cho vui.

## Thu thập thông tin

Khi đã có "ý đồ đen tối" với một website cụ thể, đầu tiên check info server xem website đó đang dùng hosting của dịch vụ nào, hay là dùng VPS - Server riêng, server đó đang chạy hệ điều hành gì, version mấy.... thử xem robots.txt xem họ có giấu giếm cái gì không, thử google xem nó có error nào mà google vô tình thu thập được không.

Nó đang dùng mã nguồn nào, nếu là dùng mã nguồn mở (wordpress, joomla, drupal...) thì check luôn version của mã nguồn đó nếu có thể. Họ có dùng https không, dùng theme hay plugin nào phụ thêm không? Tên miền của nhà cung cấp nào, ai là chủ nhân tên miền, có các sub-domain nào... vân vân và mây mây, tóm lại là thu thập càng nhiều thông tin càng tốt.

## Tìm kiếm bug đã tồn tại trên mã nguồn, hệ điều hành của website

Với các thông tin đã thu thập được, bạn bắt đầu Google các lỗi còn tồn tại đã được công bố. Web họ dùng centos 6.4, wordpress 4.3 và vài theme với plugin nữa, hãy google ngay xem phiên bản này có lỗi gì không, nếu có thì phương pháp tấn công của họ như thế nào?

Đa số các mã nguồn mở nổi tiếng thì rất ít bug và được cộng đồng vá rất sớm sau khi được công bố, tuy nhiên các website thông thường không chịu khó theo dõi và cập nhật các bản vá này. Ngoài ra, họ sử dụng rất nhiều theme, plugin, addon chưa được kiểm định, do vậy khả năng dính lỗi khá cao. Khi đã tìm ra lỗi thì dễ rồi :))

## Local attack

Từ thông tin server ở bước 1, bạn bắt đầu check  những site nằm trên cùng server này, để xem có thể "làm ăn" được gì từ những site này không. Nếu may mắn hack được một site trên cùng server, up shell để local sang website mục tiêu, có những diễn đàn hacking, UG có một đội ngũ chuyên up shell cho member, có thể vào đó để xin link shell :)

Các shared-host lúc nhúc hàng trăm web trên cùng một server có thể dễ dàng hơn trong việc local và dễ dàng mua được một gói host nhỏ nằm cùng server với mục tiêu để hành động.

## Tìm kiếm những lỗ hổng từ website

Nếu source code của website là tự viết, không dùng mã nguồn mở, và các bước trên có vẻ không hiệu quả, bạn bắt đầu check những lỗi, những sơ hở mà lập trình viên vô tình tạo ra. Cái này thì vô vàn, và cần có kinh nghiệm. Bắt đầu từ cách website hoạt động, bạn kiểm tra các file javascript, kiểm tra các ajax request... xem trình duyệt gửi nhận thông tin gì, nếu thay đổi dữ liệu input thì chuyện gì sẽ xảy ra. Dễ dàng nhất là check theo top các lỗi bảo mật web OWASP đã được công bố.

## Vẫn có những con đường khác

Thực tế thì vẫn có những con đường khác, cái này thì tùy từng website mà có cách ứng biến phù hợp tùy thuộc vào hiểu biết của bạn về website đó. Một website thường không đứng độc lập, nó có thể tương tác với hệ thống thanh toán bên ngoài, là api dữ liệu cho ứng dụng mobile... và vẫn có những sơ hở khác tồn tại. Bản thân mình đã từng hack bằng cách dịch ngược file apk của một hệ thống và đọc code của nó, gửi mail cho nhân viên cty đó có đính kèm malware... duy chỉ có chat chit, gọi điện khai thác theo hướng social engineering là chưa làm do không có tài chém gió :))

## Kết luận

Hack cần tư duy lập trình tốt và sự sáng tạo, tìm hiểu về bảo mật thông tin, Những mánh khóe, thủ thuật mà hacker sử dụng có ích giúp bạn lập trình tốt hơn. Tất cả các lập trình viên nên tạo thói quen "đa nghi", đứng dưới góc nhìn của hacker để lập trình tốt hơn khi xây dựng một ứng dụng an toàn

