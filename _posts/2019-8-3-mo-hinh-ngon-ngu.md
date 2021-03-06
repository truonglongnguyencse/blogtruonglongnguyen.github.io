---
layout: post
title: Mô hình ngôn ngữ (language model)
description: Mô hình ngôn ngữ là mô hình mà sẽ tính toán phân phối xác suất của một chuỗi các token trong các ngôn ngữ tự nhiên của con người.
excerpt: Mô hình ngôn ngữ là mô hình mà tính toán phân phối xác suất của một chuỗi các token trong ngôn ngữ tự nhiên và có nghĩa là mô hình cho phép dự đoán khả năng xuất hiện của chuỗi token này trong ngôn ngữ của nó. Tùy thuộc vào cách thức mô hình được thiết kế, các token này có thể là các từ, các ký tự hoặc thậm chí là các byte.
keywords: mô hình ngôn ngữ, language model, xử lý ngôn ngữ tự nhiên, mô hình ngôn ngữ n-grams
author: Nguyễn Trường Long
---

[Mô hình ngôn ngữ](https://nguyentruonglong.net/mo-hinh-ngon-ngu.html) là mô hình mà tính toán phân phối xác suất của một chuỗi các token trong ngôn ngữ tự nhiên {% raw %}
$$P\left( {{w_1},{w_2},{w_3},...,{w_\tau }} \right)$${% endraw %}. Điều này có nghĩa là mô hình cho phép dự đoán khả năng xuất hiện của chuỗi token này trong ngôn ngữ của nó. Tùy thuộc vào cách thức mô hình được thiết kế, các token này có thể là các từ, các ký tự hoặc thậm chí là các byte. Để tính xác suất của một chuỗi các token liên tiếp, chúng ta áp dụng quy tắc xác suất dây chuyền (chain rule of probability) tổng quát để phân tách như sau:
{% raw %}
$$\begin{align}
	P\left( {{w_1},{w_2},{w_3},...,{w_\tau }} \right) = P\left( {{w_1}} \right)P\left( {{w_2}|{w_1}} \right)P\left( {{w_3}|{w_1},{w_2}} \right)...P\left( {{w_\tau }|{w_1},...,{w_{\tau  - 1}}} \right)
\end{align}$$
{% endraw %}

Quy tắc dây chuyền này cho chúng ta thấy được mối liên hệ giữa xác suất của một chuỗi các token và xác suất của một token đối với các token đứng trước nó. Nhưng trong thực tế, quy tắc dây chuyền này tỏ ra không hữu ích vì chúng ta không thể nào có thể tính hết được tất cả các xác suất của một token được cho trước bởi các chuỗi token dài liên tiếp.

Một ý tưởng từ mô hình n-grams là thay vì sử dụng cách phân tích bằng quy tắc dây chuyền như trên, chúng ta có thể tính bằng xấp xỉ Markov bậc $n$:
{% raw %}
$$\begin{align}
	P\left( {{w_t }|{w_1},...,{w_{t  - 1}}} \right) \approx P\left( {{w_t }|{w_{t  - n}},{w_{t  - \left( {n - 1} \right)}},...,{w_{t  - 2}},{w_{t  - 1}}} \right)
\end{align}$$
{% endraw %}

Điều này có nghĩa là xác suất xuất hiện tiếp theo của token {% raw %}$${{w_t }}$${% endraw %} với chuỗi token cho trước {% raw %}
$${{w_1},{w_2},...,{w_{t  - 1}}}$${% endraw %} chỉ phụ thuộc vào $n$ token đứng liền trước nó với $n$ vừa đủ nhỏ $\left( {n < t } \right)$ thay vì toàn bộ chuỗi token {% raw %}$${{w_1},{w_2},...,{w_{t  - 1}}}$${% endraw %}. Do đó phân phối xác suất của chuỗi {% raw %}$$\left( {{w_1},{w_2},...,{w_\tau }} \right)$${% endraw %} sẽ được tính bằng công thức:
{% raw %}
$$\begin{align}
	P\left( {{w_1},{w_2},...,{w_\tau }} \right) \approx \prod\limits_{t = 1}^\tau  {P\left( {{w_t}|{w_{t - \left( {n - 1} \right)}},...,{w_{t - 2}},{w_{t - 1}}} \right)}
\end{align}$$
{% endraw %}

Dựa vào công thức trên, chúng ta có thể xây dựng mô hình ngôn ngữ n-grams bằng cách thống kê các chuỗi có ít hơn $n+1$ token liên tiếp trong kho ngữ liệu văn bản lớn theo công thức ước lượng hợp lý cực đại (maximum likelihood estimation):
{% raw %}
$$\begin{align}
	P\left( {{w_t}|{w_{t - \left( {n - 1} \right)}},...,{w_{t - 2}},{w_{t - 1}}} \right) = \frac{{C\left( {{w_{t - \left( {n - 1} \right)}},...,{w_{t - 2}},{w_{t - 1}},{w_t}} \right)}}{{C\left( {{w_{t - \left( {n - 1} \right)}},...,{w_{t - 2}},{w_{t - 1}}} \right)}}
\end{align}$$
{% endraw %}
