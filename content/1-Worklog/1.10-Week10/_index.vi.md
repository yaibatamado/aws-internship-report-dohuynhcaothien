---
title: "Worklog Tuần 10"
date: 2026-07-05
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10

* Khởi tạo ứng dụng Flutter và các màn hình nền tảng.
* Xây dựng API client để gọi backend AWS.
* Hoàn thiện đăng ký bệnh nhân và đặt lịch khám trên mobile.

### Công việc đã triển khai

| Hạng mục | Nội dung |
| --- | --- |
| Màn hình nền tảng | Xây dựng splash/loading, đăng nhập, đăng ký, trang chủ, dashboard bệnh nhân, thông tin cá nhân và menu điều hướng. |
| API client | Cấu hình base URL, header Authorization, xử lý JSON response, lỗi network, lỗi server, lỗi token và dữ liệu rỗng. |
| Đăng ký bệnh nhân | Hoàn thiện form đăng ký với họ tên, email, mật khẩu, số điện thoại, ngày sinh, giới tính, địa chỉ và CCCD. |
| Đặt lịch khám | Lấy danh sách chuyên khoa, bác sĩ, ca khám từ backend; gửi yêu cầu đặt lịch và hiển thị kết quả. |
| Model dữ liệu | Đồng bộ model Patient, Doctor, Appointment, MedicalRecord, Prescription, LabResult, Invoice và Payment với backend. |

### Kết quả đạt được

* Ứng dụng mobile có các màn hình nền tảng và điều hướng chính.
* API client có thể dùng chung cho các màn hình cần dữ liệu backend.
* Luồng đăng ký bệnh nhân và đặt lịch khám đã có nền tảng triển khai.
