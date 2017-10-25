---
layout: post
title: Lập trình trên ubuntu, tổng hợp các phần mềm web developer cần cài đặt
category: Linux - ubuntu
related_posts:
 - title: 
   link: http://laptrinhcuocsong.com/nhung-phan-mem-nen-cai-dat-tren-ubuntu.html
 - title: 
   link: http://laptrinhcuocsong.com/cai-dat-moi-truong-lap-trinh-web-tren-ubuntu-phan-1.html
 - title: 
   link: http://laptrinhcuocsong.com/thay-doi-che-do-io-schedule-de-tang-toc-ubuntu.html
---
Các bạn lập trình viên khi mới chuyển qua môi trường linux, mà cụ thể ở đây là Ubuntu cần phải cài đặt những phần mềm gì để có thể "lập trình được". Đã có rất nhiều bài viết về vấn đề này, ở đây chúng ta sẽ tổng hợp lại, dưới đây là các phần mềm mà bản thân mình đang dùng, có thể tạm gọi là complete setup để lập trình viên PHP lập trình trên Ubuntu.

Lưu ý đây là các phần mềm dành cho PHP developer, các nhu cầu khác như xem phim nghe nhạc, chơi game, chat chit tán gái các bạn tham khảo ở bài [Những phần mềm nên cài đặt trên ubuntu](http://laptrinhcuocsong.com/nhung-phan-mem-nen-cai-dat-tren-ubuntu.html)

## Trình soạn thảo code:

Tất nhiên rồi, đã là coder thì phải có cho mình một trình soạn thảo code đủ tốt, đừng nghe bọn nó xúi dại viết code trên notepad hay gedit nhé, bạn cần công cụ giúp viết code nhanh và ít mắc lỗi hơn. Cá nhân mình không thích các chương trình viết code quá cồng kềnh, mà chỉ cần nhẹ nhàng vài tính năng cơ bản cần thiết như: auto complete, syntax highlight, code folding,... là đủ.

Với nhu cầu đó mình chọn [Sublime text](http://www.sublimetext.com/) và [Atom](https://atom.io/)

Ngoài ra còn có nhiều phần mềm khác cho các bạn lựa chọn: [Brackets](http://brackets.io/), [Visual Studio Code](https://code.visualstudio.com/), [Netbeans](https://netbeans.org/), [Eclipse](https://www.eclipse.org/) ...

## Trình duyệt:

Hầu hết thời gian web developer làm việc trên trình duyệt, mà trình duyệt thì tào lao mỗi đứa một kiểu, việc thiết kế trang web tương thích với nhiều trình duyệt luôn là vấn đề nan giải, do đó khuyên bạn nên cài nhiều trình duyệt nhất có thể, để còn test.

Mình dùng chủ yếu [Chrome](https://www.google.com/intl/vi_vn/chrome/browser/desktop/index.html) và [Firefox](https://www.mozilla.org/vi/firefox/new/) cho việc hiển thị, debug javascript

## Technical stack: tôi chọn LAMP

Bên blog Tôi đi code dạo đã có một bài viết Stack là gì nên mình cũng không phải giới thiệu nhiều, nó là một cục các phần mềm được gom lại với nhau để cài đặt một cách nhanh chóng.

Trên Ubuntu, mình dùng stack quen thuộc nhất: LAMP (Linux, Apache, MySQL, PHP)

## Git GUI client:

Sử dụng một hệ thống quản lý phiên bản như Git là rất phổ biến trong quy trình phát triển phần mềm. Có nhiều lập trình viên quản lý git bằng command line, tuy nhiên để làm việc hiệu quả với Git thì quả thật mất thời gian rất dài, vậy tại sao không để phần mềm làm việc đó, chúng ta sẽ chỉ tập trung vào việc code.

Có nhiều phần mềm quản lý git bằng giao diện, cái nào cũng tuyệt vời như SmartGit, git-cola, gitg, GitEye, Cycligent Git Tool...

Tuy nhiên mình thích dùng Gitkraken và Sourcetree

## Quản lý cơ sở dữ liệu

Quản lý cơ sở dữ liệu cũng là nhu cầu rất cần thiết, nhưng mỗi loại cơ sở dữ liệu lại có các phần mềm quản lý riêng. Với lập trình viên PHP chúng ta thường làm việc với mysql là chủ yếu.

Mình dùng Mysql workbench và Emma

## Phần mềm FTP

Phần mềm FTP là ứng dụng hỗ trợ upload, download thông qua giao thức FTP, nôm na là để chuyển file lên server.

Mình chọn Filezilla vì dễ sử dụng, cross platform

## Sử dụng terminal tốt hơn với Terminator

Với php developer bạn thường xuyên sử dụng command line để build css, chạy package manager và task runner. Ứng dụng Terminal của ubuntu thì cũng có nhiều điểm hạn chế, thế nên bạn cần một Terminal tốt hơn, Terminator là ứng cử viên.

## Phần mềm đồ họa:

Bạn vẫn có thể cài đặt photoshop trên ubuntu theo như mình đã giới thiệu trong bài Cài đặt môi trường lập trình web trên ubuntu - Phần 2 . Tuy nhiên vẫn có các phần mềm đồ họa miễn phí nhưng lại rất tốt, nhanh và tiện lợi.

Ngoài photoshop mình dùng thêm cả Inkscape và Gimp

## Vẽ wireframe với Pencil project

Khi cần vẽ wireframe và thể hiện ý tưởng, wireframe là bản phác thảo thô mô tả tổng quan về sản phẩm, giúp dễ dàng truyền đạt ý tưởng tăng hiệu quả giao tiếp giữa các thành viên trong team.

Với nhu cầu này, mình dùng Pencil project, đây là một phần mềm rất hay, dễ sử dụng và miễn phí.

## Các thứ lặt vặt khác:
Ngoài các công cụ trên, còn lặt vặt nhiều phần mềm khác, chỉ cần chịu khó tìm hiểu, sau một thời gian bạn hoàn toàn có thể sử dụng tốt Ubuntu phục vụ công việc của mình.
Ví dụ: Công cụ chọn màu nhanh Gpick, composer, bower, npm, gulp

Chúc các bạn thành công.
