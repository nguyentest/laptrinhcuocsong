---
layout: post
title: Giới thiệu fluent interface - một cách để code dễ đọc hơn
thumbnail: hour-of-code.jpg
category: Chuyện lập trình
---
Fluent interface được đặt ra bởi Eric Evans và Martin Fowler, là sự mở rộng của kỹ thuật "Lời gọi theo chuỗi" (method chaining) nhằm làm cho mã lập trình dễ đọc hơn. Method chaining là một kỹ thuật về cú pháp chung cho cách gọi nhiều lần tới các hàm khác trong lập trình hướng đối tượng.

Cái đống bùi nhùi ở trên là lý thuyết rất là hàn lâm và khó hiểu. Để dễ hiểu hơn chúng ta sẽ đi thẳng vào ví dụ cho nó trực quan. Chắc hẳn các bạn đã từng thấy đâu đó những đoạn code rất đẹp đẽ kiểu như thế này:

```javascript
$person->setName('Tùng')
       ->setAge(20)
       ->showInfo();
```

Hoặc thân thuộc nhất là trong jquery:

```javascript
$('#element').first()
             .slideDown()
             .remove();
```

Như các bạn thấy, các hàm của một đối tượng được gọi một cách liên tục, làm cho code dễ đọc dễ hiểu hơn rất nhiều. Vậy làm thế nào để được như vậy? Rất đơn giản, bạn chỉ cần trả về chính object hiện tại (`return this`) để sẵn sàng cho lời gọi tiếp theo. Cụ thể ở ví dụ đầu tiên, chúng ta sẽ viết như thế này:

```javascript
class Person
{
    public $name;
    public $age; 

    public function setName($name)
    {
        $this->name = $name;
        return $this;
    }

    public function setAge($age)
    {
        $this->age = $age;
        return $this;
    }

    public function showInfo()
    {
        echo 'Name: '.$this->name.', age: '.$this->age;
    }
}
$person = new Person();
$person->setName('Tùng')
       ->setAge(20)
       ->showInfo();
```

Đến đây mọi chuyện đã sáng tỏ, chẳng có gì cao siêu ở đây cả, sau đây mình sẽ giới thiệu 3 đặc điểm của fluent interface:

**Đặc điểm 1**: Định nghĩa thông qua việc trả về một đối tượng object là chính nó, chính là cái `return this` mà mình nói ở trên.

**Đặc điểm 2**: Kết quả trả về của một chuỗi lời gọi hàm là kết quả trả về của hàm cuối cùng.

```javascript
$name = $person->setName('Tùng')->setAge(20)->getName();
```

**Đặc điểm 3**: Kết thúc khi gặp hàm không trả về:

```javascript
$person->setName(); // kết thúc
```

Thực sự nó rất đơn giản và đang được sử dụng rộng rãi, nhưng mình vẫn muốn viết ra, hi vọng giúp được gì đó cho các bạn, đặc biệt các bạn mới học.





