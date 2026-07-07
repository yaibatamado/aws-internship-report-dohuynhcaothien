---
title: "Worklog Tuần 9"
date: 2026-07-05
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9

* Phân tích phạm vi ứng dụng mobile trong hệ thống SmartHospital P2TB.
* Thiết kế cấu trúc project Flutter và định hướng kết nối backend AWS.
* Xác định các màn hình mobile cần ưu tiên triển khai.

### Công việc đã triển khai

| Hạng mục | Nội dung |
| --- | --- |
| Phân tích phạm vi | Xác định các chức năng mobile: đăng nhập, đăng ký bệnh nhân có CCCD, trang chủ, đặt lịch khám, hồ sơ bệnh án, đơn thuốc, xét nghiệm, hóa đơn và thanh toán. |
| Thiết kế Flutter | Lên cấu trúc thư mục `screens`, `services`, `models`, `widgets`, `providers`, `theme` và API client. |
| Xác thực | Xác định cách mobile đăng nhập bằng Cognito/backend, lưu token an toàn, truyền token khi gọi API và xử lý lỗi hết phiên. |
| Giao diện ban đầu | Thiết kế phong cách UI đồng bộ với website: màu sắc, tiêu đề, nút, card, form và trạng thái loading/empty/error. |
| Thanh toán | Lập kế hoạch xử lý `paymentUrl` VNPay/MoMo trên mobile bằng webview, trình duyệt ngoài hoặc deeplink tùy môi trường kiểm thử. |

### Kết quả đạt được

* Chốt được phạm vi chức năng mobile cho giai đoạn project.
* Có cấu trúc Flutter rõ ràng để triển khai các màn hình chính.
* Xác định được hướng kết nối backend AWS và luồng thanh toán trên mobile.
