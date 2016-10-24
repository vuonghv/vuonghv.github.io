---
layout: post
title: "Strong vs Weak, Static vs Dynamic typing là cái khỉ gì?"
date:   2016-10-23 10:36:13 +0700
category: blog
tags: ["python", "programming"]
---

Khi lập trình, chắc các bạn cũng từng nghe đến các khái niệm như `strong/weak`
typing, `static/dynamic` typing. Bạn có bao giờ thắc mắc chũng có nghĩa là gì?
và các ngôn ngữ như `Java`, `C/C++`, `Python`, `Javascript`, ... là strong hay
weak typing? static hay dynamic typing?

## Strong vs Weak typing
Hiện tại thì vẫn chưa có một _định nghĩa chuẩn_ thế nào là một ngôn ngữ strong
typing. Ở đây tôi muốn nêu ra khái niệm được nhiều người chấp nhận:

> Strong typing means that the type of a value doesn't **suddenly** change.

Theo đó, các ngôn ngữ **strong typing** đảm bảo rằng kiểu (types) của một object
không thay đổi một cách bất ngờ, không tường minh. Hay nói cách khác, ta phải
chỉ rõ tường minh khi muốn chuyển đổi kiểu của một object.

Những ngôn ngữ không đáp ứng yêu cầu trên là **weak typing**. Nói nhiều quá, lấy
một số ví dụ cho dễ hiểu nào:

Xét đoạn code PHP sau:

```php?start_inline=1
$a = "3" + "5"; // $a == 8
$b = 101 . " dogs"; // $b == "101 dogs"
```

Ta thấy ở câu lệnh trên, kiểu của string `"3"` và `"5"` đã tự động chuyển thành
số nguyên `3` và `5`, dẫn đến giá trị của biến `$a` là `8`. Tương tự, số nguyên
`101` đã ngầm định chuyển thành string `"101"`. Do đó PHP là một ngôn ngữ weak
typing.

Tương tự, Javascript cũng là ngôn ngữ weak typing:

```javascript
let a = "abc" + 123; // 123 is implicitly converted to string "123"
console.log(a); // "abc123"
```

Trái lại, ta cùng xem đoạn code Python dưới đây:

```python
>>> "abc" + 3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't convert 'int' object to str implicitly
>>> "abc" + str(3)
'abc3'
```

Ta thấy rằng, khi cố gắng thực hiện phép toán cộng giữa một object string và một
số nguyên, trình thông dịch Python sẽ thông báo lỗi `TypeError` bởi vì ta không
được phép _ngầm định_ chuyển đổi object kiểu int sang kiểu string. Thay vào đó,
ta phải chỉ rõ _tưòng minh_ thao tác chuyển đổi kiểu thông qua hàm `str()`.

Nếu không quá khắt khe thì ta có thể coi Python là ngôn ngữ strong typing, bởi vì
Python vẫn có một số ngoại lệ, ví dụ như biểu thức `1.0 + 2` sẽ cho ra giá trị
là số thực `3.0` (số nguyên `2` đã tự động chuyển sang kiểu số thực).

Với strong typing, chương trình của chúng ta sẽ rõ ràng, dễ debug và kiểm soát
hơn so với weak typing. Bất cứ khi nào ta thực hiện một thao tác với các đối
tượng có kiểu không tương thích nhau, chương trình sẽ xuất ra một thông báo
lỗi sai kiểu (chẳng hạn `TypeError` exception trong Python). Chúng ta không
cần phải nhớ một đống quy tắc tự động chuyển đổi kiểu trong các phép toán cơ
bản ( ví dụ như, khi nào thì string sẽ tự động chuyển sang kiểu số, và ngưọc
lại, ...) và hơn nữa, quả thật rất khó để debug khi biến _âm thầm_ đổi kiểu mà
ta không biết.

## Static vs Dynamic typing

Trong các ngôn ngữ **static typing** (C/C++, Java), mỗi biến (_variable_) có một
kiểu cố định liên kết với nó. Kiểu của biến được kiểm tra lúc **compiled-time**
và trình biên dịch yêu cầu ta phải khai báo rõ kiểu của biến trước khi sử dụng.

Ví dụ về khai báo biến trong C:

```c
int a;  // the type of a is integer
a = 3;  // OK, assign 3 to a
a = "Hello"; // Error, cannot assign string value to int
```

Nếu ta đã khai báo một biến có kiểu nguyên, ta sẽ không thể gán các giá trị có
kiểu khác tới nó.

Trái lại, với **dynamic typing**, mỗi biến chỉ đơn giản là một cái nhãn (label)
được liên kết với một object. Mỗi object sẽ có kiển riêng của nó (ví dụ trong
Python, ta có kiểu `int, str, list, dict, ...`) nhưng bản thân biến thì không.
Và kiểu của biến hay nói chính xác hơn là kiểu của object liên kết với biến được
kiểm tra lúc **runtime**.

Dynamic typing trong Python:

```python
b = 3   # variable b is bound to integer object
isinstance(b, int)  # True

b = 'hello world!'   # Now b is bound to string object
isinstance(b, str)   # True

b = ['blue', 'black', 'brown'] # Now b is a list
```

Hy vọng bài viết cung cấp cho bạn những thông tin hữu ích.

\_EOF\_
