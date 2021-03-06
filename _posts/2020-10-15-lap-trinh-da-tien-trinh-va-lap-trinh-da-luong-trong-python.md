---
layout: post
title: Lập trình đa tiến trình và lập trình đa luồng trong Python
description: Vấn đề đồng bộ hóa trong Python có thể được phân chia thành hai loại chính là đồng bộ hóa tài nguyên (resource synchronization) và đồng bộ hóa hoạt động (activity synchronization).
keywords: cơ chế đồng bộ trong Python, đồng bộ hóa trong Python, đồng bộ thread, đồng bộ tài nguyên, synchronization, đồng bộ trong Python, đồng bộ hoạt động, ngôn ngữ lập trình Python, đồng bộ các luồng, cơ chế đồng bộ, lập trình đa luồng, cơ chế lập trình đồng bộ
excerpt: Vấn đề đồng bộ hóa có thể được phân chia thành hai loại chính là đồng bộ hóa tài nguyên và đồng bộ hóa hoạt động. Trong khoa học máy tính, bài toán buổi ăn tối của các triết gia (Dining Philosophers Problem) thường được xem là ví dụ minh họa tốt nhất cho các vấn đề về đồng bộ hóa.
author: Nguyễn Trường Long
---

### Tiến trình (process), luồng (thread) và đồng bộ hóa (synchronization)

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/MultithreadingvsMultiprocessing.png" alt="Đa luồng và đa tiến trình trong Python">
  <figcaption>
	  <i>Đa luồng và đa tiến trình trong Python</i>
  </figcaption>
</center>
</figure>

#### <i>Khái niệm về tiến trình</i>

Tiến trình là một thể hiện (instance) của một chương trình máy tính đang chạy được thực thi bởi bộ xử lý máy tính (computer processor). Mỗi tiến trình được biểu diễn trong hệ điều hành bằng một khối dữ liệu được gọi là Process Control Block (PCB). Nó bao gồm tất cả thông tin của một tiến trình.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/ProcessControlBlock.png" alt="Cấu trúc dữ liệu của một Process Control Block">
  <figcaption>
	  <i>Cấu trúc dữ liệu của một Process Control Block</i>
  </figcaption>
</center>
</figure>

Một tiến trình có thể khởi tạo các tiến trình con (subprocess hay còn gọi là child process). Một tiến trình con là bản sao của tiến trình cha và chia sẻ tài nguyên của nó, nhưng tiến trình con không thể tồn tại nếu tiến trình cha bị chấm dứt.

#### <i>Khái niệm về luồng</i>

Luồng là đơn vị thực thi trong một tiến trình. Một tiến trình có thể có một hoặc nhiều luồng khác nhau.

Các tiến trình chạy trong không gian bộ nhớ riêng biệt với nhau trong khi các luồng trong cùng một tiến trình chạy chung trong một không gian bộ nhớ. Các luồng không độc lập với nhau giống như các tiến trình do đó các luồng có thể chia sẻ phần dữ liệu và tài nguyên cho nhau.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/ThreadControlBlock.png" alt="Cấu trúc dữ liệu của một Thread Control Block">
  <figcaption>
	  <i>Cấu trúc dữ liệu của một Thread Control Block</i>
  </figcaption>
</center>
</figure>

Vấn đề đồng bộ hóa có thể được phân chia thành hai loại chính:

* <i>Đồng bộ hóa tài nguyên (resource synchronization):</i> Xác định việc truy cập vào tài nguyên dùng chung (shared resource) có an toàn hay không, khi nào an toàn và khi nào không an toàn.
* <i>Đồng bộ hóa hoạt động (activity synchronization):</i> Đảm bảo thứ tự thực thi chính xác giữa các tác vụ khi được sử dụng phối hợp cùng với nhau. Đồng bộ hóa hoạt động bao gồm cả các vấn đề về đồng bộ (synchronous) và bất đồng bộ (asynchronous).

### Phân biệt khái niệm đồng thời và song song

Cả hai khái niệm đồng thời (concurrency) và song song (parallelism) đều đề cập đến việc giải quyết nhiều tác vụ tại một thời điểm nhưng có một chút khác biệt giữa hai khái niệm này. Thuật ngữ lập trình đồng thời (concurrent programming) để cập đến hai hoặc nhiều tiến trình được xử lý xen kẽ nhau thông qua cơ chế context switch và hoàn thành tác vụ trong các khoảng thời gian chồng chéo nhau trên một lõi đơn của CPU. Thuật ngữ lập trình song song (parallel programming) đề cập đến hai hoặc nhiều tiến trình được xử lý song song với nhau trên nhiều lõi CPU khác nhau.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/HardwareConcurrencyParallel.png" alt="Ảnh minh phân biệt phân biệt khái niệm đồng thời và song song">
  <figcaption>
	  <i>Sự khác biệt về phần cứng giữa lập trình đồng thời và lập trình song song</i>
  </figcaption>
</center>
</figure>

### Giới thiệu về bài toán kinh điển "Bữa ăn tối của các triết gia"

Trong khoa học máy tính, bài toán buổi ăn tối của các triết gia (Dining Philosophers Problem) thường được xem là ví dụ minh họa tốt nhất cho các vấn đề về đồng bộ hóa. Chúng ta hãy cùng tìm hiểu bài toán này.

Bài toán buổi ăn tối của các triết gia được đề xuất lần đầu tiên bởi E. W. Dijkstra. Mình tạm dịch tóm lược lại nội dung của <a href="https://en.wikipedia.org/wiki/Dining_philosophers_problem" target="_blank">bài toán này</a> từ Wikipedia như sau:<br/>

* Có 5 nhà triết học ngồi xung quanh một chiếc bàn tròn
* Mỗi nhà triết học có một bát mỳ Ý và một chiếc nĩa được đặt giữa mỗi cặp nhà triết học kề nhau
* Mỗi nhà triết học chỉ có hai trạng thái luân phiên nhau là suy nghĩ và ăn mỳ
* Tuy nhiên, một nhà triết học chỉ có thể ăn mỳ khi họ cả cả nĩa đặt bên trái và nĩa đặt bên phải của họ
* Mỗi một chiếc nĩa chỉ được sử dụng bởi một nhà triết học tại một thời điểm, do đó một nhà triết học chỉ sử dụng được nĩa khi nó hiện đang chưa được sử dụng bởi nhà triết học khác
* Sau khi một nhà triết học ăn mỳ xong cần đặt cả hai nĩa trở về vị trí gốc ban đầu để các nhà triết học còn lại có thể sử dụng
* Một nhà triết học không thể bắt đầu ăn mỳ khi họ chưa lấy được đầy đủ cả hai nĩa bên trái lẫn bên phải
* Giả sử việc ăn uống của mỗi nhà triết học này là không bị giới hạn và không một nhà triết học nào có thể biết liệu khi nào những người còn lại có thể muốn ăn mỳ hoặc suy nghĩ
* Hãy thiết kế một thuật toán sao cho mỗi nhà triết học có thể tiếp tục mãi mãi giữa hai trạng thái suy nghĩ và ăn mỳ mà không bị nhịn đói

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/DiningPhilosophersProblem.png" alt="Ảnh minh họa cho bài toán buổi ăn tối của các triết gia">
  <figcaption>
	  <i>Ảnh minh họa cho bài toán buổi ăn tối của các triết gia. Nguồn: O'Reilly</i>
  </figcaption>
</center>
</figure>

Trong bài toán này, mỗi cái nĩa đại diện cho tài nguyên của hệ thống và mỗi nhà triết học đại diện cho một tiến trình. Những vấn đề mà các nhà triết học này có thể gặp phải tương tự như những vấn đề trong lập trình máy tính khi nhiều tiến trình cần quyền truy cập độc quyền vào các tài nguyên dùng chung.

### Vấn đề Deadlock

Chúng ta có thể thấy một tình huống có thể phát sinh với bài toán đặt ra là tất cả 5 nhà triết học đều chọn nĩa bên trái và ngồi suy nghĩ cho đến khi lấy được nĩa bên phải để có thể ăn mỳ. Điều này dẫn đến trạng thái bế tắc, hay còn được gọi là deadlock, là trạng thái mà mỗi nhà triết học đã chọn cái nĩa ở bên trái đang đợi cái nĩa ở bên phải dẫn đến không có sự kiện nào tiếp theo có thể xảy ra. Có thể khái quát một cách tổng quát rằng deadlock xảy ra khi mỗi tiến trình (process) nắm giữ một tài nguyên và đợi được cấp tài nguyên từ bất kỳ tiến trình nào khác. Đây là một trong những vấn đề lớn mà chúng ta thường hay gặp nhất trong việc thiết kế những hệ thống chạy đồng thời (concurrent systems).

### Vấn đề Starvation

Giả sử chúng ta bổ sung thêm một quy tắc vào tập hợp các quy tắc trong bài toán trên là các nhà triết học nếu đang nắm giữ một nĩa sẽ phải đặt nĩa này xuống sau mười phút chờ đợi nếu vẫn chưa nắm giữ được nĩa còn lại, sau đó đợi thêm mười phút nữa để bắt đầu lại quá trình lấy nĩa. Nếu tất cả năm nhà triết học xuất hiện trong phòng ăn cùng một lúc và mỗi người này cầm chiếc nĩa bên trái cùng một lúc, các nhà triết học sẽ đợi mười phút cho đến khi tất cả đặt nĩa xuống và sau đó đợi thêm mười phút nữa trước khi tất cả cùng bắt đầu lại quá trình cầm nĩa lên.

Khái quát hóa một cách tổng quát thì tình trạng đói tài nguyên (resource starvation) có thể xảy ra do sự thiếu hụt tài nguyên máy tính hoặc do nhiều tiến trình đang cạnh tranh nắm giữ cho cùng một tài nguyên máy tính. Trong thực tế, tình trạng đói tài nguyên có thể xảy ra do lỗi trong việc thiết kế các thuật toán lập lịch hoặc thuật toán loại trừ tương hỗ, nhưng cũng có thể do rò rỉ tài nguyên và cũng có thể xảy ra qua hình thức tấn công có tên gọi là "<a href="https://www.imperva.com/learn/ddos/fork-bomb/" target="_blank">fork bomb</a>".

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/ForkBombAttack.jpg" alt="Ảnh minh họa mô phỏng hình thức tấn công fork bomb">
  <figcaption>
	  <i>Ảnh minh họa mô phỏng hình thức tấn công fork bomb. Nguồn: https://www.imperva.com</i>
  </figcaption>
</center>
</figure>

### Vấn đề Livelock

Livelock là một trường hợp đặc biệt của deadlock, trong đó các tiến trình (process) hoặc luồng (thread) có thể chuyển đổi trạng thái nhưng bị mắc kẹt và không đạt được tiến triển mới nào. Đây cũng là một vấn đề gặp phải tương đối phổ biến trong các chương trình đồng thời (concurrent program). Có thể minh họa trường hợp này bằng một ví dụ nhỏ sau. Giả sử có hai người gặp nhau trong một lối đi nhỏ. Khi người thứ nhất dịch chuyển qua phải để nhường lối đi thì người thứ hai cũng dịch chuyển qua phải. Khi người thứ nhất dịch chuyển qua trái để nhường lối đi thì người thứ hai cũng đồng thời dịch chuyển qua trái. Quá trình này cứ lặp đi lặp lại vô tận nhưng kết quả cuối cùng vẫn rơi vào bế tắc.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/LivelockIllustration.png" alt="Ảnh minh họa cho trường hợp Livelock">
  <figcaption>
	  <i>Ảnh minh họa cho trường hợp Livelock</i>
  </figcaption>
</center>
</figure>

### Vấn đề Critical Section

Critical Section hay còn gọi là vùng tranh chấp, là đoạn mã chứa các biến dùng chung có thể được truy cập bởi nhiều tiến trình hoặc luồng khác nhau có thể gây ra xung đột trong chương trình đồng thời. Vùng tranh chấp chứa các biến hoặc tài nguyên được chia sẻ cần được đồng bộ hóa để duy trì tính nhất quán của các biến dữ liệu. Nói một cách dễ hiểu, vùng tranh chấp là tập hợp các câu lệnh hoặc vùng mã cần thực hiện các tác vụ nguyên tử (atomic operation) chẳng hạn như truy cập tài nguyên (tệp, cổng đầu vào hoặc đầu ra, dữ liệu toàn cục,... ). Điều này đặc biệt đúng khi các tiến trình hoặc luồng tương tác với nó được lập lịch thiếu chính xác. Chúng ta cần thiết kế các giải pháp để bảo vệ tính toàn vẹn dữ liệu có liên quan đến các đoạn mã này.

### Vấn đề Race Condition

Race condition là một trường hợp xảy ra khi có nhiều luồng riêng biệt cùng truy cập vào một tài nguyên chung và thay đổi dữ liệu cùng lúc, làm cho dữ liệu cuối cùng không được chính xác như mong muốn. <i>Thread-safe</i> là thuật ngữ được sử dụng để mô tả một chương trình, đoạn mã hoặc cấu trúc dữ liệu không xảy ra race condition khi được nhiều luồng truy cập. Race condition có thể được ngăn chặn bằng cách tuần tự hóa các quá trình truy cập vào tài nguyên chung. Nếu các lệnh đọc và ghi là đồng thời với nhau, chúng ta sẽ mặc định ưu tiên lệnh đọc luôn được thực hiện và hoàn thành trước. 

### Tài liệu tham khảo

* <a href="https://computersciencewiki.org/index.php/Processes_and_Threads/" target="_blank">https://computersciencewiki.org/index.php/Processes_and_Threads/</a>
* <a href="https://www.geeksforgeeks.org/difference-between-deadlock-and-starvation-in-os/" target="_blank">https://www.geeksforgeeks.org/difference-between-deadlock-and-starvation-in-os/</a>
* <a href="https://en.wikipedia.org/wiki/Dining_philosophers_problem" target="_blank">https://en.wikipedia.org/wiki/Dining_philosophers_problem</a>
* <a href="https://en.wikipedia.org/wiki/Starvation_(computer_science)" target="_blank">https://en.wikipedia.org/wiki/Starvation_(computer_science)</a>
* <a href="https://csrc.nist.gov/glossary/term/Resource_Starvation" target="_blank">https://csrc.nist.gov/glossary/term/Resource_Starvation</a>
* <a href="https://www.geeksforgeeks.org/deadlock-starvation-and-livelock/" target="_blank">https://www.geeksforgeeks.org/deadlock-starvation-and-livelock/</a>
* <a href="https://www.imperva.com/learn/ddos/fork-bomb/" target="_blank">https://www.imperva.com/learn/ddos/fork-bomb/</a>
* <a href="http://www.embeddedlinux.org.cn/rtconforembsys/5107final/LiB0091.html/" target="_blank">http://www.embeddedlinux.org.cn/rtconforembsys/5107final/LiB0091.html/</a>




