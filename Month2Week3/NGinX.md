# Tìm hiểu về NGinX
## 1. NGinX là gì?
### 1.1. Định nghĩa
NGINX là một máy chủ web mã nguồn mở mạnh mẽ và máy chủ reverse proxy đã trở nên phổ biến rộng rãi nhờ hiệu suất cao, khả năng mở rộng và tính linh hoạt của nó. Ban đầu được tạo ra vào năm 2004 bởi Igor Sysoev, NGINX hiện được phát triển và duy trì bởi NGINX, Inc. NGINX được phát âm là "engine X", thể hiện mục đích của nó là xử lý hiệu quả lưu lượng truy cập web lớn.
### 1.2. Cách hoạt động
NGINX hoạt động như một máy chủ web, phục vụ nội dung tĩnh như tệp HTML, CSS và JavaScript cho máy khách. Nó vượt trội trong việc xử lý các kết nối đồng thời và phân phối hiệu quả nội dung tĩnh với mức sử dụng tài nguyên tối thiểu. Kiến trúc của NGINX là hướng theo sự kiện và không đồng bộ, cho phép nó xử lý một số lượng lớn các kết nối đồng thời một cách hiệu quả, khiến nó trở nên lý tưởng cho các trang web có lưu lượng truy cập cao.
### 1.3. Khả năng mở rộng
NGINX có khả năng mở rộng cao thông qua các modules và hỗ trợ nhiều giao thức khác nhau như HTTP, HTTPS, SMTP, WebSocket, v.v. Nó có thể xử lý kết thúc SSL/TLS, cho phép nó xử lý các kết nối an toàn và giảm tải quá trình mã hóa từ các máy chủ phụ trợ. Ngoài ra, NGINX cung cấp các tùy chọn cấu hình mạnh mẽ, cho phép quản trị viên tinh chỉnh hành vi của nó để đáp ứng các yêu cầu cụ thể.
## 2. Reverse Proxy & caching
### 2.1. Reverse Proxy
NGINX nằm giữa máy khách và backends server, thay mặt máy chủ chấp nhận các yêu cầu của máy khách. Khi một máy khách gửi yêu cầu tới reverse proxy NGINX, nó sẽ chuyển tiếp yêu cầu tới backends server thích hợp dựa trên các quy tắc được xác định trước và thuật toán cân bằng tải(load balancing). Điều này cho phép NGINX phân phối lưu lượng đến trên nhiều máy chủ, cân bằng tải và ngăn không cho bất kỳ máy chủ đơn lẻ nào bị quá tải. Bằng cách đó, NGINX giúp cải thiện hiệu suất tổng thể và tính khả dụng của ứng dụng.
### 2.2. Caching
Ngoài ra, NGINX có thể hoạt động như một máy chủ bộ đệm (caching server), lưu trữ nội dung được truy cập thường xuyên trong bộ nhớ của nó. Khi một khách hàng yêu cầu một tài nguyên, NGINX sẽ kiểm tra bộ đệm của nó trước để xem liệu nó có bản sao của nội dung được yêu cầu hay không. Nếu nội dung được tìm thấy trong bộ đệm, NGINX sẽ gửi trực tiếp nội dung đó đến máy khách mà không chuyển tiếp yêu cầu đến máy chủ phụ trợ. Cơ chế lưu vào bộ nhớ đệm này giúp giảm đáng kể thời gian phản hồi và giúp máy chủ phụ trợ không phải xử lý các yêu cầu dư thừa, giúp cải thiện hiệu suất và giảm tải cho máy chủ.

Nhìn chung, các chức năng bộ nhớ đệm và reverse proxy của NGINX góp phần phân phối lưu lượng hiệu quả, cân bằng tải và phân phối nội dung được tăng tốc, cuối cùng là nâng cao hiệu suất, khả năng mở rộng và trải nghiệm người dùng của các ứng dụng web.
## 4. Load Balancing
NGINX cũng cung cấp các khả năng cân bằng tải nâng cao, chẳng hạn như round-robin, least connections, IP hash,... Các thuật toán này phân phối yêu cầu một cách thông minh, xem xét các yếu tố như tình trạng máy chủ và thời gian phản hồi, để đảm bảo sử dụng tài nguyên hiệu quả và trải nghiệm người dùng tối ưu.
Dưới đây là một số thuật toán cân bằng tải thường được sử dụng được NGINX hỗ trợ:
1. Round Robin (mặc định): Các yêu cầu được phân phối đồng đều theo cách tuần tự giữa các máy chủ phụ trợ. Mỗi yêu cầu tiếp theo được chuyển tiếp đến máy chủ tiếp theo trong nhóm. 
2. Least Connections: Yêu cầu được chuyển đến máy chủ có ít kết nối hoạt động nhất vào thời điểm đó. Thuật toán này giúp phân phối tải dựa trên dung lượng máy chủ hiện tại. 
3. IP Hash: Địa chỉ IP của máy khách được sử dụng để xác định máy chủ phụ trợ nào sẽ xử lý yêu cầu. Điều này đảm bảo rằng các yêu cầu từ cùng một máy khách được định tuyến nhất quán đến cùng một máy chủ, điều này có thể hữu ích cho tính bền vững của phiên. 
4. Generic Hash: Khóa tùy chỉnh do người dùng xác định được sử dụng để xác định máy chủ phụ trợ. Điều này cho phép kiểm soát nhiều hơn hành vi cân bằng tải vì bất kỳ dữ liệu liên quan nào cũng có thể được sử dụng để đưa ra quyết định định tuyến. 
5. Least Time: NGINX đo thời gian phản hồi từ các máy chủ phụ trợ và hướng yêu cầu đến máy chủ có thời gian phản hồi nhanh nhất. Thuật toán này rất hữu ích khi thời gian phản hồi là một yếu tố quan trọng. 
6. Ngẫu nhiên: Các yêu cầu được phân phối ngẫu nhiên giữa các máy chủ phụ trợ, điều này có thể hiệu quả đối với một số tình huống nhất định khi không cần thiết phải phân phối đồng đều.