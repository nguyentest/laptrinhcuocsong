---
layout: post
title: Tổng hợp tất tần tật những công cụ cần thiết cho web developer
thumbnail: web-developer.png
category: Chuyện lập trình
related_posts:
 - title: Lập trình viên cần học những gì ?
   link: http://laptrinhcuocsong.com/lap-trinh-vien-can-hoc-nhung-gi.html
 - title: Lập trình viên PHP đứng đầy đường
   link: http://laptrinhcuocsong.com/lap-trinh-vien-php-dung-day-duong.html
 - title: Thay đổi chế độ đọc ghi lên đĩa cứng (io scheduling) để tăng tốc ubuntu
   link: http://laptrinhcuocsong.com/thay-doi-che-do-io-schedule-de-tang-toc-ubuntu.html
---
Làm gì cũng phải có công cụ, tất nhiên rồi, bạn không thể tạo ra một trang web bằng tay không. Nếu bạn là một web developer, những món "đồ nghề" sau đây sẽ giúp ích rất nhiều cho bạn, đây là những công cụ mà mình đang thường xuyên sử dụng trong công việc hàng ngày.

## Một code editor xịn

Code editor, hay trình soạn thảo code là một trong những cái căn bản nhất, hỗ trợ cho lập trình viên rất nhiều. Dùng notepad++ để code toàn bộ một website hoành tráng thì cũng hơi mệt. Lập trình android thì có android studio, lập trình ios đã có Xcode, lập trình .Net đã có visual studio, toàn cái xịn, riêng chỉ có lập trình web thì không theo thể thống nhất nào cả. Sublime text, phpdesigner, netbean, eclipse, phpStorm, notepad++ ... tạp nham  đủ thể loại, thế nên bạn phải chọn cho mình một cái mà bạn cảm thấy dễ dùng nhất, code nhanh nhất và gắn bó với nó.

Mình thường dùng [Sublime Text](https://www.sublimetext.com/) bởi nó nhẹ, nhiều plugin hỗ trợ và miễn phí :D

## Package manager và task runner

Tiếp theo bạn cần phải có package manager, là công cụ để quản lý các thư viện, giúp tiết kiệm thời gian, tránh phức tạp phiền phức khi cần chèn hay cập nhật các thư viện. Đồng thời bạn cũng cần task runner để tự động hoá một số thao tác thường gặp trong quá trình làm việc.

Mình dùng [composer](https://getcomposer.org/), [bower](https://bower.io/), [npm](https://www.npmjs.com/) và [gulp](http://gulpjs.com/)

## Quản lý Phiên bản

Việc dùng một hệ quản lý phiên bản mã nguồn là rất cần thiết, nó giúp quy trình làm việc code theo nhóm đơn giản hơn rất nhiều. Để sử dụng bạn cần cài đặt một git client như: [tortoisegit](https://tortoisegit.org/), [git for windows](https://git-scm.com/download/win) hay [sourcetree](https://www.sourcetreeapp.com/) và một dịch vụ repository hosting như Github hay Bitbucket.

## CSS preprocessors

CSS preprocessors giúp bạn viết code css nhanh hơn, thống nhất hơn với sự mở rộng hay ho như: hỗ trợ biến, hàm, compile và nén các tập tin css. Có hai css preprocessor phổ biến nhất là [less](http://lesscss.org/) và [sass](http://sass-lang.com/), mình sử dụng cả hai cái này, compiler cho nó thì có thể dùng CodeKit, Koala hay dùng compiler mặc định của less và sass luôn.

## Front-end framework

Bạn vẫn có thể code tay trang web của mình, nhưng đời không như mơ, việc đó quá mất thời gian trong khi bạn cần nhanh hơn để theo kịp tiến độ dự án, suy cho cùng, cái bạn cần là tạo ra sản phẩm nhanh và tốt, méo ai quan tâm code của bạn viết bằng cái gì đâu. Sử dụng Front-end framework cũng giúp làm việc nhóm hiệu quả hơn khi đồng đội của bạn cũng cùng sử dụng framework đó.

Với web, bạn có thể sử dụng [Bootstrap](http://getbootstrap.com/) vì nó rất phổ biến, ngoài ra có một framework khá nổi tiếng khác là Foundation 3 cũng khá tốt.

## Backend framework

Tương tự như frontend, về phía backend cũng tương tự, nguyên tắc DRY (Don't repeat yourself) dạy ta rằng không nên phát minh lại cái bánh xe, những thứ phải làm thường xuyên như thêm xóa sửa dữ liệu đã được đơn giản hóa rất nhiều bằng các framework, giúp bạn làm việc nhanh hơn, giảm bug phát sinh và tránh gặp những phiền phức không cần thiết. Mình khuyên là bạn nên chọn framework nào được nhiều người dùng nhất, chắc chắn bạn sẽ làm việc nhóm tốt hơn khi nhiều người biết framework của bạn.

Hiện mình chủ yếu làm việc với php nên mình chọn [Laravel](https://laravel.com/) và [Codeigniter](https://codeigniter.com/)

## Vài chrome extension hữu ích

Ngoài chrome developer tool quen thuộc thì bạn cũng nên cài vài extension mở rộng như [color zilla](https://chrome.google.com/webstore/detail/colorzilla/bhlhnicpbhignbdhedgjhgdocnmhomnp) để chọn màu trên trang web nhanh và chính xác, [measureit](https://chrome.google.com/webstore/detail/measureit/pokhcahijjfkdccinalifdifljglhclm?hl=vi) để đo đạc khi cắt giao diện cho chuẩn, 

## Nguồn ảnh và chỉnh sửa hình ảnh

Bạn cần hình ảnh để đăng lên blog, tuy nhiên các ảnh trên internet đa phần là có bản quyền, bạn lại không phải là nhiếp ảnh gia để tự chụp ảnh cho riêng mình. Bạn có thể lên FreePik để tìm kiếm hình ảnh, hầu hết các ảnh ở đây đều miễn phí và cho phép tải ở định dạng bitmap hay vector. Điều này là cực kỳ cần thiết, tránh phiền phức bản quyền sau này. 

Dân web developer thường không chuyên về đồ họa lắm, tuy nhiên bạn vẫn phải biết sử dụng photoshop, illustrator để cắt giao diện sang html, css. Trên linux mình hay sử dụng gimp,  tuy không bằng photoshop nhưng cái này cũng khá hay, hỗ trợ đầy đủ các tác vụ thông thường, và miễn phí.

Khi thiết kế hoặc cả khi code, đôi khi bạn cần một màu nào đó ngay lập tức, hãy đến website [http://color.hairpixcel.com](http://color.hairpixcel.com) và click, bạn sẽ có một màu đẹp.

## Thư viện javascript:

Có rất nhiều thư viên javascript bạn có thể sử dụng cho dự án của mình, phổ biến nhất là **jquery**, **angularJs** hoặc **vue.js**. Mục đích cuối cùng cũng chỉ là tiết kiệm thời gian công sức, tạo ra sản phẩm nhanh và hoàn thiện.

## Nguồn icon, font và icon font

Có hai cách để tạo icon trên web, một là dùng icon ảnh và icon font, mỗi cách có ưu nhược điểm khác nhau. Để tìm icon bạn có thể lên [IconFinder](https://www.iconfinder.com/), [IconMonster](https://iconmonstr.com/) để tìm, hoặc sử dụng các icon font có sẵn như [fontawesome](http://fontawesome.io/), [Fontello](http://fontello.com/). Font chữ cho web có rất nhiều trên google font, với sự phổ biến của CSS3, việc nhúng font chữ lên web đã trở nên rất đơn giản.

## Bug tracking: Quản lý lỗi với [bugsnag](https://www.bugsnag.com/)

Mình cũng chưa từng được dùng các hệ thống quản lý nào khác ngoài bugsnag nên không có ý kiến gì nhiều. Bạn không nhất thiết phải dùng bugsnag, nhưng việc có một hệ thống quản lý lỗi là rất cần thiết, sản phẩm chạy sinh ra lỗi sẽ được log lên hệ thống này, developer sẽ nhận được email đầy đủ thông tin, thuận tiện cho việc fix bug.

## Vẽ wireframe và thể hiện ý tưởng:

Wireframe là bản phác thảo thô mô tả tổng quan về sản phẩm, giúp dễ dàng truyền đạt ý tưởng tăng hiệu quả giao tiếp giữa các thành viên trong team. Mình đã có một bài viết về tầm quan trọng của wireframe và [cách để vẽ một wireframe tuyệt vời](http://laptrinhcuocsong.com/cac-buoc-tao-mot-wireframe-tuyet-voi.html). Mình sử dụng Balsamiq Mockups, đây là một phần mềm rất hay, nhưng tại vì nó phải trả phí, chỉ cho trial 30 ngày nên mình chuyển qua một phần mềm miễn phí là  [Pencil project](http://pencil.evolus.vn/).

## Tạo và quản lý task với [Jira](https://www.atlassian.com/software/jira)

Khi bạn làm việc trong một công ty phần mềm, bạn có thể sẽ được (hoặc bắt buộc) phải sử dụng một phần mềm quản lý task như Jira, nó giúp kiểm soát theo dõi vấn đề và lỗi phát sinh trong quá trình của một dự án. Ban đầu bạn có thể sẽ khá khó sử dụng, nhưng sau này bạn lại thích nó, và muốn áp dụng vào team của mình.

## Viết và chia sẻ

Với các bạn lập trình viên nói chung và web developer nói riêng, viết blog công nghệ và chia sẻ kinh nghiệm lập trình là một cách rất tốt để tự học và giúp đỡ cộng đồng. Thật dễ dàng để tạo cho mình một blog bằng wordpress, và chia sẻ code của bạn bằng jsfiddle, jsbin, hay codeshare.io.

Bạn cũng cần có thói quen ghi lại mọi thứ, đôi khi ở một nơi nào đó, bạn bất chợt có một ý tưởng hay một cách giải quyết vấn đề mới. Hãy ghi lại ngay bởi sau đó bạn rất có thể sẽ quên phéng mất, mình hay dùng google keep trên điện thoại để ghi chép ngay lúc đó, rất tiện lợi. Ngoài google keep, [evernote](https://evernote.com/) cũng là một dịch vụ tuyệt vời.

## Một vài cái mà web developer nào cũng dùng:

**Google Webmaster Tool**: là một công cụ hỗ trợ bạn quản lý website được cung cấp miễn phí bởi Google.

**Google Analytic**: một công cụ phân tích Website hết sức tin cậy, đây được xem là công cụ rất hiệu quả dành cho những Webmaster và những người làm SEO khi muốn thông kê những thông tin về website của mình.

**Zoho mail**: Giúp bạn tạo email theo tên miền riêng miễn phí, dạng your_name@domain.com rất chuyên nghiệp.

Đến đây thì mình viết mệt quá rồi, chắc chắn có thể còn thiếu, mình sẽ bổ sung khi nghĩ ra, đã gần 4 giờ sáng rồi. Hi vọng bài viết này giúp được chút gì đó cho bạn, chúc bạn thành công.



