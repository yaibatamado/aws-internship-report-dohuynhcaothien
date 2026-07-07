---
title: "Worklog Tuần 12"
date: 2026-07-05
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12

* Kiểm thử toàn bộ ứng dụng mobile với backend AWS đã deploy.
* Kiểm tra đồng bộ dữ liệu giữa mobile và website.
* Chuẩn bị minh chứng và nội dung mô tả đóng góp cá nhân.

### Công việc đã triển khai

| Hạng mục | Nội dung |
| --- | --- |
| Kiểm thử mobile | Kiểm tra đăng nhập, đăng ký, thông tin bệnh nhân, đặt lịch, lịch hẹn, hồ sơ bệnh án, xét nghiệm, đơn thuốc và hóa đơn. |
| Kiểm thử thanh toán | Chọn hóa đơn, mở `paymentUrl`, xử lý kết quả sau thanh toán, reload trạng thái hóa đơn và hiển thị thông báo rõ ràng. |
| Đồng bộ web/mobile | Kiểm tra cùng một tài khoản bệnh nhân thấy cùng thông tin cá nhân, lịch hẹn, hồ sơ bệnh án, hóa đơn và trạng thái thanh toán. |
| Sửa lỗi cuối | Sửa lỗi thiếu trang chủ, layout màn hình nhỏ, button tràn, danh sách rỗng thiếu thông báo và trạng thái loading chưa rõ. |
| Minh chứng báo cáo | Chuẩn bị ảnh/nội dung cho đăng nhập, đăng ký, trang chủ, đặt lịch, hồ sơ bệnh án, hóa đơn/thanh toán và kết nối backend thật. |

### Kết quả đạt được

* Ứng dụng mobile được kiểm thử theo các luồng chính với backend AWS.
* Mobile và website được định hướng hiển thị dữ liệu thống nhất cho cùng bệnh nhân.
* Hoàn thiện mô tả đóng góp của Cao Thiên: chuyển mobile từ demo tĩnh sang ứng dụng kết nối API backend và hỗ trợ chức năng chính.
