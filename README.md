# B-Profile Generator

Dự án này chứa tài liệu và hướng dẫn kỹ thuật chi tiết để xây dựng **B-Profile (Benign Profile - Hồ sơ hành vi lành tính)**. Đây là quy trình cốt lõi được sử dụng để tạo ra các tập dữ liệu benchmark cho Hệ thống Phát hiện Xâm nhập (IDS) như CIC-IDS2017.

## 🎯 Mục tiêu dự án
Việc sử dụng dữ liệu mạng nội bộ thực tế để nghiên cứu thường gặp rào cản về quyền riêng tư (chứa thông tin nhạy cảm), còn việc tự tạo dữ liệu ngẫu nhiên lại thiếu tính chân thực. B-Profile giải quyết bài toán này bằng cách:
1. Phân tích dữ liệu mạng thô (PCAP).
2. Rút trích và gom cụm các thói quen hành vi của người dùng (ví dụ: giờ lướt web, thói quen gửi email).
3. Tính toán ra các "Nguyên mẫu trừu tượng" đại diện cho từng hành vi bằng toán học.

Những nguyên mẫu này sau đó được sử dụng làm khuôn mẫu để máy tự động sinh ra hàng triệu luồng traffic giả lập. Kết quả là ta có một nền tảng dữ liệu mạng sạch, cực kỳ giống người thật, nhưng an toàn 100% về bảo mật thông tin.

## 📁 Cấu trúc Tài liệu

Dự án bao gồm 2 tài liệu chính để bạn có thể nắm bắt trọn vẹn từ lý thuyết đến thực hành:

1. **[`Hướng dẫn tạo B-Profile_By_Gemini.md`](./Hướng%20dẫn%20tạo%20B-Profile_By_Gemini.md)**
   - **Nội dung:** Báo cáo phân tích lý thuyết chuyên sâu.
   - **Tác dụng:** Giúp bạn hiểu rõ bối cảnh lịch sử, nguyên lý hoạt động của CICFlowMeter, và các mô hình toán học ẩn sau hệ thống.

2. **[`Towards a Reliable Intrusion DetectionBenchmark Dataset.md`](./Towards%20a%20Reliable%20Intrusion%20DetectionBenchmark%20Dataset.md)**
   - **Nội dung:** Sổ tay hướng dẫn thực hành từng bước (Step-by-step).
   - **Tác dụng:** Dẫn dắt bạn từ Bước 1 (Tiền xử lý file PCAP) đến Bước 8 (Chốt B-Profile). Các bước phức tạp được chia nhỏ và minh họa cặn kẽ bằng các ma trận số liệu cụ thể và biểu đồ không gian.

3. **`Thư mục Images/`**
   - Chứa các hình ảnh, biểu đồ phân tán (Scatter plot), biểu đồ đường (Line chart) và ma trận (Heatmap) trực quan giúp giải thích các bước biến đổi dữ liệu.

## 🧠 Các Thuật toán Trọng tâm
Quy trình xây dựng B-Profile được vận hành bởi 3 thuật toán cốt lõi (Xem chi tiết tại Bước 6, 7, 8 trong file Hướng dẫn thực hành):
- **DTW (Dynamic Time Warping):** Đo lường khoảng cách giữa các hành vi. Thuật toán này có khả năng "uốn cong" thời gian để khắc phục hiện tượng lệch pha (ví dụ: hôm nay đi làm trễ 30 phút).
- **X-Means kết hợp Tiêu chuẩn BIC:** Tự động dò tìm và chẻ nhỏ các nhóm hành vi để tìm ra số lượng cụm (K) tối ưu nhất, thay vì phải đoán mò như K-Means truyền thống.
- **DBA (DTW Barycenter Averaging):** Kỹ thuật tính trung bình cộng đặc biệt dành riêng cho chuỗi thời gian, giúp tạo ra "Bản thiết kế" đại diện cho mỗi cụm mà không làm mất đi các đỉnh năng lượng quan trọng (spikes).

---
*Tài liệu được biên soạn với tiêu chí "cầm tay chỉ việc", trực quan hóa tối đa bằng số liệu và biểu đồ để bất kỳ ai cũng có thể dễ dàng tiếp cận và triển khai.*
