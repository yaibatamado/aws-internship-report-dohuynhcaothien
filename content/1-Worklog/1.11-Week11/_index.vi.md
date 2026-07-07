---
title: "Worklog Tuần 11"
date: 2026-07-05
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11

* Xây dựng hồ sơ bệnh án, hóa đơn và thanh toán trên mobile.
* Tích hợp luồng payment URL từ backend.
* Đồng bộ dữ liệu mobile với backend và website.

### Công việc đã triển khai

| Hạng mục | Nội dung |
| --- | --- |
| Hồ sơ bệnh án | Xây dựng màn hình hiển thị mã hồ sơ theo CCCD, thông tin bệnh nhân, danh sách đợt khám, phiếu khám, đơn thuốc, xét nghiệm và sự kiện y tế. |
| Hóa đơn | Xây dựng màn hình hóa đơn chờ thanh toán, hóa đơn đã thanh toán, chi tiết tiền dịch vụ và trạng thái thanh toán. |
| Thanh toán thật | Tích hợp luồng nhận `paymentUrl` từ backend và mở cổng thanh toán VNPay/MoMo bằng webview hoặc trình duyệt ngoài. |
| Màn hình hỗ trợ | Bổ sung các màn hình liên quan như xét nghiệm, giỏ hàng/hóa đơn, phân quyền và các trang còn thiếu để mobile không chỉ là demo tĩnh. |
| Sửa lỗi Flutter | Xử lý lỗi import, model, route, overflow, null-safety, thiếu `await` và widget không rebuild sau khi dữ liệu cập nhật. |

### Kết quả đạt được

* Mobile có màn hình hồ sơ bệnh án và hóa đơn theo dữ liệu backend.
* Luồng thanh toán thật trên mobile được chuẩn bị theo payment URL từ backend.
* Tên endpoint, trường dữ liệu và trạng thái nghiệp vụ được đồng bộ với nhóm backend/frontend.
