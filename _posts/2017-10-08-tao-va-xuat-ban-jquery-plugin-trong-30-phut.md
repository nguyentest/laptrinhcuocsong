---
layout: post
title: Tạo và xuất bản một jquery plugin trong 30 phút
category: Chuyện lập trình
thumbnail: jquery-plugin.png
related_posts:
 - title: Tổng hợp 9 kênh youtube mà dân công nghệ nên theo dõi
   link: http://laptrinhcuocsong.com/tong-hop-9-kenh-youtube-ma-dan-cong-nghe-nen-theo-doi.html
 - title: Lập trình viên cần học những gì ?
   link: http://laptrinhcuocsong.com/lap-trinh-vien-can-hoc-nhung-gi.html
 - title: Tổng hợp tất tần tật những công cụ cần thiết cho web developer
   link: http://laptrinhcuocsong.com/tong-hop-nhung-cong-cu-can-thiet-cho-web-developer.html
---
Jquery có lẽ không còn xa lạ với các bạn web developer, nó là một thư viện javascript giúp tạo nhiều hiệu ứng trên website nhanh với cú pháp code đơn giản hơn. Jquery được sử dụng rộng rãi và ngày càng mạnh mẽ bởi nhiều plugin mở rộng. Cũng đú theo phong trào ấy, chúng ta sẽ cùng nhau tạo và xuất bản một plugin đơn giản nhất.

## Plugin này làm được gì ?

Đầu tiên phải giới thiệu cái plugin của chúng ta đã, nó là plugin làm nhiệm vụ xem trước ảnh trước khi upload, kiểu như lúc đăng ảnh lên facebook, bạn bấm chọn ảnh, facebook sẽ hiện ảnh nhỏ nhỏ cho bạn xem trước khi quyết định đăng. Mình tạm đặt tên plugin này là Jpreview.

Bạn có thể xem code trên github: [tại đây](https://github.com/buivannguyen/jpreview)

Hoặc cài đặt thông qua composer: `composer require buivannguyen/jpreview`

## Các file cần thiết

Mình bắt đầu tạo một thư mục mới cùng các file cần thiết như sau:

- composer.json : Đây là file chứa các thông tin của gói jpreview để sau khi xuất bản có thể cài đặt bằng composer.
- demo.html : Là file demo sử dụng plugin của chúng ta.
- jpreview.js : Đây là file javascript chính, thực hiện xử lý việc xem trước ảnh
- jpreview.css : File css mặc định

## Bắt đầu thôi

Ok, chúng ta bắt đầu với đoạn code tạo plugin kinh điển, nó là anonymous function nhận object jQuery là tham số.

```javascript
(function ( $ ) {

    $.fn.jPreview = function() {
        console.log('jPreview loaded');
         // code xử lý ở đây
    };
    
}( jQuery ));
```

Tiếp theo là viết hàm chính jPreview, chúng ta muốn rằng sau khi plugin hoàn thành, nó có thể được gọi như thế này:

```javascript
$(document).ready(function(){
	$('.demo').jPreview();
});
```

Thế nên chúng ta sẽ viết hàm jPreview, nó được nằm trong `$.fn`

```javascript
(function ( $ ) {

    $.fn.jPreview = function() {
        console.log('jPreview loaded');
         // code xử lý ở đây
    };
    
}( jQuery ));
```

Đến đây thì đã có thể gọi plugin trong demo.html được rồi, mở chrome developer tool lên sẽ thấy "jPreview loaded"

Để có thể hiện ảnh, trước hết phải viết một hàm đọc image data url từ một file bất kỳ.

var jPreview = this;

jPreview.readImageData = function(file, successCallback){
    var reader = new FileReader();
    reader.onload = function(event){
        successCallback(event.target.result);
    }
    reader.readAsDataURL(file);
}

Và hàm thực hiện hiển thị ảnh này ra.

jPreview.addPreviewImage = function(container, imageDataUrl){
    $(container).append('<div class="jpreview-image" style="background-image: url('+ imageDataUrl +')"></div>');
}

Hàm trên sẽ thêm các div có background là biến imageDataUrl và hiển thị vào div có id là biến container.

Tiếp theo chúng ta sẽ viết hàm hiển thị ảnh của một cái input bất kỳ, kịch bản là khi input đó thay đổi (change event) thì sẽ lấy từng file của nó, đọc image data url, rồi hiển thị nó ra.

```javascript
jPreview.preview = function(selector){
    var container = $(selector).data('jpreview-container');

    $(selector).change(function(){
        $(container).empty();
        $.each(selector.files, function(index, file){
            var imageData = jPreview.readImageData(file, function(data){
                jPreview.addPreviewImage(container, data);
            });
        });
    });
}
```

Như các bạn thấy, biến container được lấy từ thuộc tính `data-jpreview-container`, như vậy người dùng sẽ tiện lợi hơn vì muốn hiện ảnh vào div nào cũng được. Kiểu như:

```javascript
<input type="file" data-jpreview-container="#some_div_want_to_preview">
<div id="some_div_want_to_preview"></div>
```

Vì selector có thể nhiều hơn một, ví dụ họ chọn bằng class như thế này: `$(".class")` chẳng hạn. Thế nên chúng ta phải thực hiện lặp qua tất cả selector để preview

```javascript
// start it
var selectors = $(this);
return $.each(selectors, function(index, selector){
    jPreview.preview(selector);
});
```

Ok, đến đây chúng ta đã hoàn thành plugin này, bạn có thể viết thêm tí css cho đẹp, cũng như làm vài cái demo vào `demo.html` cho nó trông chuyên nghiệp tí. Đây là code hoàn chỉnh:

```javascript
(function ( $ ) {
 
    $.fn.jPreview = function() {
        var jPreview = this;

        jPreview.preview = function(selector){
            var container = $(selector).data('jpreview-container');

            $(selector).change(function(){
                $(container).empty();
                $.each(selector.files, function(index, file){
                    var imageData = jPreview.readImageData(file, function(data){
                        jPreview.addPreviewImage(container, data);
                    });
                });
            });
        }

        jPreview.readImageData = function(file, successCallback){
            var reader = new FileReader();
            reader.onload = function(event){
                successCallback(event.target.result);
            }
            reader.readAsDataURL(file);
        }
        
        jPreview.addPreviewImage = function(container, imageDataUrl){
            $(container).append('<div class="jpreview-image" style="background-image: url('+ imageDataUrl +')"></div>');
        }

        // start it
        var selectors = $(this);
        return $.each(selectors, function(index, selector){
            jPreview.preview(selector);
        });
 
    };
 
}( jQuery ));
```

## Xuất bản plugin để cài được bằng composer

Bước đầu tiên để xuất bản plugin này là tạo file composer.json như sau:

```javascript
{
    "name": "buivannguyen/jpreview",
    "type": "library",
    "description": "jquery plugin preview image before upload",
    "keywords": ["preview image","jquery plugin preview"],
    "homepage": "https://github.com/buivannguyen/jpreview",
    "license": "MIT",
    "authors": [
        {
            "name": "Nguyen Bui Van",
            "email": "toi@buivannguyen.com",
            "homepage": "http://buivannguyen.com",
            "role": "Developer"
        }
    ]
}
```

Mình tạo một repository trên github tại địa chỉ https://github.com/buivannguyen/jpreview và bắt đầu commit code lên repository này, sau đó tạo bản release phiên bản 1.0

![Github](images/jpreview-github.png)

Bước cuối cùng là tạo một tài khoản trên https://packagist.org rồi paste link github vào để submit package này lên. Bây giờ thì đã có thể cài đặt jpreview bằng lệnh:

> composer require buivannguyen/jpreview

Chúc các bạn có một ngày chủ nhật vui vẻ, bây giờ thì mình đi uống bia :D
