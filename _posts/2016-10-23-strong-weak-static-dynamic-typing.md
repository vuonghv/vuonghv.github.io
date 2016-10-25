---
layout: post
title: "Strong vs Weak, Static vs Dynamic typing là cái khỉ gì?"
date:   2016-10-23 10:36:13 +0700
category: blog
tags: ["python", "programming"]
---

Trên con đường đến với đạo lập trình, chắc các bạn cũng từng nghe đến các khái
niệm như `strong/weak` typing, `static/dynamic` typing. Bạn có bao giờ thắc mắc
chúng có nghĩa là gì? và các ngôn ngữ thông dụng như Java, C/C++, Python,
Javascript, ... là strong hay weak typing? static hay dynamic typing?

## Strong vs Weak typing

Hiện tại thì người ta vẫn chưa thống nhất một _định nghĩa chuẩn_ thế nào là một
ngôn ngữ strong typing hay weak typing. Và đây cũng là một chủ đề gây ra rất
nhiều tranh luận mỗi khi có ai đó nêu ra. Ở đây tôi muốn nêu ra khái niệm được
nhiều người chấp nhận và theo tôi thấy thì cũng ngắn gọn và dễ hiểu nhất:

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

Nếu không quá khắt khe thì ta có thể coi Python là ngôn ngữ strong typing, bởi
vì Python vẫn có một số ngoại lệ, ví dụ như biểu thức `1.0 + 2` sẽ cho ra giá
trị là số thực `3.0` (số nguyên `2` đã tự động chuyển sang kiểu số thực).

Với strong typing, chương trình của chúng ta sẽ rõ ràng, dễ debug và kiểm soát
hơn so với weak typing. Bất cứ khi nào ta thực hiện một thao tác với các đối
tượng có kiểu không tương thích nhau, chương trình sẽ xuất ra một thông báo
lỗi sai kiểu (chẳng hạn `TypeError` exception trong Python). Chúng ta không
cần phải nhớ một đống quy tắc tự động chuyển đổi kiểu trong các phép toán cơ
bản ( ví dụ như, khi nào thì string sẽ tự động chuyển sang kiểu số, và ngược
lại, ...) và hơn nữa, rất khó để debug khi biến _âm thầm_ đổi kiểu mà
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

Tuy rằng có thể gán các object có kiểu khác nhau cho cùng một biến trong các
ngôn ngữ dynamic typing nhưng việc đấy được xem như _bad practice_ trong coding.
Bởi vì việc thay đổi kiểu của biến tùy tiện sẽ làm cho code của chương trình rất
khó đọc và khó debug.

_Nghe cũng thú vị đấy, nói nghe ưu nhược điểm của từng loại xem nào?_

Dưới đây là một vài tiêu chí so sánh ưu nhược điểm của static và dynamic typing:

* **Ngắn gọn**: Với dynamic typing, code trông sẽ ngắn gọn hơn bởi vì nó bỏ đi
các khai báo kiểu cho biến, tham số cũng như giá trị trả về của hàm.

* **Tài liệu**: Với tiêu chí này thì static typing lại chiếm ưu thế hơn, khi
khai báo kiểu cho biến, tham số,... bản thân nó cũng đã phục vụ như bản đặc tả
tài liệu. Hơn nữa static typing giúp tính năng _intelligent completion_ trong
IDE làm việc tốt hơn. Gần đây Python (version 3.5) có [type hints][4] và
Microsoft đẻ ra thằng [typescript][5] cũng có một phần vì lý do này.

* **Tính đúng đắn**: Trong một ngôn ngữ static typing, những lỗi về kiểu (type
errors) có thể được phát hiện tại thời điểm compile vì vậy chương trình sẽ an
toàn và ít lỗi hơn so với dynamic typing, do lỗi về kiểu chỉ có thể phát hiện lúc
chạy chương trình.

* **Hiệu năng**: Trong ngôn ngữ dynamic typing, do phải mất chi phí để kiểm tra 
kiểu lúc runtime nên hiệu năng sẽ giảm đi đáng kể. Trái lại, static typing cho
phép compiler thực hiện một số tối ưu lúc biên dịch chương trình do kiểu của
biến đã được khai báo trước.

Hy vọng bài viết cung cấp cho bạn những thông tin hữu ích.

Nguồn tham khảo:

1. [Why is Python a dynamic language and also a strongly typed language][1]
2. [Is Python strongly typed?][2]
3. [The difference between a strongly and a statically typed language?][3]

[1]: https://wiki.python.org/moin/Why%20is%20Python%20a%20dynamic%20language%20and%20also%20a%20strongly%20typed%20language
[2]: http://stackoverflow.com/a/11328980/5514109
[3]: http://stackoverflow.com/a/2690593/5514109
[4]: https://www.python.org/dev/peps/pep-0484/
[5]: https://www.typescriptlang.org/

\_EOF\_
