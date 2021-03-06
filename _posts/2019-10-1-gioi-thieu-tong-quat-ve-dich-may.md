---
layout: post
title: Giới thiệu tổng quát về dịch máy
description: Dịch máy hay còn được gọi là dịch tự động có thể được định nghĩa như một lĩnh vực nghiên cứu việc sử dụng phần mềm máy tính để dịch văn bản hoặc lời nói từ ngôn ngữ tự nhiên này sang ngôn ngữ tự nhiên khác.
excerpt: Các ý tưởng về dịch máy manh nha bắt đầu xuất hiện vào thế kỷ 17. Năm 1629, René Descartes đã đề xuất lý thuyết về một ngôn ngữ tổng quát (universal language) mô tả tất cả những ý tưởng và khái niệm tương đương nhau trong các ngôn ngữ khác nhau. Tuy nhiên, mãi cho đến thế kỷ 20, những ý tưởng cụ thể đầu tiên về dịch máy mới bắt đầu được công nhận.
keywords: dịch máy, dịch tự động, machine translation, giới thiệu tổng quát về dịch máy, xử lý ngôn ngữ tự nhiên, BLEU, lịch sử dịch máy
author: Nguyễn Trường Long
---

### Giới thiệu

Dịch máy (machine translation) hay còn được gọi là dịch tự động có thể được định nghĩa như một lĩnh vực nhỏ của ngành ngôn ngữ tính toán (computational linguistics) mà nghiên cứu việc sử dụng phần mềm máy tính để dịch văn bản hoặc lời nói từ ngôn ngữ tự nhiên này sang ngôn ngữ tự nhiên khác. Đây là một lĩnh vực sử dụng kết hợp nhiều ý tưởng và các kỹ thuật với nhau từ ngôn ngữ học, khoa học máy tính, xác suất thống kê và trí tuệ nhân tạo. Mục tiêu của dịch máy là phát triển một hệ thống cho phép tạo ra bản dịch chính xác giữa các ngôn ngữ tự nhiên của con người.

### Lịch sử phát triển của dịch máy

Các ý tưởng về dịch máy manh nha bắt đầu xuất hiện vào thế kỷ 17. Năm 1629, René Descartes đã đề xuất lý thuyết về một ngôn ngữ tổng quát (universal language) mô tả tất cả những ý tưởng và khái niệm tương đương nhau trong các ngôn ngữ khác nhau. Tuy nhiên, mãi cho đến thế kỷ 20, những ý tưởng cụ thể đầu tiên về dịch máy mới bắt đầu được công nhận. Cả hai người là George Artsrouni và Petr Petrovich Troyanskii đều được cấp bằng sáng chế cho các phát minh độc lập với nhau vào năm 1933. Artsrouni đã tạo ra một thiết bị lưu trữ trên băng giấy có thể dùng để tra nghĩa của bất kỳ từ nào trong ngôn ngữ khác. Trong khi đó, nhà khoa học Troyanskii đã phát minh ra một từ điển cơ khí (mechanized dictionary) cho phép dịch từ ngôn ngữ này sang ngôn ngữ khác, nhưng nó bị xem là "vô giá trị" và người ta nhanh chóng lãng quên cho tới khi hai nhà khoa học Liên Xô khác đã tìm thấy bằng sáng chế của ông vào 1956.

Những đề xuất đầu tiên về khả năng sử dụng máy tính để thực hiện một chương trình dịch tự động đã được thảo luận bởi Warren Weaver và nhà tinh thể học người Anh là Andrew D.Booth. Ý tưởng này dựa trên lý thuyết thông tin, sự thành công trong việc phá vỡ mật mã Enigma trong Chiến tranh Thế giới thứ hai và sự suy đoán các nguyên tắc nền tảng tổng quát (speculation about universal underlying principles) của ngôn ngữ tự nhiên.

Năm 1954, công ty IBM và trường đại học Georgetown đã hợp tác xây dựng một hệ thống dịch Nga-Anh tuy còn nhiều hạn chế nhưng kết quả đạt được đã thu hút sự quan tâm của công chúng và các nhà tài trợ từ chính phủ. Ở Liên Xô, những nghiên cứu về dịch máy cũng diễn ra mạnh mẽ như tại Hoa Kỳ. Các thử nghiệm về hệ thống dịch Anh-Nga dựa trên những cách tiếp cận tương tự như hệ thống dịch máy Georgetown-IBM nhưng đạt được ít thành công hơn.

Tuy nhiên vào năm 1960, nhà ngôn ngữ học Bar-Hillel đã chỉ ra những rào cản của dịch máy ở thời điểm hiện tại và đưa ra kiến nghị rằng dịch máy chỉ nên được áp dụng cho các mục tiêu với phạm vi hẹp. Năm 1964, những nhà tài trợ cho các nghiên cứu về dịch máy tại Hoa Kỳ đã thành lập Automatic Language Processing Advisory Committee (ALPAC) để kiểm tra triển vọng của dịch máy. Trong báo cáo diễn ra vào năm 1966, kết luận đưa ra cho thấy rằng dịch máy tỏ ra chậm chạp, kém chính xác, tốn chi phí gấp đôi so với dịch thuật từ con người và tỏ ra không có triển vọng. Báo cáo khuyến nghị rằng không nên tiếp tục đầu tư vào nghiên cứu dịch máy và thay vào đó nên đầu tư phát triển các công cụ hỗ trợ cho người dịch chẳng hạn như từ điển tự động và tiếp tục hỗ trợ các nghiên cứu cơ bản trong ngôn ngữ học tính toán. Do đó mà các hoạt động nghiên cứu về dịch máy trong giai đoạn này tạm thời diễn ra chậm lại.

Ở giai đoạn trong những năm 1970 trở về sau, do quá trình toàn cầu hóa bắt đầu diễn ra, các nhu cầu về một hệ thống với chi phí thấp có thể dịch một loạt các tài liệu kỹ thuật và thương mại được thúc đẩy gia tăng. Đến năm 1980, các hệ thống dịch máy thương mại bắt đầu xuất hiện ngày càng đa dạng như SYSTRAN, AS-TRANSAC, METAL, ALPS,... Các hướng nghiên cứu đột phá về mặt lý thuyết trong dịch máy được ra đời tạo thêm nhiều triển vọng lớn đối với dịch máy.

### Các hướng tiếp cận trong dịch máy

Có nhiều tiêu chí và cách thức để phân loại các hệ thống dịch máy khác nhau từ nhiều nhà nghiên cứu. Nhưng trong phạm vi của bài viết này mình sẽ phân chia các hệ thống dịch máy theo ba hướng tiếp cận chính là:

- *Dịch máy dựa trên luật (Rule-based Machine Translation - RBMT)*: Hướng tiếp cận này còn được biết đến với tên gọi dịch máy dựa trên kiến thức (Knowledge-based Machine Translation - KBMT), là tên gọi chung cho một nhóm các hệ thống dịch máy hoạt động dựa trên các thông tin về ngôn ngữ học giữa ngôn ngữ nguồn và ngôn ngữ đích. Các hệ thống dịch máy dựa trên hướng tiếp cận này hoạt động theo nguyên tắc chung là nhận các văn bản đầu vào ở ngôn ngữ nguồn và tạo thành các văn bản đầu ra ở ngôn ngữ đích dựa trên việc phân tích hình thái (morphological), cú pháp (syntactic) và ngữ nghĩa (semantic).
	
- *Dịch máy dựa trên kho ngữ liệu (Corpus-based Machine Translation - CBMT)*: Theo hướng tiếp cận này, quá trình tạo ra bản dịch được thực hiện dựa trên các tri thức được trích xuất tự động thông qua việc phân tích các văn bản song ngữ đạt tiêu chuẩn do con người xây dựng. Kho ngữ liệu chứa càng nhiều mẫu ví dụ thì chất lượng của bản dịch càng được cải thiện tốt hơn. Nhưng chính vì thế mà việc thu thập và quản lý kho ngữ liệu cũng trở nên phức tạp và tốn kém chi phí, tài nguyên cho hệ thống cũng phải đủ lớn để đáp ứng yêu cầu.
	
- *Dịch máy kết hợp (Hybrid Machine Translation - HMT)*: Trên thực tế, các hệ thống dịch máy dựa trên mỗi hướng tiếp cận đơn lẻ trên đều tồn tại nhiều nhược điểm riêng. HMT ra đời dựa trên nguyên tắc kết hợp nhiều hướng tiếp cận dịch máy đơn lẻ lại để giải quyết những nhược điểm tồn tại ở mỗi hướng tiếp cận đơn lẻ này. Hiện nay, nhiều hệ thống HMT đã thành công trong việc cải thiện tốt hơn chất lượng của bản dịch.

### Phương pháp đánh giá các mô hình dịch máy

Hiện nay có nhiều hệ thống dịch máy khác nhau có thể dịch một văn bản từ ngôn ngữ này sang ngôn ngữ khác và ngày càng có nhiều mô hình lý thuyết về dịch máy được đề xuất. Tuy nhiên, chất lượng các bản dịch từ những hệ thống dịch máy là yếu tố được quan tâm nhiều hơn cả. Chúng ta cần phải đánh giá được hệ thống dịch máy nào tạo ra bản dịch tốt và đạt chất lượng cao để lựa chọn sử dụng. Việc đánh giá chất lượng này có thể được thực hiện thủ công thông qua con người hoặc được thực hiện một cách tự động.

Khi con người thực hiện đánh giá chất lượng một bản dịch, các yếu tố như tính lưu loát, tính đúng đắn và sự mạch lạc ngữ nghĩa của bản dịch đều được xem xét. Tuy nhiên, điều này có thể gây tốn kém nhiều thời gian, nguồn lực và chi phí khi số lượng các bản dịch cần đánh giá có số lượng lớn. Hơn nữa, cùng một người đánh giá một bản dịch cố định tại hai thời điểm khác nhau có thể cho ra hai kết quả đánh giá khác nhau. 

Tất cả những nhược điểm đã nêu ra đều cho thấy rằng để đánh giá và so sánh chất lượng bản dịch giữa các hệ thống dịch máy khác nhau một cách hiệu quả và khách quan cần phải sử dụng các thước đo được tính toán tự động, không phụ thuộc vào ngôn ngữ và có tương quan cao với con người.

### Thuật toán BLEU

Thuật toán BLEU được đề xuất trong một báo cáo nghiên cứu của IBM tại hội nghị ACL vào năm 2011. Ý tưởng chính của thuật toán BLEU đó là đánh giá chất lượng bản dịch từ đầu ra của hệ thống dịch máy thông qua việc so sánh nó với các bản dịch tham khảo có chất lượng tốt từ con người, bản dịch này càng giống với bản dịch của con người thì nó càng đạt chất lượng. Việc đánh giá các bản dịch sẽ dựa trên việc so sánh điểm số được tính bởi công thức sau đây:

{% raw %}
$$\begin{align}
BLEU = {\text{ BP}} \cdot \exp \left( {\sum\limits_{n = 1}^4 {{n^{ - 1}}{{\log }_e}{p_n}} } \right)
\end{align}$$
{% endraw %}

Trong đó:

- $ BP $ là chỉ số brevity penalty, bao gồm các tham số $c$ là tổng số lượng các từ trong bản dịch cần đánh giá (candidate translation) từ hệ thống dịch máy, $r$ là tổng số lượng các từ trong bản dịch tham khảo từ con người (reference translation) và được tính như sau:
	
  {% raw %}
  $$BP = \left\{ {\begin{array}{*{20}{c}}
      1&{if\,\,c > r}\\
      {{e^{\left( {1 - \frac{r}{c}} \right)}}}&{if\,\,c \le r}
      \end{array}} \right. $$
  {% endraw %}
- $ {p_n} $ là chỉ số modified n-gram precision, biểu diễn mức độ trùng khớp của văn bản cần đánh giá từ hệ thống dịch máy so với các bản dịch tham khảo từ con người, $ {p_n} $ được tính như sau:
	
  {% raw %}$$
  {p_n} = \frac{{\sum\limits_{C \in \left\{ {Candidates} \right\}} {\sum\limits_{n - gram \in C} {Coun{t_{clip}}\left( {n - gram} \right)} } }}{{\sum\limits_{C \in \left\{ {Candidates} \right\}} {\sum\limits_{n - gram \in C} {Count\left( {n - gram} \right)} } }}$$
  {% endraw %}
  Trong đó:
	- {% raw %}$$ {Coun{t_{clip}}\left( {n - gram} \right)} $${% endraw %} là số lượng các cụm có $n$ từ liên tiếp (n-gram) trùng nhau giữa bản dịch cần đánh giá (candidate translation) và các bản dịch tham khảo từ con người (reference translation).
	- {% raw %}$$ {Count\left( {n - gram} \right)} $${% endraw %} là số lượng các cụm có $n$ từ liên tiếp trong bản dịch từ hệ thống dịch máy.

Giá trị của BLEU luôn nằm trong khoảng từ $0$ đến $1$. Khi giá trị của BLEU càng gần $1$, điều này chỉ ra rằng bản dịch từ hệ thống dịch máy càng gần sát so với các bản dịch tham khảo. Với thiết kế đã được đưa ra, BLEU có thể đánh giá bản dịch từ đầu ra của hệ thống dịch máy so với nhiều bản dịch tham khảo tương đương về nghĩa từ con người trên các văn bản tài liệu rất lớn. Vì một văn bản ở ngôn ngữ nguồn có thể tồn tại nhiều bản dịch khác nhau ở ngôn ngữ đích nhưng đều tương đương với nhau về nghĩa nên việc bổ sung thêm nhiều bản dịch tham khảo có thể làm tăng giá trị của điểm BLEU. Mặc dù vậy, điểm BLEU cũng tồn tại một số nhược điểm. Nó không thể đánh giá được tính dễ hiểu (intelligibility) và tính đúng đắn ngữ pháp (grammatical correctness) của bản dịch giống như con người. Tuy nhiên, nó đã được chứng minh là một thước đo có tương quan hợp lý so với các đánh giá từ con người.
