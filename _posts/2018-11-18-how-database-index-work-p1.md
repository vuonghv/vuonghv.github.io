---
layout: post
title: "Database cài đặt index như thế nào? - Hash Indexes (phần 1)"
date: 2018-11-18 21:25:34 +0700
category: blog
tags: ["algorithm", "database"]
---

Nếu đã có kinh nghiệm làm việc với Database thì bạn hẳn đã biết rằng đánh chỉ mục (index) sẽ tối ưu hiệu năng truy vấn. Vậy có bao giờ bạn thắc mắc hệ quản trị Database cài đặt index hoặc lưu trữ dữ liệu như thế nào chưa? Các cấu trúc dữ liệu nào được Database sử dụng để phục vụ công việc của mình?

Trong series này, mình sẽ nói về cách các storage engines lưu trữ và xử lý dữ liệu cũng như các index thông dụng.

Giả sử ta cần cài đặt:

{% gist a71eb60227d75ffcd2f6b732122c25a1 %}