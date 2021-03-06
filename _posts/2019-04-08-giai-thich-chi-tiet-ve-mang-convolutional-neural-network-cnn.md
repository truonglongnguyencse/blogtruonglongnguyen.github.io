---
layout: post
title: Giải thích chi tiết về mạng Convolutional Neural Network (CNN)
description: Mạng Convolutional Neural Network (CNN) có kiến trúc khá giống một mạng nơ-ron truyền thẳng thông thường, bao gồm các nơ-ron có khả năng tự tối ưu hóa thông qua quá trình huấn luyện.
excerpt: Đối với một số loại dữ liệu, đặc biệt là dữ liệu ở dạng hình ảnh, mạng nơ-ron truyền thẳng nhiều lớp tỏ ra không hiệu quả để đáp ứng xử lý tốt. Để áp dụng mạng nơ-ron truyền thẳng nhiều lớp cho việc xử lý các dữ liệu ở dạng hình ảnh, chúng ta cần phải chuyển đổi được hình ảnh về dưới dạng vector.
keywords: mạng tích chập cnn, mạng cnn, Convolutional Neural Network, mạng Convolutional Neural Network, mạng nơ-ron tích chập CNN, mạng nơ-ron tích chập, mạng tích chập
author: Nguyễn Trường Long
---

[Mạng nơ-ron tích chập (Convolutional Neural Networks - CNN)](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-convolutional-neural-network-cnn.html) là một loại mạng neural network đã đạt được nhiều thành tựu trong các bài toán có liên quan đến hình ảnh như nhận dạng hình ảnh (image recognition) và phân lớp hình ảnh (image classification) hiện nay. Ngoài ra, [mạng CNN](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-convolutional-neural-network-cnn.html) còn được ứng dụng trong các bài toán xử lý ngôn tự nhiên (natural language processing) như phát hiện thư rác (spam detection), phân loại văn bản (topic categorization),...

Các mạng nơ-ron truyền thẳng nhiều lớp nhiều lớp (multilayer perceptron) chỉ được xây dựng để nhận dữ liệu đầu vào dưới dạng vector. Đối với một số loại dữ liệu, đặc biệt là dữ liệu ở dạng hình ảnh, mạng nơ-ron truyền thẳng nhiều lớp tỏ ra không hiệu quả để đáp ứng xử lý tốt. Để áp dụng mạng nơ-ron truyền thẳng nhiều lớp cho việc xử lý các dữ liệu ở dạng hình ảnh, chúng ta cần phải chuyển đổi được hình ảnh về dưới dạng vector. Điều này thường gây ra sự mất mát nhiều thông tin trong dữ liệu gốc ban đầu. [Mạng CNN](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-convolutional-neural-network-cnn.html) được giới thiệu bởi LeCun đã lược bỏ công việc trích xuất các đặc trưng một cách thủ công.

[Mạng CNN](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-convolutional-neural-network-cnn.html) được có kiến trúc được cấu tạo bởi một số loại layer bao gồm:
- Convolutional layer
- Pooling layer
- Fully connected layer

<figure class="image">
  <img src="https://nguyentruonglong.net/images/CompleteCNNArchitecture.png" alt="Kiến trúc tổng quát của một Convolutional Neural Network">
  <figcaption><center><i>Kiến trúc tổng quát của một Convolutional Neural Network. Nguồn: Nikhil Ketkar</i></center></figcaption>
</figure>

### Phép tích chập (convolution operation)

Để đào sâu và hiểu rõ hơn về mạng [mạng nơ-ron tích chập](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-convolutional-neural-network-cnn.html), chúng ta cần lướt qua một chút về các kiến thức toán học có liên quan đến phép tích chập. Chúng ta có thể hình dung một cách đơn giản rằng ý nghĩa của phép tích chập giống như một hoạt động trộn thông tin lại với nhau. Phép tích chập được ứng dụng tương đối rộng rãi trong nhiều ngành khoa học và kỹ thuật khác nhau.

Trong toán học, phép tích chập giữa hai hàm $f$ và $g$ sẽ tạo ra một hàm thứ ba biểu diễn sự biến đổi của của một hàm đối với hàm còn lại. Xét hai hàm $f$ và $g$, phép tích chập giữa hai hàm này được định nghĩa như sau:

{% raw %}
$$h\left( x \right) = f \otimes g = \int\limits_{ - \infty }^\infty  {f\left( {x - u} \right)} g\left( u \right)du = {F^{ - 1}}\left( {\sqrt {2\pi } F\left[ f \right]F\left[ g \right]} \right)$$
{% endraw %}

{% raw %}
$$\begin{array}{l}
{\rm{feuture map}} &= input \otimes kernel\\
&= \sum\limits_{y = 0}^{columns} {\left( {\sum\limits_{x = 0}^{rows} {input\left( {x - a,y - b} \right){\rm{kernel}}\left( {x,y} \right)} } \right)} \\
&= {F^{ - 1}}\left( {\sqrt {2\pi } F\left[ {input} \right]F\left[ {{\rm{kernel}}} \right]} \right)
\end{array}$$
{% endraw %}

<figure class="image">
  <img src="https://nguyentruonglong.net/images/ConvolutionKernel.png" alt="Ví dụ về một hình ảnh 2D đầu vào của mặt trời được tích chập với một kernel">
  <figcaption><center><i>Ví dụ về một hình ảnh 2D đầu vào của mặt trời được tích chập với một kernel. Một bản đồ đặc trưng (feature map) có kích thước (N - 2) x (N - 2) là kết quả được tạo ra từ phép tích chập này. Nguồn: Carlos José Díaz Baso</i></center></figcaption>
</figure>

Chúng ta xem xét trong không gian một chiều, phép tích chập giữa hai hàm $f$ và $g$ được mô tả bởi phương trình sau:

{% raw %}
$$\left( {f * g} \right)\left( x \right) = \sum\limits_t {f\left( t \right)} g\left( {x + t} \right)$$
{% endraw %}

Đối với dữ liệu đầu vào 2 chiều như hình ảnh, chúng ta có hai đầu vào cho phép tích chập. Đầu vào thứ nhất là một hình ảnh 2D, đầu vào còn lại được gọi là kernel hoặc mask hoạt động giống như bộ lọc (filter) cho hình ảnh 2D đầu vào và tạo ra một hình ảnh khác cho đầu ra. Chúng ta xem xét cụ thể một 2D-convolution sau:

{% raw %}
$$\left( {K * I} \right)\left( {i,j} \right) = \sum\limits_{m,n} {K\left( {m,n} \right)} I\left( {i + n,j + m} \right)$$
{% endraw %}

<figure class="image">
  <img src="https://nguyentruonglong.net/images/2DConvolution.png" alt="Ví dụ minh họa về 2D-Convolution">
  <figcaption><center><i>Một ví dụ minh họa về 2D-Convolution. Nguồn: Ian Goodfellow</i></center></figcaption>
</figure>

### Convolutional Layer

### Pooling Layer

Chức năng chung của pooling layer là giảm kích thước không gian của đặc trưng với mục đích chính là giảm số lượng tham số và khối lượng tính toán trong network. Pooling layer hoạt động trên từng feuture map độc lập với nhau. Hướng tiếp cận phổ biến nhất được sử dụng là max pooling.

<figure class="image">
  <img src="https://nguyentruonglong.net/images/PoolingSchematic.gif" alt="Ví dụ minh họa cho thấy pooling đang hoạt động trên 4 vùng không chồng chéo nhau của hình ảnh">
  <figcaption><center><i>Ví dụ minh họa cho thấy pooling đang hoạt động trên 4 vùng không chồng chéo nhau của hình ảnh. Nguồn: UFLDL Tutorial</i></center></figcaption>
</figure>


(Bài viết đang trong quá trình hoàn thiện)
