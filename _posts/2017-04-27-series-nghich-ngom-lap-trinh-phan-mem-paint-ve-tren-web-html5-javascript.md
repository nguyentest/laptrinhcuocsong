---
layout: post
title: Series nghịch ngợm - Lập trình phần mềm paint, vẽ trên web với html5 và javascript
thumbnail: drawing.png
category: Chuyện lập trình
related_posts:
 - title: Xem video này bạn sẽ muốn ngồi vào bàn và lập trình ngay lập tức
   link: http://laptrinhcuocsong.com/series-nghich-ngom-lam-game-hung-trung.html
 - title: Nếu một ngày những đoạn mã lập trình biến mất
   link: http://laptrinhcuocsong.com/neu-mot-ngay-nhung-doan-ma-lap-trinh-bien-mat.html
 - title: Lập trình viên PHP đứng đầy đường
   link: http://laptrinhcuocsong.com/lap-trinh-vien-php-dung-day-duong.html
---
Lập trình phần mềm vẽ là một trong những đề tài mà hầu hết các bạn đang học IT muốn làm, bởi vì nó rất thú vị. Hiểu đơn giản nó giống phần mềm paint của windows, người dùng có thể chọn màu, chọn độ dày nét bút và vẽ tự do lên đó.

Đường nét ngoằn ngoèo phức tạp của người dùng khi vẽ tự do là rất khó để biểu diễn bằng công thức toán học, đa phần là các bố vẽ linh tinh nhăng cuội. Để giải quyết vấn đề này, chúng ta xem đường nét đó là tập hợp của vô số đường thẳng vô cùng ngắn, nối tiếp nhau.

![vẽ đường cong](images/ve-duong-cong.png)

Theo cách hiểu trên, hành động vẽ tự do bằng chuột có thể miêu tả như sau:
- Khi người dùng bấm chuột và chưa thả tay (mouse down), chúng ta lưu lại vị trí hiện tại và đặt biến drawing = true để xác định trạng thái bắt đầu vẽ.
- Người dùng đang giữ chuột, di chuột qua vị trí khác (mouse move), ta vẽ liên tục các đường thẳng từ vị trí cũ đến vị trí mới.
- Khi người dùng thả tay (mouse up) đặt biến drawing = false để không tiếp tục vẽ nữa.

Các bạn có thể xem video để hiểu cách làm, video này mình viết tất cả từ đầu trong khoảng 1 tiếng live stream. Toàn bộ code trong video bạn có thể download tại đây

<div class="youtube">
<iframe width="560" height="315" src="https://www.youtube.com/embed/pDSxzvyJ6k8" frameborder="0" allowfullscreen></iframe>
</div>

Đầu tiên chúng ta tạo một object đại diện cho bảng vẽ với các thuộc tính cơ bản, tạo canvas và append nó vào body.

```javascript
var draw = function(){
    this.canvas    = null;
    this.context   = null;
    this.width     = 700;
    this.height    = 500;
    this.x         = 0;
    this.y         = 0;
    this.drawing   = false;
    this.lineWidth = 3;
    this.color     = "#000000"; // mặc định là màu đen

    var self = this;

    this.init = function(){
        this.canvas        = document.createElement('canvas');
        this.context       = this.canvas.getContext('2d');
        this.canvas.width  = this.width;
        this.canvas.height = this.height;

        document.body.appendChild(this.canvas);
    }
}
```

Sau đó chúng ta tạo nền cho canvas bằng cách vẽ một hình chữ nhật màu trắng bao phủ toàn bộ canvas:

```javascript
this.drawWhiteBackground = function(){
    this.context.fillStyle = "#ffffff";
    this.context.fillRect(0, 0, this.width, this.height);
}
```

Như đã nói ở trên, đường vẽ tự do là tập hợp của các đường thẳng, do đó chúng ta sẽ viết hàm vẽ đường thẳng từ vị trí (startX, startY) đến vị trí (endX, endY) bất kỳ:

```javascript
this.drawLine = function(startX, startY, endX, endY){
    this.context.beginPath();
    this.context.moveTo(startX, startY);
    this.context.lineTo(endX, endY);
    this.context.lineWidth = this.lineWidth;
    this.context.strokeStyle = this.color;
    this.context.stroke();
}
```

Tiếp tục viết hàm lấy vị trí của con trỏ chuột, hàm này sẽ trả về một object chứa thông tin vị trí x và y hiện tại của con trỏ chuột vào thời điểm sảy ra sự kiện event:

```javascript
this.getMousePosition = function(event){
    var rect = this.canvas.getBoundingClientRect();
    return {
        x: event.clientX - rect.left,
        y: event.clientY - rect.top
    }
}
```

Bắt các sự kiện chuột: mouse down, mouse up và mouse move để thực hiện các hàm xử lý tương ứng:

```javascript
this.canvas.addEventListener('mousedown', function(event){
    self.proccessMouseDown(event);
});
this.canvas.addEventListener('mouseup', function(event){
    self.proccessMouseUp(event);
});
this.canvas.addEventListener('mousemove', function(event){
    self.proccessMouseMove(event);
});
```

Với sự kiện mouse down, chúng ta lưu vị trí hiện tại và đặt biến drawing = true

```javascript
this.processMouseDown = function(event){
    var position = this.getMousePosition(event);
    this.x = position.x;
    this.y = position.y;
    this.drawing = true; // bấm chuột xuống thì bắt đầu vẽ
}
```

Ngược lại với mouse down, khi người dùng mouse up, chúng ta đặt biến drawing = false để xác định người dùng đã thôi vẽ.

```javascript
this.proccessMouseUp = function(event){
    this.drawing = false;
}
```

Khi người dùng di chuyển chuột (mouse move) nếu drawing == true, tức là chưa nhả chuột ra, thì chúng ta sẽ vẽ liên tiếp các đường thẳng từ vị trí cũ đến vị trí mới, và cập nhật vị trí mới cho nó.

```javascript
this.proccessMouseMove = function(event){
    if (this.drawing){
        var newPos = this.getMousePosition(event);
        this.drawLine(this.x, this.y, newPos.x, newPos.y, 2, '#000000');
        this.x = newPos.x;
        this.y = newPos.y;
    }
}
```

Đến đây, bạn đã tạo được hiệu ứng vẽ tự do trên nền web, trong video, mình còn làm thêm phần chọn màu nét vẽ, bạn có thể download code về xem để tìm hiểu thêm.
