Báo Cáo Phân Tích Chuyên Sâu Về Kiến Trúc Thuật Toán, Mô Hình Toán Học Xây Dựng B-Profile Và Kỹ Thuật Sinh Lưu Lượng Mạng Lành Tính 

# Lịch Sử Tiến Hóa Của Các Hệ Thống Phát Hiện Xâm Nhập Và Yêu Cầu Cấp Thiết Về Tập Dữ Liệu Benchmark Hiện Đại 

Sự bùng nổ theo cấp số nhân của các cuộc tấn công mạng, cùng với sự tinh vi ngày càng gia tăng của phần mềm độc hại, đã thúc đẩy cộng đồng an toàn thông tin phát triển mạnh mẽ các Hệ thống Phát hiện Xâm nhập (Intrusion Detection Systems - IDS) và Hệ thống Ngăn ngừa Xâm nhập (Intrusion Prevention Systems - IPS) dựa trên các thuật toán Học máy (Machine Learning) và Học sâu (Deep Learning). 1 Mục tiêu cốt lõi của các hệ thống này là phân tích lưu lượng mạng theo thời gian thực để phát hiện các mẫu bất thường, từ đó ngăn chặn kịp thời các mối đe dọa như Tấn công Từ chối Dịch vụ Phân tán (DDoS), Botnet, hay các mối đe dọa dai dẳng nâng cao (Advanced Persistent Threats - APT). 3 Tuy nhiên, để huấn luyện, tinh chỉnh và đánh giá một cách khách quan tính hiệu quả của các mô hình này, các nhà nghiên cứu cần có quyền truy cập vào các tập dữ liệu benchmark (chuẩn đối sánh) phản ánh trung thực toàn cảnh môi trường mạng thực tế. 

Trong lịch sử nghiên cứu bảo mật hai thập kỷ qua, các tập dữ liệu truyền thống như DARPA 98, KDD CUP 99, hay ISC2012 đã đóng vai trò quan trọng trong việc định hình các hệ thống IDS thế hệ đầu. 4 Tuy nhiên, các phân tích chuyên sâu đã chỉ ra rằng những tập dữ liệu này hiện đã trở nên lỗi thời và mang nhiều khiếm khuyết chí mạng, khiến chúng không còn độ tin cậy đối với các hệ thống phòng thủ hiện đại. Cụ thể, các tập dữ liệu cũ thường thiếu đi sự đa dạng về lưu lượng, không phản ánh các giao thức mã hóa phổ biến ngày nay (như HTTPS), đồng thời thiếu hụt sự phong phú của các họ tấn công mới. 1 Một nỗ lực nâng cấp đáng chú ý là bộ dữ liệu ADFA13 của Đại học New South Wales, trong đó các nhà nghiên cứu đã cài đặt Apache, MySQL và Tikiwiki để cung cấp dịch vụ web, cơ sở dữ liệu và FTP server nhằm sinh dữ liệu. 6

Dù vậy, nó vẫn chưa đủ sức bao quát sự phức tạp của lưu lượng mạng doanh nghiệp quy mô lớn. 4

Một trong những bài toán hóc búa nhất khi xây dựng dữ liệu IDS là sự xung đột trực tiếp giữa tính chân thực của dữ liệu và quyền riêng tư của tổ chức. Việc sử dụng kỹ thuật sao chép dữ liệu công khai từ mạng doanh nghiệp (replaying publicly available datasets) luôn đi kèm với quy trình ẩn danh hóa (anonymization) bắt buộc nhằm loại bỏ thông tin nhạy cảm. 6 Tuy nhiên, quá trình ẩn danh hóa này thường phá hủy hoàn toàn nội dung payload (tải trọng gói tin), làm mất đi các đặc trưng ngữ nghĩa và thống kê cốt lõi mà các mô hình học máy cần để phân biệt giữa hành vi bình thường và chữ ký của mã độc. 1 Hệ quả là các mô hình được đào tạo trên dữ liệu bị ẩn danh thường rơi vào trạng thái quá khớp (overfitting) hoặc tạo ra tỷ lệ cảnh báo giả (false positive rate) ở mức không thể chấp nhận được trong môi trường thực tế. 7

Để giải quyết triệt để rào cản này, hệ thống B-Profile (Benign Profile) và M-Profile (Malicious Profile) đã được các nhà nghiên cứu tại Viện An ninh Mạng Canada (CIC) phát triển. 4 B-Profile đại diện cho một bước chuyển mình mang tính mô thức: thay vì ghi lại và xáo trộn lưu lượng của con người một cách thụ động, hệ thống sử dụng các kỹ thuật học máy, lý thuyết thống kê, và kỹ thuật giả lập (agent-based simulation) để "trích xuất" và "đóng gói" các hành vi trừu tượng của người dùng. 6 Các đặc tính hành vi này sau đó được sử dụng làm khuôn mẫu để tự động sinh ra dữ liệu mạng nhiễu nền (background traffic) hoàn toàn lành tính nhưng mang các tính chất vật lý và thống kê giống hệt dữ liệu sinh học. 2 Vì lưu lượng được tạo ra bằng nhân tạo dựa trên các trọng tâm toán học chứ không phải từ thao tác vật lý của nhân viên, vấn đề ẩn danh hóa dữ liệu được giải quyết tận gốc, mở ra khả năng chia sẻ công khai các tập dữ liệu cực kỳ chất lượng như CIC-IDS2017 và CSE-CIC-IDS2018 cho cộng đồng nghiên cứu toàn cầu. 9

# Giai Đoạn Khởi Tạo: Thu Thập Đặc Trưng Luồng Và Phương Pháp Biểu Diễn Chuỗi Thời Gian 48-Cột (Individual Profiling) 

Bước đầu tiên và quan trọng nhất để xây dựng B-Profile là giai đoạn Lập Hồ sơ Cá nhân (Individual Profiling). Hệ thống phải quan sát người dùng thực trong một môi trường được kiểm soát chặt chẽ để thu thập dữ liệu về cách họ tương tác với các ứng dụng. 9

## Quá Trình Trích Xuất Đặc Trưng Với CICFlowMeter 

Hành vi của người dùng trên mạng không phải là những gói tin vô nghĩa bay lơ lửng, mà chúng tuân theo những đặc tính phân phối thống kê cụ thể đối với từng giao thức. Để đảm bảo hồ sơ phản ánh được thực tiễn hiện đại, B-Profile tập trung theo dõi 5 nhóm giao thức xương sống của mọi môi trường mạng bao gồm: HTTP, HTTPS (đại diện cho lưu lượng lướt web mã hóa và không mã hóa), FTP (giao thức truyền tải tệp tin), SSH (giao thức điều khiển từ xa mã hóa), và các giao thức Email (như SMTP, IMAP, POP3). 6 Các nhà nghiên cứu thiết lập nhiều phương pháp linh hoạt để giám sát và ghi nhận hoạt động mạng, bao gồm tấn công Man-In-The-Middle (MITM) trong môi trường thử nghiệm, đánh hơi mạng (network sniffing), và đối chiếu với lịch sử duyệt web cũng như lịch sử email của người dùng. 6

Dữ liệu thô thu được từ các tệp PCAP (Packet Capture) không được đưa trực tiếp vào mô hình học máy mà trải qua quá trình trích xuất đặc trưng chuyên sâu bằng công cụ CICFlowMeter (trước đây là ISCXFlowMeter). 11 CICFlowMeter tiến hành đọc cấu trúc gói tin và kết xuất ra hơn 80 đặc trưng thống kê và vật lý liên quan đến tầng mạng (network layer) và tầng giao vận (transport layer). 4 Một số đặc trưng hạt nhân bao gồm: thời lượng luồng (fl_dur), tổng số gói tin theo chiều đi (tot_fw_pk), tổng số gói tin theo chiều về (tot_bw_pk), tổng kích thước gói tin theo chiều đi (tot_l_fw_pkt), cùng với các mẫu cụ thể trong payload và sự phân phối thời gian của các yêu cầu đối với từng giao thức (request time distribution). 2 Những nhãn luồng này đều được định danh rõ ràng bởi 5 yếu tố cấu thành (5-tuple): Địa chỉ IP Nguồn, Cổng Nguồn, Địa chỉ IP Đích, Cổng Đích và Giao thức. 13 

Bảng 1: Các đặc trưng tiêu biểu được trích xuất bởi CICFlowMeter phục vụ lập hồ sơ hành vi. 9

Tên Đặc Trưng (Feature 

Name) 

Mô Tả Kỹ Thuật  Ý Nghĩa Trong Lập Hồ Sơ 

Hành Vi 

fl_dur  Thời lượng tồn tại của luồng 

(Flow duration). 

Phản ánh thời gian người dùng 

duy trì kết nối (vd: phiên SSH 

dài hay kết nối HTTP ngắn). 

tot_fw_pk / tot_bw_pk  Tổng số gói tin chiều tiến/lùi.  Xác định tỷ lệ tải lên/tải xuống, 

đặc trưng cho hành vi lướt web 

hoặc upload file FTP. 

tot_l_fw_pkt  Tổng kích thước gói tin chiều 

tiến. 

Định lượng dung lượng 

payload được gửi đi, giúp hệ 

thống tái tạo kích thước dữ liệu 

chân thực. 

Payload Patterns  Các mẫu chuỗi byte xuất hiện 

trong payload. 

Nhận diện chữ ký của các giao 

thức không mã hóa hoặc các 

thao tác gửi lệnh quản trị. 

Request Time Dist.  Phân phối thời gian yêu cầu 

gói tin. 

Nắm bắt nhịp độ tương tác 

(nhấn chuột, thời gian chờ đọc 

văn bản) mang tính con người. 

## Phương Pháp Biểu Diễn Hành Vi Dưới Dạng Chuỗi Thời Gian (Time-Series Histogram) 

Nếu chỉ dựa vào các chỉ số trung bình của các đặc trưng mạng, hệ thống sẽ đánh mất một yếu tố quan trọng bậc nhất của hành vi con người: Tính thời điểm và tính bùng nổ (burstiness). Một người dùng có thể tải xuống 10GB dữ liệu trong 30 phút buổi sáng và hoàn toàn không làm gì vào buổi chiều; điều này rất khác với một máy chủ tự động tải xuống rải rác 10GB dữ liệu trong suốt 24 giờ. Để giải quyết bài toán định lượng thời gian này, B-Profile triển khai một kỹ thuật mã hóa dữ liệu độc đáo. 6

Các hoạt động mạng của mỗi cá nhân được ghi lại và phân loại theo từng ngày và từng giao thức riêng biệt. Thay vì lưu trữ chuỗi log khổng lồ, hệ thống tính toán một biểu đồ tần suất (histogram) gồm chính xác 48 cột (48 bars) cho mỗi 24 giờ. 6 Khung thời gian một ngày được chia nhỏ thành các khoảng thời gian (bin) bằng nhau, với mỗi cột đại diện cho một khoảng thời gian 30 phút. 6 Các hành vi mạng như số lượng kết nối HTTP hay dung lượng truyền FTP được tổng hợp và phân bổ vào các cột tương ứng theo thời gian thực thi. 

Việc cấu trúc hóa hồ sơ thành một biểu đồ 48-cột mang lại nhiều lợi thế toán học và kỹ thuật. Thứ nhất, độ phân giải 30 phút là điểm cân bằng lý tưởng. Nếu khoảng thời gian quá ngắn (ví dụ: 1 phút), chuỗi thời gian sẽ dài 1440 cột, dẫn đến hiện tượng ma trận thưa thớt (data sparsity) và "lời nguyền của số chiều" (curse of dimensionality) khiến các thuật toán phân cụm không thể hội tụ. 16 Nếu khoảng thời gian quá dài (ví dụ: 2 giờ), độ chi tiết của hành vi – như một đợt lướt web ngắn trong giờ nghỉ trưa – sẽ bị san phẳng và hòa tan vào thời gian làm việc. Thứ hai, biểu đồ 48-cột chuyển đổi dữ liệu mạng hỗn loạn thành một dạng dữ liệu chuỗi thời gian chuẩn hóa (standardized time-dependent sequence), tạo tiền đề hoàn hảo cho các thuật toán phân tích chuỗi thời gian và khớp động trong các bước tiếp theo. 6

# Phá Vỡ Giới Hạn Của K-Means: Phân Cụm Hành Vi Trừu Tượng Bằng Thuật Toán X-Means Và Tiêu Chuẩn Thông Tin Bayes (BIC) 

Sau khi hồ sơ của hàng trăm, hoặc hàng nghìn người dùng được số hóa thành các chuỗi biểu đồ 48-cột, thách thức kế tiếp là bài toán Gom cụm (Clustering). Mục tiêu của giai đoạn này là đối chiếu hồ sơ cá nhân của từng người dùng với tất cả những người dùng khác, qua đó tìm ra các nhóm người có hành vi và phân phối hoạt động thống kê tương đồng. 6 Mỗi cụm (cluster) thu được sẽ cung cấp một giá trị trọng tâm, được coi là khuôn mẫu "hành vi trừu tượng" (abstract behavior) của tập hợp người dùng đó. 6

## Sự Bất Lực Của Thuật Toán K-Means Trước Dữ Liệu Hành Vi Động 

Theo thông lệ, thuật toán K-Means (hoặc thuật toán Lloyd) thường được sử dụng làm công cụ chủ lực cho các tác vụ phân cụm, nhờ vào sự đơn giản và tốc độ tính toán. 16 Thuật toán 

K-Means hoạt động bằng cách cố gắng chia  mẫu quan sát thành  cụm sao cho phương sai trong cụm (within-cluster sum-of-squares) hay "quán tính" (inertia) đạt giá trị cực tiểu. 16 

Tuy nhiên, K-Means mang trong mình những điểm yếu chí mạng khi đối mặt với dữ liệu hành vi người dùng chưa biết trước cấu trúc. Vấn đề lớn nhất là K-Means đòi hỏi người vận hành phải 

xác định trước số lượng cụm  ngay từ lúc khởi tạo thuật toán. 19 Trong các kịch bản thế giới 

thực, hành vi mạng của con người vô cùng đa dạng, thay đổi liên tục theo chức năng công việc, múi giờ, và sở thích cá nhân; hoàn toàn không có một cơ sở toán học hay chuyên gia nào có thể dự đoán chính xác có bao nhiêu nhóm "nguyên mẫu hành vi trừu tượng" tồn tại trong một 

hệ thống mạng doanh nghiệp. 6 Nếu chọn  quá nhỏ, K-Means sẽ ép buộc các nhóm hành vi 

khác biệt gộp lại với nhau, làm mờ đi các đặc trưng riêng lẻ và sinh ra một trọng tâm nhiễu. 

Ngược lại, nếu chọn  quá lớn, một mẫu hành vi thống nhất có thể bị chia cắt thành nhiều 

tiểu nhóm một cách giả tạo. Hơn thế nữa, K-Means còn tỏ ra chậm chạp và mở rộng kém khi dữ liệu ngày càng khổng lồ, đồng thời thường rơi vào các cực tiểu cục bộ tồi tệ khi bị ép chạy 

với một giá trị  cố định. 19 

## Sự Chuyển Đổi Sang Thuật Toán X-Means 

Để vượt qua giới hạn cứng nhắc của K-Means, hệ thống B-Profile ứng dụng thuật toán phân cụm X-Means do Pelleg và Moore phát triển (2000). 6 X-Means là một biến thể mở rộng tiên tiến của K-Means, sở hữu năng lực tự động ước lượng số lượng cụm tối ưu từ dữ liệu mà không 

cần thông số  định trước. 17 Thuật toán này không chỉ giải quyết triệt để bài toán xác định 

, mà còn gia tăng hiệu suất xử lý thông qua việc áp dụng cấu trúc cây dữ liệu đa độ phân giải (multiresolution kd-tree) và lưu trữ các thống kê cần thiết tại các nút (nodes), giúp cho thuật toán mở rộng hoàn hảo với các tập dữ liệu có số lượng bản ghi khổng lồ. 20 

Cơ chế hoạt động của X-Means bắt đầu bằng việc yêu cầu người dùng định nghĩa một ranh 

giới tối thiểu và tối đa  mà giá trị  thực sự có thể nằm trong đó. 25 Khởi đầu 

với số lượng cụm tối thiểu (thường là  hoặc  ), thuật toán X-Means xen kẽ 

thực hiện hai bước chính yếu một cách liên tục cho tới khi đạt đến giới hạn trên hoặc tìm được cấu trúc tối ưu: 

1.  Cải thiện tham số (Improve-Params): Chạy thuật toán K-Means cổ điển đến điểm hội tụ trên trung tâm các cụm hiện tại nhằm tìm ra vị trí tốt nhất cho các tâm cụm theo cấu trúc hiện tại. 24 

2.  Cải thiện cấu trúc (Improve-Structure): Đây là khâu cốt lõi làm nên sức mạnh của X-Means. Thuật toán tiến hành các đánh giá cục bộ (local decisions) trên từng cụm hiện hành để xem xét xem liệu cụm đó có nên được phân tách thành hai cụm con hay không nhằm khớp với dữ liệu tốt hơn. 20 Động Cơ Phân Tách Toán Học: Tiêu Chuẩn Thông Tin Bayes (BIC) 

Bước "Cải thiện cấu trúc" cần một thước đo khách quan để quyết định khi nào việc phân tách là hợp lý. Nếu chỉ dựa vào việc giảm phương sai (inertia), hệ thống sẽ tiếp tục tách cụm cho đến khi mỗi điểm dữ liệu trở thành một cụm riêng biệt, dẫn đến quá khớp (overfitting). Để ngăn chặn điều này, X-Means áp dụng Tiêu chuẩn Thông tin Bayes (Bayesian Information Criterion - BIC), do Gideon E. Schwarz công bố vào năm 1978, làm hàm mục tiêu cho các quyết định phân tách. 25 

BIC là một công cụ tuyển chọn mô hình trong thống kê, được thiết kế để tìm kiếm điểm cân bằng tối ưu giữa "độ khớp của mô hình với dữ liệu" và "độ phức tạp của mô hình". 21 Về mặt toán học, hệ thức BIC được biểu diễn toàn diện như sau: 

Trong hệ phương trình này: 

● đại diện cho giá trị cực đại của hàm hợp lý (maximized likelihood) của mô hình dựa 

trên dữ liệu quan sát. 27 Đối với X-Means, hàm hợp lý được tính dựa trên giả định rằng các điểm dữ liệu trong một cụm tuân theo phân phối chuẩn (Gaussian distribution) với 

một giá trị trung bình  và ma trận hiệp phương sai  xác định. 28 

● biểu thị tổng số lượng tham số tự do (free parameters) cần thiết để xây dựng mô 

hình. 27 Việc chia một cụm thành hai đồng nghĩa với việc mô hình phải duy trì thêm các 

vector trung bình và ma trận phương sai mới, làm gia tăng giá trị  .

● là tổng số lượng các điểm dữ liệu quan sát (sample size). 27 

Phân tích động lực học của công thức này cho thấy cơ chế chống quá khớp tuyệt vời của BIC. 

Hạng tử thứ hai,  , đo lường sai số của mô hình. Bất cứ khi nào X-Means thử tách 

một cụm gốc thành hai cụm con (bằng cách đặt hai tâm cụm mới dọc theo vector ngẫu nhiên ở khoảng cách bằng 1/3 từ trung tâm đến rìa cụm) 28 , khoảng cách từ các điểm dữ liệu đến tâm 

cụm gần nhất sẽ giảm đi. Điều này làm gia tăng hàm hợp lý  , và do đó làm giảm giá trị của 

hạng tử  , tạo ra áp lực thúc đẩy việc chia tách. 

Tuy nhiên, áp lực này bị kháng cự mãnh liệt bởi hạng tử phạt thứ nhất,  . Hình phạt 

này đánh trực tiếp vào sự phức tạp của mô hình; với số lượng mẫu  càng lớn (đặc biệt khi 

), hình phạt của BIC áp đặt lên việc tăng tham số càng nặng nề so với các tiêu chuẩn tương đương như Tiêu chuẩn Thông tin Akaike (AIC). 26 

Thuật toán X-Means sẽ tính toán và so sánh điểm số BIC của hai cấu trúc: (1) Giữ nguyên cụm hiện tại, và (2) Chia cụm đó thành hai. Quyết định phân tách chỉ được thực thi nếu cấu trúc mới sinh ra điểm BIC cao hơn (hoặc thấp hơn, tùy thuộc vào cách dấu trừ được lập trình trong hàm tối ưu). 24 Việc sử dụng mô hình xác suất Gaussian cho phép X-Means thực hiện các quyết định thông minh, chẳng hạn như phân tách phân phối dọc theo trục chính của nó khi khoảng cách lớn hơn 1.2 độ lệch chuẩn. 28 Toàn bộ quá trình này tiếp diễn tự động cho đến khi mọi nỗ lực phân tách đều dẫn đến việc điểm BIC xấu đi do hình phạt tham số quá cao. Cuối cùng, tập hợp các tâm cụm bảo tồn được điểm số tốt nhất sẽ trở thành kết quả đầu ra chung cuộc, biểu thị chính xác số lượng nhóm hành vi trừu tượng mà dữ liệu gợi ý. 25 

# Kỷ Nguyên Của Khớp Động Tuyến Tính: Dynamic Time Warping (DTW) Thay Thế Khoảng Cách Hình Học Cổ Điển 

Bên cạnh việc giải quyết số lượng cụm bằng thuật toán X-Means, hệ thống B-Profile phải xử lý một nút thắt cổ chai vô cùng nan giải khác: Lựa chọn hàm khoảng cách (Distance Function) cho chuỗi dữ liệu. Các nhà nghiên cứu phát hiện ra rằng, trong nhiều bài toán khai phá dữ liệu, việc lựa chọn một hàm khoảng cách để đo sự tương đồng thậm chí còn đóng vai trò quan trọng hơn bản thân thuật toán phân cụm. 6 Do hồ sơ mạng 48-cột mang bản chất của dữ liệu chuỗi thời gian (time-series data), các hàm khoảng cách không gian cổ điển như Euclidean, Cosine, hay Jaccard thể hiện hiệu năng tồi tệ một cách hệ thống trong việc phân nhóm hành vi. 6

## Vấn Đề Lock-Step Và Khoảng Cách Lạc Quan Giả Tạo Của Euclidean 

Khoảng cách Euclidean là thước đo sự tương đồng phổ biến nhất giữa hai vector, hoạt động 

bằng cách đối chiếu từng điểm  của chuỗi thứ nhất với điểm  tương ứng của chuỗi thứ hai 

trong không gian  chiều. Cơ chế này được gọi là phương pháp đối chiếu đồng bộ (lock-step 

one-to-one mapping). 30 

Mặc dù khoảng cách Euclidean phản ánh đúng bản chất hình học, nó thất bại hoàn toàn trước độ trễ thời gian (phase shift) – một hiện tượng sinh lý hiển nhiên trong hành vi của con người. 32 

Chẳng hạn, xem xét hoạt động của một nhân viên thường xuyên khởi động máy tính, kiểm tra email và truy cập vào máy chủ tệp tin nội bộ. Vào ngày đầu tiên, người này đến văn phòng lúc 8:00 sáng. Hành vi mạng tạo ra một biểu đồ gồm chuỗi các đỉnh băng thông tại cột thứ 16 (tương ứng với 8:00). Vào ngày thứ hai, do giao thông ùn tắc, nhân viên này đến văn phòng lúc 8:30 sáng và thực hiện chính xác cùng một khối lượng công việc, tạo ra biểu đồ đỉnh tại cột thứ 17. 

Về mặt logic và hành vi, hai chuỗi biểu đồ này giống hệt nhau về hình dạng (shape) và thuộc về cùng một khuôn mẫu trừu tượng, chỉ bị xê dịch dọc theo trục thời gian do độ trễ sinh hoạt. 32 Tuy nhiên, dưới con mắt của thuật toán Euclidean, hai chuỗi này bị coi là khác biệt một cách cực đoan. 31 Do nguyên lý lock-step, đỉnh lưu lượng của ngày thứ nhất tại cột 16 sẽ bị trừ đi đáy lưu lượng (lúc chưa có ai làm việc) của ngày thứ hai tại cột 16, tạo ra một giá trị bình phương sai số khổng lồ. 30 Hậu quả là các nhiệm vụ phân cụm, phân loại của chuỗi thời gian sẽ hoàn toàn sụp đổ nếu những sai lệch cục bộ (minor misalignments) này không được khắc phục. 30 

## Giải Pháp Toán Học: Dynamic Time Warping (DTW) 

Nhằm đo lường sự tương đồng giữa hai mẫu thời gian bị lệch pha hoặc khác biệt về tốc độ tiến triển, hệ thống B-Profile tích hợp hàm khoảng cách Dynamic Time Warping (DTW) vào nền tảng X-Means. 6 Khởi nguồn từ lĩnh vực nhận dạng giọng nói tự động vào thập niên 1970 34 , DTW mang lại tính toàn vẹn (invariance) chống lại các hiệu ứng dịch chuyển và co giãn dọc theo trục thời gian. 32 

Nguyên tắc vàng của DTW là loại bỏ sự cứng nhắc "một-đối-một" của khoảng cách Euclidean, thay thế bằng khả năng ánh xạ "nhiều-đối-một" (many-to-one) hoặc "một-đối-nhiều" (one-to-many). 33 Cơ chế này cho phép thuật toán "uốn cong" không gian thời gian (time-warp) để tìm ra cách căn chỉnh tối ưu giữa hai tín hiệu. 34 Nhờ đó, cột thứ 16 của ngày 1 hoàn toàn có thể được khớp nối hợp lệ với cột thứ 17 của ngày 2 mà không phát sinh sai số giả tạo, giúp hệ thống nhận diện thành công sự đồng dạng trong cấu trúc hành vi. 32 

Để hình thành giải pháp thuật toán, xét hai chuỗi thời gian phụ thuộc:  và 

.9 Thuật toán bắt đầu bằng cách khởi tạo một ma trận  có kích thước 

(với  cột biểu đồ), trong đó mỗi phần tử chứa khoảng cách Euclidean 

giữa điểm  và điểm  .6

Mục tiêu cốt lõi của DTW là xác định một "đường đi uốn éo" (warping path) 

, với  , kết nối từ ô đầu tiên đến ô cuối cùng của ma trận  sao 

cho tổng chi phí tích lũy dọc theo đường đi đạt giá trị cực tiểu. 6 Công thức tổng quát của bài toán tối ưu được diễn đạt: 

> 9

Sự di chuyển dọc theo ma trận này phải đáp ứng các định lý ràng buộc nghiêm ngặt để bảo vệ tính logic vật lý của dòng thời gian 32 :

1.  Điều kiện biên (Boundary Conditions): Đường đi phải xuất phát ở gốc thời gian và kết thúc chính xác ở điểm tận cùng  . Không một 

phân đoạn dữ liệu nào của biểu đồ 24 giờ bị phép thuật toán bỏ sót trong quá trình đánh giá. 

2.  Tính đơn điệu (Monotonicity): Hành trình ánh xạ phải luôn tịnh tiến, tức là chỉ số  và 

trong cặp tọa độ  không bao giờ được giảm đi. 32 Điều này tương đương với việc 

cấm đi ngược dòng thời gian. 

3.  Tính liên tục (Contiguity / Continuity): Đường đi bị giới hạn kích thước bước chuyển; nó chỉ có thể lan truyền qua các ô kề cạnh (ngang, dọc) hoặc đường chéo liền kề, tức là không được phép bỏ qua (skip) bất kỳ dữ liệu trung gian nào. 32 

Do số lượng các đường đi hợp lệ xuyên qua ma trận  có quy mô bùng nổ theo cấp số 

nhân (được định lượng bởi các số Delannoy) 32 , việc duyệt vét cạn (brute-force) là bất khả thi. Vì vậy, DTW sử dụng thuật toán Quy hoạch động (Dynamic Programming) với công thức truy hồi thanh lịch sau 6:

> 6

Công thức đệ quy này đảm bảo tính toán hiệu quả cực tiểu của chi phí tại ô tử  bằng 

cách cộng khoảng cách cơ sở  với giá trị nhỏ nhất của một trong ba đường dẫn 

trước đó (đường chéo  , đường ngang  , và đường dọc 

). 6 Sự xuất hiện của toán tử  chính là cơ chế linh hoạt cốt lõi, trao cho thuật 

toán khả năng tự động lựa chọn giãn dòng thời gian (đi ngang/dọc) hay tiến đồng bộ (đi chéo) để duy trì hình thái khớp nối có độ lệch thấp nhất. 38 Với độ phức tạp tính toán được nén xuống 

chỉ còn  , việc áp dụng DTW cho không gian 48-chiều của B-Profile xử lý siêu tốc, 

giải quyết được khiếm khuyết chậm chạp vốn là tiếng xấu của DTW khi ứng dụng trên các tập dữ liệu dài. 32 

Để ngăn chặn hệ thống lợi dụng việc "uốn cong" quá mức – ví dụ: ánh xạ hành vi buổi sáng với hành vi đêm khuya – các nhà khoa học thường áp dụng thêm các ràng buộc toàn cục (global 

constraints) như dải Sakoe-Chiba (Sakoe-Chiba band) có chiều rộng  hay hình bình hành 

Itakura. 32 Những dải này ép buộc đường đi  phải bám sát trục đường chéo chính của ma 

trận, cho phép sự lệch pha trong giới hạn trễ một vài giờ của sinh lý con người mà không làm mất đi tính toàn vẹn của mô hình thời gian thực tế. 32 Một giải pháp khác cũng được nhắc đến là Amerced DTW (ADTW), bổ sung thêm một khoản tiền phạt trực tiếp (additive penalty) mỗi khi đường đi uốn cong, giúp kiểm soát sự dễ dãi trong việc căn chỉnh. 34 

Bảng 2: So sánh đặc tính của Euclidean và DTW trong kiến trúc phân cụm B-Profile. 32 

Đặc tính so sánh  Khoảng cách Euclidean  Dynamic Time Warping 

(DTW) 

Bản chất ánh xạ  Đồng bộ (Lock-step, 1-1)  Phi tuyến tính, uốn dẻo 

(Many-1, 1-Many) 

Xử lý độ trễ thời gian  Yếu kém (Tạo sai số lớn giả 

tạo) 

Xuất sắc (Miễn nhiễm với 

phase shift) 

Độ phức tạp tính toán  Thấp (  ) Cao hơn bằng quy hoạch động 

( )

Tác động đến X-Means  Phân mảnh các hành vi cùng 

bản chất 

Gom cụm chính xác các hành 

vi tương quan 

# Lời Giải Toán Học Tìm Tâm Điểm: DTW Barycenter Averaging (DBA) 

Khi hệ thống X-Means (sử dụng BIC và DTW) hoàn tất quá trình phân nhóm và xác định cấu trúc cuối cùng, một bước tính toán thiết yếu khác xuất hiện: Xác định vị trí trọng tâm (centroid) của mỗi cụm. 6 Trong thế giới B-Profile, các trọng tâm này không chỉ là những điểm dữ liệu vô tri; chúng đại diện cho "các nguyên mẫu hành vi trừu tượng" (abstract behavior of users) tối hậu sẽ được Agent sử dụng để phát sinh lưu lượng. 6

Tính toán tâm điểm trong không gian phẳng Euclidean là thao tác cực kỳ sơ đẳng – nó đơn giản là việc lấy trung bình cộng số học của toàn bộ các phần tử thuộc cụm. Tuy nhiên, việc áp dụng công thức trung bình cộng cổ điển cho các chuỗi thời gian đã bị "uốn cong" bởi không gian DTW sẽ đem lại kết quả thảm họa. 40 Việc lấy trung bình các đỉnh sóng bị lệch pha ở các mốc thời gian khác nhau sẽ khiến cho hình thù của sóng lưu lượng mạng bị là phẳng (flattened) và trở nên mờ nhạt, làm mất đi các đỉnh bùng nổ năng lượng (spike) vốn là cốt lõi trong lưu lượng mạng của con người. 40 

Để khắc phục, hệ thống phải triển khai các kỹ thuật trung bình hóa thời gian nâng cao, tiêu biểu là phương pháp DTW Barycenter Averaging (DBA) hoặc các biến thể Soft-DTW. 41 Cốt lõi của DBA nằm ở việc cập nhật từng tọa độ của chuỗi trung bình giả định thông qua một cơ chế lặp (iterative refinement). Thuật toán khởi tạo một chuỗi trung tâm tạm thời, sau đó liên tục thực hiện căn chỉnh DTW giữa chuỗi trung tâm này với tất cả các chuỗi hồ sơ thành viên trong cụm. 41 Tại mỗi chu kỳ tinh chỉnh, DBA thay thế mỗi phần tử của chuỗi trung bình bằng tâm trọng lực (barycenter) của tất cả các phần tử trên các chuỗi thành viên mà đã được ánh xạ quang học đến nó. 41 Quá trình này được lặp lại nhiều lần (đôi khi yêu cầu từ 22 đến 35 vòng lặp hội tụ 42 ) cho đến khi hình thái của chuỗi trung tâm ổn định. Thuật toán DBA, dù có xu hướng tạo ra một số nhiễu gai nhỏ (spike artifacts) tại các mép căn chỉnh 42 , vẫn bảo tồn được nguyên vẹn sự mạnh mẽ của các đỉnh băng thông, duy trì đầy đủ sắc thái dữ liệu mạng lịch sử. 

Khi các giá trị centroid này được hoàn thiện, hệ thống đã trích xuất thành công bản chất trừu tượng của toàn bộ môi trường tổ chức. Từng bản B-Profile được lưu trữ như một bộ gen quy định mọi đặc tính (số gói tin, phân bổ thời gian, quy mô payload) mà không hề chứa bất kỳ một chuỗi địa chỉ IP hay văn bản thực tế nhạy cảm nào của con người. 2 Mục tiêu bảo vệ quyền riêng tư đã được hoàn tất một cách xuất sắc. 

# Hiện Thực Hóa Lưu Lượng: Cơ Chế Hoạt Động Của Tác Nhân (Agent) Và Kỹ Thuật Web-Crawling 

Có được mô hình toán học tối ưu chỉ là một nửa chặng đường. Để một hệ thống IDS như CIC-IDS2017 hay CSE-CIC-IDS2018 có thể huấn luyện các bộ phân lớp học máy, các hồ sơ B-Profile tĩnh phải được "thổi hồn" vào một mạng vật lý thực thụ dưới dạng các luồng gói tin TCP/UDP. 6

Giai đoạn sinh lưu lượng này dựa trên hoạt động của các Tác nhân phần mềm (Agents) tự trị. Tác nhân được thiết kế dưới dạng các kịch bản lập trình (script) bằng ngôn ngữ Python hoặc Java, sở hữu năng lực thực thi yêu cầu đa luồng (multi-threaded), cho phép nó tiến hành khởi tạo đồng thời hàng loạt yêu cầu kết nối mà không bị tắc nghẽn cục bộ. 4

## Quá Trình Nhập Vai Và Sinh Sự Kiện 

Vào thời điểm bắt đầu mỗi chu kỳ 24 giờ của hệ thống mô phỏng (ví dụ: bắt đầu ngày làm việc lúc 9:00 sáng), Agent sẽ ngẫu nhiên truy xuất và "nhập vai" một hồ sơ B-Profile cụ thể từ bộ sưu tập các cụm hành vi đã được tạo. 6 Sau khi đã khoác lên mình hình hài toán học của B-Profile (quy định mức độ thường xuyên sử dụng SSH, khối lượng tệp FTP được phép tải, nhịp độ mở HTTPS), Agent bắt đầu tương tác với mạng nội bộ. 

Quá trình giả lập lưu lượng các giao thức như FTP hay SSH tương đối trực tiếp bằng cách sinh ra các lệnh chuyển đổi tệp tin theo tỷ lệ phân phối thời gian đã lập trình. Tuy nhiên, đối với giao thức HTTP và HTTPS, việc chỉ gửi một lệnh GET rỗng hoặc tải một file tĩnh là không đủ để đánh lừa các cơ chế kiểm tra gói tin sâu (Deep Packet Inspection) của các hệ thống IDS hiện đại. 44 Nếu chỉ thực hiện kết nối nông, hành vi của Agent sẽ lộ rõ bản chất của một botnet ngớ ngẩn thay vì giống với một người dùng văn phòng phức tạp. 44 

## Kỹ Thuật Web-Crawling Nâng Cao Giả Lập Trình Duyệt 

Để các yêu cầu web trở nên tinh vi và sát thực tế nhất có thể, B-Profile triển khai một cơ chế thu thập dữ liệu web (web-crawling mechanism) đã được tinh chỉnh khéo léo. 6

Về mặt nền tảng công nghệ, cơ chế này sử dụng sức mạnh của khung ứng dụng (framework) Scrapy trên Python để định hướng luồng thu thập. Tuy nhiên, thay vì chỉ tải mã nguồn HTML đơn thuần, Agent được trang bị thêm lớp trung gian Selenium, có nhiệm vụ tự động hóa và điều khiển một trình duyệt web thực tế, ví dụ như Google Chrome. 46 Việc sử dụng trình duyệt vật lý đảm bảo rằng quá trình kết xuất (rendering) nội dung được thực thi trọn vẹn: JavaScript được biên dịch, các bảng CSS được tải về, và toàn bộ tài nguyên hình ảnh hay nội dung đa phương tiện phụ trợ trên trang web đều được nạp vào mạng nội bộ. 46 Cơ chế này tự động phục dựng lại sự phân bổ tỷ lệ HTML-to-Image và tái lập chính xác phân phối tải trọng (payload sizes) vốn rất phổ biến ở hành vi người dùng lướt các trang tin tức hoặc mạng xã hội. 44 

Vì thư viện Selenium đôi khi không phơi bày đầy đủ các gói tin cấp mạng (network-level details), hệ thống thu thập thông tin mạng tận dụng thêm Giao diện Lập trình Ứng dụng (API) của Chrome DevTools (Chrome DevTools API). Sự kết hợp này mang lại khả năng ghi nhận chi tiết, điều hướng đến tầng HTTP, lưu giữ các yêu cầu (requests) và phản hồi (responses) một cách trọn vẹn. 46 

Cơ chế web-crawling còn được tích hợp hệ thống tạo độ trễ mô phỏng hành vi con người (Human Delay). Việc điều chỉnh tỷ lệ nhấp chuột (click rate) và chèn các khoảng nghỉ ngẫu nhiên giúp Agent bẻ gãy cấu trúc đồng hồ hệ thống (clock-based structure) của mã tự động. 44 

Kết quả cuối cùng là hàng triệu luồng mạng (flows) chảy ra ngoài hệ thống từ Tác nhân Python đều mang đặc tính tự nhiên học máy, biến mạng lưới nội bộ thành một văn phòng ảo hoạt động nhộn nhịp như thế giới thực. 11 

# Tương Tác Giữa B-Profile Và M-Profile Trong Mô Phỏng Cấu Trúc Dữ Liệu Tập CIC-IDS2017 

Giá trị của tiếng ồn nền (B-Profile) chỉ được khẳng định khi nó phải đấu tranh với các kịch bản tấn công nguy hiểm. Để hiện thực hóa mục tiêu tạo ra tập dữ liệu chuẩn mực nhất thế giới, B-Profile được đặt vào một môi trường thực nghiệm nơi nó hoạt động song song với hệ thống M-Profile (Malicious Profile). 2

## Cấu Trúc Hệ Thống Mạng Thử Nghiệm 

Hệ thống phòng thí nghiệm được phân tách thành hai thực thể độc lập 1:

1.  Victim-Network (Mạng nạn nhân): Đây là khu vực nội bộ nơi các B-Profile Agents hoạt động. Nó mô phỏng một doanh nghiệp trọn vẹn với hạ tầng định tuyến đầy đủ, bao gồm tường lửa (Firewall Fortinet tại IP 205.174.165.80 và 172.16.0.1), Switch cấp phát, các Server nền tảng (DNS và Domain Controller Server tại 192.168.10.3), và đa dạng hệ điều hành của máy trạm (Ubuntu, Mac OS X, Windows Vista, 7, 8.1, 10). 1 Một máy chủ phân tích mạng được liên kết với cổng Mirror của Switch nhằm chụp lại toàn bộ mọi gói tin chảy qua mạng dưới định dạng PCAP. 48 

2.  Attack-Network (Mạng tấn công): Nằm bên ngoài hệ thống bảo mật nội bộ, sử dụng chủ yếu môi trường Kali Linux (IP 205.174.165.73) và một vài điểm nối Windows (IP 205.174.165.69,.70,.71). 1 Đây là nơi khởi nguồn của M-Profile, nơi những chuyên gia bảo mật điều hành các công cụ phổ biến như Nmap hay Metasploit. 46 

M-Profile định nghĩa các kịch bản tấn công rõ ràng nhằm đảm bảo tập dữ liệu bao phủ đầy đủ các lỗ hổng mạng hiện hành. Sáu cấu hình tấn công tiêu biểu bao gồm Brute Force (thử nghiệm mật khẩu bạo lực vào FTP và SSH), Heartbleed (khai thác lỗ hổng thư viện mã hóa OpenSSL), Botnet (nhiễm mã độc Ares và liên lạc máy chủ C&C), DoS/DDoS (như Slowloris, Hulk, GoldenEye làm cạn kiệt tài nguyên), Tấn công Ứng dụng Web (Web Attack như SQL Injection và XSS), và đặc biệt là Infiltration (kịch bản tiêm nhiễm mạng từ bên trong thông qua email độc hại và lỗ hổng trình duyệt để nâng quyền hệ thống). 4

## Chiến Lược Đan Xen Lưu Lượng Theo Trình Tự Thời Gian (Kịch Bản 5 Ngày) 

Để mô phỏng hoàn hảo các bối cảnh khác nhau, giai đoạn thu thập dữ liệu trong tập CIC-IDS2017 kéo dài trong 5 ngày liên tục từ 9:00 sáng Thứ Hai (3/7/2017) đến 5:00 chiều Thứ Sáu (7/7/2017). 1 Tổng lưu lượng thu được lên đến hàng triệu sự kiện phân tích. 50 

Bảng 3: Cấu trúc mô phỏng lưu lượng và đan xen sự kiện của B-Profile và M-Profile. 1

Ngày Mô Phỏng  Kịch Bản Lưu 

Lượng 

Kích Thước (GB)  Tương Tác Cốt Lõi 

Và Mức Độ Đan 

Xen 

Thứ Hai  Hoạt Động Bình 

Thường (Normal) 

11.0 GB  Không có sự can 

thiệp của M-Profile. 

B-Profile vận hành 

tự do, đóng vai trò 

nền tảng dữ liệu 

sạch (baseline) 

hoàn hảo phục vụ 

đào tạo mô hình 

Phát hiện Bất thường (Anomaly 

Detection). 46 

Thứ Ba  Normal + Tấn công  11.0 GB  B-Profile duy trì 

hoạt động trong bối 

cảnh 

Attack-Network liên 

tục dội bom mật 

khẩu bằng Brute 

Force (FTP-Patator, 

SSH-Patator) vào 

sáng và chiều. 11 

Thứ Tư  Normal + Tấn công  13.0 GB  Ngày có cường độ 

mạng nặng nhất. 

M-Profile khởi chạy 

Tấn công Web ứng 

dụng, Heartbleed và 

dội bom kết nối 

bằng hàng loạt 

công cụ DoS (Hulk, 

GoldenEye, 

Slowloris, 

Slowhttptest). 11 

Thứ Năm  Normal + Tấn công  7.8 GB  M-Profile kích hoạt 

các kịch bản 

Infiltration (Thâm 

nhập nội bộ) cực kỳ 

tĩnh lặng. B-Profile 

vô tình che đậy sự 

di chuyển ngang 

(lateral movement) 

của cửa hậu 

(backdoor) khi nó 

quét mạng nội bộ. 9

Thứ Sáu  Normal + Tấn công  8.3 GB  Kịch bản mạng bị 

xâm chiếm bởi hệ 

thống Botnet, đồng 

thời phải chống chọi 

với cường độ bóp nghẹt của Tấn công 

DDoS (DDoS 

PortScan). 11 

Các kịch bản Infiltration trong M-Profile, như tài liệu B-Profile mô tả, được thiết kế vô cùng tinh xảo. 9 Một nạn nhân nhận tài liệu độc hại qua email, một backdoor thực thi, sau đó quét mạng nội bộ để lây nhiễm các máy yếu kém; ngoài ra còn có kịch bản Infiltration thất bại (Unsuccessful Infiltration) nhằm đảm bảo hệ thống IDS có khả năng học các dấu hiệu của những đợt tấn công leo thang đặc quyền bất thành, chứ không chỉ phát hiện các cuộc tấn công trót lọt. 9 Tổng cộng, hơn 2,8 triệu phiên kết nối đã được gắn nhãn trong tập dữ liệu, cung cấp một hệ sinh thái không thể hoàn hảo hơn cho việc đánh giá khả năng chống chịu của hệ thống học máy nhiều lớp. 50 

# Kết Luận Về Giá Trị Đóng Góp Và Sự Hình Thành Tiêu Chuẩn Mới 

Tập hợp các giải pháp kiến trúc trong báo cáo này cung cấp một minh chứng rõ ràng về sự trưởng thành của lý thuyết phân tích hành vi mạng. Sự phối hợp mượt mà giữa các nền tảng toán học – bắt đầu từ kỹ thuật giảm thiểu kích thước không gian bằng biểu đồ Histogram 48-cột, kết hợp với sức mạnh phân rã tự động của thuật toán X-Means dưới sự kiểm soát chống quá khớp của Tiêu chuẩn Thông tin Bayes (BIC) – đã tạo nên một cơ chế định vị hành vi độc lập khỏi những thiên kiến chủ quan của con người. Hơn thế nữa, bằng cách thay thế khoảng cách tĩnh Euclidean bằng sự linh hoạt về mặt thời gian của Dynamic Time Warping (DTW) và hội tụ qua phương pháp DTW Barycenter Averaging (DBA), mô hình đã chứng minh rằng mọi dao động sinh học trong môi trường máy tính hoàn toàn có thể được đồng bộ hóa và tái thiết thành những khuôn mẫu tinh vi. 

Trong môi trường thực tiễn, việc ứng dụng B-Profile thông qua các Tác nhân đa luồng (Multi-threaded Agents) sử dụng kỹ thuật Web-crawling và kịch bản Selenium đã tạo ra một lớp ngụy trang xuất sắc. Nó sinh ra một khối lượng lưu lượng lành tính dồi dào, tự nhiên và tương thích chuẩn xác với các hệ thống phân tích sâu (Deep Packet Inspection), che lấp đi các nỗ lực xâm nhập của M-Profile. Tầm quan trọng vĩ mô nhất của kỹ thuật B-Profile là khả năng giải quyết dứt điểm nghịch lý giữa tính toàn vẹn của dữ liệu và đạo đức an ninh (quyền riêng tư dữ liệu). Không có bất kỳ email, mật khẩu hay tài nguyên cá nhân thực sự nào bị xâm phạm, mà thế giới an ninh mạng vẫn thu được các tập dữ liệu cực kỳ đáng tin cậy như CIC-IDS2017 hay CSE-CIC-IDS2018. Thành tựu này đã chính thức trở thành hình mẫu tiêu chuẩn, đặt nền móng vững chắc cho kỷ nguyên nghiên cứu các mô hình học sâu phòng thủ mạng toàn cầu. 

Nguồn trích dẫn 

1.  Intrusion detection evaluation dataset (CIC-IDS2017) - University of New Brunswick, truy cập vào tháng 4 23, 2026, 

https://www.unb.ca/cic/datasets/ids-2017.html 2.  Benign profiling design. | Download Scientific Diagram - ResearchGate, truy cập vào tháng 4 23, 2026, 

https://www.researchgate.net/figure/Benign-profiling-design_fig2_318286637  

> 3.

An Intelligent Agent-Based Detection System for DDoS Attacks Using Automatic Feature Extraction and Selection - MDPI, truy cập vào tháng 4 23, 2026, 

https://www.mdpi.com/1424-8220/23/6/3333  

> 4.

Toward Generating a New Intrusion Detection Dataset and Intrusion Traffic Characterization - SciTePress, truy cập vào tháng 4 23, 2026, 

https://www.scitepress.org/papers/2018/66398/66398.pdf  

> 5.

Evaluation of Machine Learning Techniques for Traffic Flow-Based Intrusion Detection, truy cập vào tháng 4 23, 2026, 

https://pmc.ncbi.nlm.nih.gov/articles/PMC9740321/  

> 6.

Towards a Reliable Intrusion Detection Benchmark Dataset - ResearchGate, truy cập vào tháng 4 23, 2026, 

https://www.researchgate.net/publication/318286637_Towards_a_Reliable_Intrusi 

on_Detection_Benchmark_Dataset  

> 7.

Adaptive Deception Framework with Behavioral Analysis for Enhanced Cybersecurity Defense - arXiv, truy cập vào tháng 4 23, 2026, 

https://arxiv.org/html/2510.02424v1  

> 8.

Benchmarking of Machine Learning for AnomalyBased Intrusion Detection Systems in the CICIDS2017 Dataset - ResearchGate, truy cập vào tháng 4 23, 2026, 

https://www.researchgate.net/publication/349054179_Benchmarking_of_Machine_ 

Learning_for_AnomalyBased_Intrusion_Detection_Systems_in_the_CICIDS2017_ 

Dataset  

> 9.

B-Profile.pdf  

> 10.

Network Intrusion Datasets: A Survey, Limitations, and Recommendations - arXiv, 

truy cập vào tháng 4 23, 2026,  https://arxiv.org/html/2502.06688v1  

> 11.

Coldwave96/NET-Analyzer: BiLSTM for Network Intrusion Detection System (NIDS). · GitHub, truy cập vào tháng 4 23, 2026, 

https://github.com/Coldwave96/NET-Analyzer/  

> 12.

Generating Network Intrusion Detection Dataset Based on Real and Encrypted Synthetic Attack Traffic - MDPI, truy cập vào tháng 4 23, 2026, 

https://www.mdpi.com/2076-3417/11/17/7868?type=check_update&version=1  

> 13.

Generating Network Intrusion Detection Dataset Based on Real and Encrypted Synthetic Attack Traffic - MDPI, truy cập vào tháng 4 23, 2026, 

https://www.mdpi.com/2076-3417/11/17/7868  

> 14.

Network Intrusion dataset(CIC-IDS- 2017) - Kaggle, truy cập vào tháng 4 23, 

2026,  https://www.kaggle.com/datasets/chethuhn/network-intrusion-dataset  

> 15.

Intrusion Detection Dataset (BCCC-CIC-IDS2017) - York University, truy cập vào tháng 4 23, 2026, 

https://www.yorku.ca/research/bccc/ucs-technical/cybersecurity-datasets-cds/intru 

sion-detection-dataset-bccc-cic-ids2017/  

> 16.

2.3. Clustering — scikit-learn 1.8.0 documentation, truy cập vào tháng 4 23, 2026, 

https://scikit-learn.org/stable/modules/clustering.html 17.  Profiling Academic Library Patrons using K-means and X-means Clustering, truy 

cập vào tháng 4 23, 2026,  https://ijtech.eng.ui.ac.id/article/view/3440  

> 18.

(PDF) Profiling Academic Library Patrons using K-means and X-means Clustering, truy cập vào tháng 4 23, 2026, 

https://www.researchgate.net/publication/337970603_Profiling_Academic_Library 

_Patrons_using_K-means_and_X-means_Clustering  

> 19.

X-Means — A Complement to the K-Means Clustering Algorithm | by ..., truy cập vào tháng 4 23, 2026, 

https://medium.com/geekculture/x-means-algorithm-a-complement-to-the-k-means 

-algorithm-b087ae88cf88  

> 20.

X-means: Extending K-means with, truy cập vào tháng 4 23, 2026, 

https://web.cs.dal.ca/~shepherd/courses/csci6403/clustering/xmeans.pdf  

> 21.

xmeans - SMILE, truy cập vào tháng 4 23, 2026, 

http://haifengl.github.io/api/kotlin/smile-kotlin/smile.clustering/xmeans.html  

> 22.

An algorithm similar to (or based on) K-means that do not require the 'k' number of clusters, truy cập vào tháng 4 23, 2026, 

https://stats.stackexchange.com/questions/319807/an-algorithm-similar-to-or-base 

d-on-k-means-that-do-not-require-the-k-number  

> 23.

Algorithms in the AI Toolkit | Splunk Enterprise, Splunk Cloud Platform (last updated 2025-12-03T00:52:28.941Z), truy cập vào tháng 4 23, 2026, 

https://help.splunk.com/splunk-enterprise/apply-machine-learning/use-ai-toolkit/5.6 

.4/algorithms-and-scoring-metrics-in-the-ai-toolkit/algorithms-in-the-ai-toolkit  

> 24.

Extending -means with Efficient Estimation of the Number of Clusters Dan Pelleg dpelleg@cs.cmu.edu Andrew Moore awm@cs., truy cập vào tháng 4 23, 2026, 

https://www.cs.cmu.edu/~dpelleg/download/xmeans.pdf  

> 25.

X-Means Clustering Explained - by Alif Arshad Bakshi - Medium, truy cập vào tháng 4 23, 2026, 

https://medium.com/@arshadbakshi/x-means-clustering-explained-e4335a31cf8e  

> 26.

Adaptive Covers for Mapper Graphs Using Information Criteria - Scientific Computing and Imaging Institute, truy cập vào tháng 4 23, 2026, 

https://www.sci.utah.edu/~beiwang/publications/TDA_workshop_xmean_BeiWang 

_2021.pdf  

> 27.

Bayesian information criterion - Wikipedia, truy cập vào tháng 4 23, 2026, 

https://en.wikipedia.org/wiki/Bayesian_information_criterion  

> 28.

machine learning - X-means algorithm and BIC - Cross Validated - Stats StackExchange, truy cập vào tháng 4 23, 2026, 

https://stats.stackexchange.com/questions/169319/x-means-algorithm-and-bic  

> 29.

Bayesian Clustering Factor Models - PMC - NIH, truy cập vào tháng 4 23, 2026, 

https://pmc.ncbi.nlm.nih.gov/articles/PMC12826354/  

> 30.

A measure of distance between time series: Dynamic Time Warping -INFORMS.org, truy cập vào tháng 4 23, 2026, 

https://www.informs.org/Publications/OR-MS-Tomorrow/A-measure-of-distance-be 

tween-time-series-Dynamic-Time-Warping  

> 31.

Does it make sense to use dynamic time warping when clustering time series that all have the same length and sampling interval? - Stats StackExchange, truy cập vào tháng 4 23, 2026, 

https://stats.stackexchange.com/questions/64585/does-it-make-sense-to-use-dyn 

amic-time-warping-when-clustering-time-series-that  

> 32.

An introduction to Dynamic Time Warping - Romain Tavenard, truy cập vào tháng 

4 23, 2026,  https://rtavenar.github.io/blog/dtw.html  

> 33.

Difference between DTW distance and Euclidean distance (green lines... -ResearchGate, truy cập vào tháng 4 23, 2026, 

https://www.researchgate.net/figure/Difference-between-DTW-distance-and-Euclid 

ean-distance-green-lines-represent-mapping_fig4_233751236  

> 34.

Dynamic time warping - Wikipedia, truy cập vào tháng 4 23, 2026, 

https://en.wikipedia.org/wiki/Dynamic_time_warping  

> 35.

Understanding Dynamic Time Warping | Databricks Blog, truy cập vào tháng 4 23, 2026, 

https://www.databricks.com/blog/2019/04/30/understanding-dynamic-time-warping 

.html  

> 36.

DTWNet: a Dynamic Time Warping Network, truy cập vào tháng 4 23, 2026, 

http://papers.neurips.cc/paper/9338-dtwnet-a-dynamic-time-warping-network.pdf  

> 37.

truy cập vào tháng 4 23, 2026, 

https://www.researchgate.net/figure/Difference-between-DTW-distance-and-Euclid 

ean-distance-green-lines-represent-mapping_fig4_233751236#:~:text=Dynamic% 

20Time%20Warping%20(%20DTW%20)%20%5B,one%20(and%20viceversa)%2 

0comparison.  

> 38.

Everything you know about Dynamic Time Warping is Wrong - Computer Science and Engineering, truy cập vào tháng 4 23, 2026, 

https://www.cs.ucr.edu/~eamonn/DTW_myths.pdf  

> 39.

DS-Means: Distributed Data Stream Clustering, truy cập vào tháng 4 23, 2026, 

http://disi.unitn.it/~montreso/pubs/papers/europar12.pdf  

> 40.

DTW averaging allows faster and more accurate classification - Computer Science and Engineering, truy cập vào tháng 4 23, 2026, 

https://www.cs.ucr.edu/~eamonn/ICDM_2014_DTW_average.pdf  

> 41.

Bridging the Gap: A Decade Review of Time-Series Clustering Methods - arXiv, 

truy cập vào tháng 4 23, 2026,  https://arxiv.org/html/2412.20582v1  

> 42.

Classifying Human Movement Using Discrete Fréchet and DTW Distances -Department of Computer Science, truy cập vào tháng 4 23, 2026, 

https://www.cs.tufts.edu/research/geometry/FWCG24/papers/FWCG_24_paper_1 

5.pdf  

> 43.

A Scalable DNN Training Framework for Traffic Forecasting in Mobile Networks, truy cập vào tháng 4 23, 2026, 

https://dspace.networks.imdea.org/bitstream/handle/20.500.12761/1908/authors'% 

20version.pdf?sequence=2  

> 44.

Detecting Malicious Web Crawlers Using Clustering | PDF - Scribd, truy cập vào 

tháng 4 23, 2026,  https://www.scribd.com/document/906683364/Stevanovic-2011  

> 45.

BLADE: Behavior-Level Anomaly Detection Using Network Traffic in Web Services 

- arXiv, truy cập vào tháng 4 23, 2026,  https://arxiv.org/pdf/2511.05193  

> 46.

Detection of Intrusions and Malware, and Vulnerability Assessment: 17th International Conference, DIMVA 2020, Lisbon, Portugal, June 24–26, 2020, Proceedings [1st ed.] 9783030526825, 9783030526832 - DOKUMEN.PUB, truy cập vào tháng 4 23, 2026, 

https://dokumen.pub/detection-of-intrusions-and-malware-and-vulnerability-assess 

ment-17th-international-conference-dimva-2020-lisbon-portugal-june-2426-2020-p 

roceedings-1st-ed-9783030526825-9783030526832.html  

> 47.

Information Retrieval Techniques by Iresh Dhotre | PDF - Scribd, truy cập vào tháng 4 23, 2026, 

https://www.scribd.com/document/624615785/Information-Retrieval-Techniques-b 

y-Iresh-Dhotre  

> 48.

Artificial Intelligence for Security Attacks Detection - WebThesis - Politecnico di Torino, truy cập vào tháng 4 23, 2026, 

https://webthesis.biblio.polito.it/25562/1/tesi.pdf  

> 49.

Robust Anomaly Detection in Network Traffic: Evaluating Machine Learning Models on CICIDS2017 - arXiv, truy cập vào tháng 4 23, 2026, 

https://arxiv.org/pdf/2506.19877  

> 50.

Intrusion Detection (CIC-IDS2017) - GitHub, truy cập vào tháng 4 23, 2026, 

https://github.com/noushinpervez/Intrusion-Detection-CICIDS2017  

> 51.

Intelligent Techniques for Detecting Network Attacks: Review and Research Directions, truy cập vào tháng 4 23, 2026, 

https://pmc.ncbi.nlm.nih.gov/articles/PMC8587628/