---
title: "Blog 1"
date: 2026-07-05
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Đơn giản hóa mã hóa đa thuê mục với chiến lược AWS KMS Key tối ưu chi phí

Trong các ứng dụng SaaS hiện đại, bảo vệ dữ liệu là một trong những yêu cầu kiến trúc quan trọng nhất. Một hệ thống SaaS thường phục vụ nhiều khách hàng cùng lúc. Mỗi khách hàng được xem là một tenant riêng, và mỗi tenant đều yêu cầu dữ liệu của mình phải được cô lập với các tenant khác.

Điều này có nghĩa là mặc dù nhiều tenant có thể dùng chung cùng một hạ tầng ứng dụng, dữ liệu của họ vẫn phải được bảo vệ và phân tách rõ ràng. Để làm được điều đó, mã hóa thường được sử dụng như một lớp bảo mật quan trọng. AWS Key Management Service, hay AWS KMS, giúp tổ chức tạo, quản lý và kiểm soát các khóa mã hóa cho workload trên AWS.

Tuy nhiên, thiết kế mã hóa cho hệ thống đa thuê mục không chỉ là bài toán bảo mật. Đây còn là bài toán về chi phí, khả năng mở rộng và vận hành. Nếu thiết kế không hợp lý, chi phí KMS và độ phức tạp quản lý có thể tăng rất nhanh khi số lượng tenant phát triển.

Bài viết AWS **“Simplify multi-tenant encryption with a cost-conscious AWS KMS key strategy”** trình bày cách xây dựng mô hình mã hóa đa thuê mục hiệu quả hơn. Thay vì cấp một KMS Customer Managed Key riêng cho mọi tenant, bài viết đề xuất cách tiếp cận cân bằng hơn bằng cách kết hợp phân tầng tenant, key dùng chung, Encryption Context, chính sách truy cập động, audit log và tối ưu chi phí lưu trữ.

## 1. Thách thức của mã hóa đa thuê mục

Trong hệ thống SaaS đa thuê mục, nhiều khách hàng thường dùng chung hạ tầng như API, database, storage và backend service. Tuy nhiên, dù hạ tầng được dùng chung, dữ liệu khách hàng không được phép dùng chung. Đây là yêu cầu bảo mật cốt lõi: mỗi tenant chỉ được phép truy cập dữ liệu của chính mình.

Một cách tiếp cận phổ biến là tạo riêng một AWS KMS Customer Managed Key cho từng tenant. Cách này đem lại mức cô lập cao vì mỗi tenant có một khóa mã hóa riêng. Tuy nhiên, khi số lượng tenant tăng lên, cách làm này có thể trở nên tốn kém và khó quản lý.

Ví dụ, nếu một nền tảng SaaS chỉ có vài tenant, việc quản lý một KMS Key cho mỗi tenant có thể khá đơn giản. Nhưng khi hệ thống phát triển lên hàng trăm hoặc hàng nghìn tenant, số lượng key, policy, audit log và công việc vận hành cũng tăng theo. Điều này làm tăng chi phí cố định hàng tháng và tạo thêm gánh nặng vận hành.

Bài viết nhấn mạnh rằng một chiến lược mã hóa tốt cần cân bằng ba yếu tố quan trọng:

- Bảo mật và cô lập tenant
- Tối ưu chi phí
- Khả năng mở rộng trong vận hành

Điều này có nghĩa là hệ thống không nên áp dụng duy nhất một mô hình mã hóa cho tất cả tenant. Thay vào đó, chiến lược mã hóa cần được thiết kế dựa trên yêu cầu của từng nhóm tenant, giá trị kinh doanh, yêu cầu tuân thủ và độ nhạy cảm của dữ liệu.

## 2. Chiến lược AWS KMS Key chú trọng chi phí

Khuyến nghị chính của bài viết là sử dụng **chiến lược KMS Key chú trọng chi phí**. Điều này có nghĩa là hệ thống không nên mặc định tạo key riêng cho mọi tenant. Thay vào đó, tenant nên được chia thành nhiều tầng dịch vụ khác nhau.

Đối với khách hàng có giá trị cao như Enterprise hoặc Premium, một KMS Key riêng có thể là cần thiết. Những khách hàng này có thể yêu cầu mức độ cô lập dữ liệu cao hơn, tiêu chuẩn tuân thủ nghiêm ngặt hơn hoặc các thỏa thuận bảo mật riêng. KMS Key riêng giúp đáp ứng tốt hơn những yêu cầu đó.

Đối với khách hàng Standard hoặc Free, mô hình dùng chung KMS Key có thể phù hợp hơn. Những tenant này có thể sử dụng một nhóm KMS Key chung để giảm chi phí và đơn giản hóa quản lý. Hệ thống vẫn có thể bảo vệ dữ liệu tenant bằng các cơ chế bổ sung như Encryption Context.

Chiến lược phân tầng này giúp nhà cung cấp SaaS tránh chi phí không cần thiết nhưng vẫn đảm bảo mức bảo vệ cao cho những khách hàng cần nó. Đồng thời, kiến trúc cũng dễ mở rộng hơn vì số lượng KMS Key không tăng cùng tốc độ với số lượng tenant.

Mô hình đơn giản có thể được mô tả như sau:

```text
Enterprise Tier  → KMS Key riêng cho từng tenant
Standard Tier    → KMS Key dùng chung kết hợp tenant-specific context
Free Tier        → KMS Key dùng chung kết hợp policy kiểm soát truy cập
```

Cách tiếp cận này giúp hệ thống linh hoạt hơn. Thay vì chỉ chọn giữa “một key cho tất cả” hoặc “một key cho mỗi tenant”, kiến trúc có thể sử dụng nhiều chiến lược key khác nhau cho từng nhóm khách hàng.

## 3. Sử dụng Encryption Context để cô lập tenant

Khi nhiều tenant dùng chung một KMS Key, hệ thống vẫn cần ngăn chặn truy cập chéo dữ liệu. Đây là lúc **Encryption Context** trở nên rất quan trọng.

Encryption Context là metadata dạng key-value được gửi đến AWS KMS trong quá trình mã hóa và giải mã. Ví dụ, khi mã hóa dữ liệu cho một tenant, ứng dụng có thể gửi kèm mã định danh tenant vào context.

Ví dụ:

```text
TenantID = tenant-a
```

Khi dữ liệu đã mã hóa được giải mã sau đó, hệ thống phải cung cấp đúng Encryption Context tương ứng. Nếu request sử dụng TenantID khác, thao tác có thể bị từ chối dựa trên các điều kiện policy.

Điều này tạo thêm một lớp cô lập logic. Dù nhiều tenant dùng chung một KMS Key, mỗi thao tác mã hóa và giải mã vẫn có thể được gắn với một tenant cụ thể.

Ví dụ đơn giản:

```text
Tenant A mã hóa dữ liệu với:
TenantID = tenant-a

Tenant B cố gắng giải mã cùng dữ liệu đó với:
TenantID = tenant-b

Request bị từ chối vì Encryption Context không khớp.
```

Cách làm này rất hữu ích trong các hệ thống đa thuê mục vì nó giúp giảm nhu cầu tạo key riêng cho mọi tenant nhưng vẫn duy trì khả năng bảo vệ theo từng tenant.

Encryption Context cũng giúp tăng khả năng truy vết. Vì thông tin context có thể xuất hiện trong log, hệ thống dễ xác định tenant nào liên quan đến một request mã hóa hoặc giải mã cụ thể.

## 4. Giảm gánh nặng vận hành bằng chính sách truy cập động

Một nền tảng SaaS lớn có thể có rất nhiều tenant. Nếu quản trị viên phải tự tạo policy thủ công cho từng tenant, hệ thống sẽ nhanh chóng trở nên khó vận hành. Quản lý policy thủ công cũng làm tăng nguy cơ sai sót do con người.

Bài viết giải thích rằng **dynamic IAM policies** và policy variables có thể giúp giảm gánh nặng này. Với policy động, quyền truy cập có thể được đánh giá dựa trên các giá trị tại thời điểm thực thi, chẳng hạn như mã định danh tenant. Điều này cho phép hệ thống tạo các quy tắc truy cập linh hoạt thay vì duy trì số lượng lớn policy tĩnh.

Ví dụ, thay vì tạo một policy cho Tenant A, một policy khác cho Tenant B và một policy khác nữa cho Tenant C, hệ thống có thể định nghĩa một mẫu policy tái sử dụng để kiểm tra request có thuộc đúng tenant hay không.

Cách tiếp cận này đem lại nhiều lợi ích:

- Giảm số lượng policy cần quản lý
- Giảm nguy cơ lỗi cấu hình thủ công
- Dễ onboard tenant mới
- Dễ mở rộng khi số lượng tenant tăng
- Quy tắc truy cập nhất quán hơn

Thiết kế policy động đặc biệt quan trọng với hệ thống SaaS vì tenant có thể được tạo, cập nhật hoặc xóa thường xuyên. Tự động hóa giúp mô hình bảo mật phát triển cùng với ứng dụng.

## 5. Audit và minh bạch với AWS CloudTrail

Mã hóa thôi là chưa đủ cho một kiến trúc an toàn. Hệ thống cũng cần khả năng quan sát cách các khóa mã hóa được sử dụng. AWS CloudTrail giúp cung cấp khả năng quan sát này bằng cách ghi lại các hành động quan trọng liên quan đến AWS KMS.

CloudTrail có thể ghi log các hoạt động như:

- Tạo key
- Sử dụng key
- Request mã hóa
- Request giải mã
- Thay đổi policy
- Sự kiện bị từ chối truy cập

Những log này rất quan trọng cho kiểm toán bảo mật và tuân thủ. Chúng giúp quản trị viên trả lời các câu hỏi như:

- Ai đã sử dụng một KMS Key cụ thể?
- Dữ liệu được mã hóa hoặc giải mã khi nào?
- Tenant nào liên quan đến request đó?
- Request thành công hay bị từ chối?
- Có mẫu truy cập bất thường nào không?

Đối với nhà cung cấp SaaS, CloudTrail logs cũng có thể hỗ trợ chargeback hoặc phân bổ chi phí. Nếu hệ thống ghi nhận context liên quan đến tenant, doanh nghiệp có thể hiểu cách từng tenant sử dụng tài nguyên và phân bổ chi phí chính xác hơn.

Điều này giúp tăng tính minh bạch và hỗ trợ doanh nghiệp đưa ra quyết định vận hành tốt hơn.

## 6. Tối ưu hiệu năng và chi phí với Amazon EBS gp3

Bài viết cũng đề cập đến Amazon EBS gp3 như một phần trong chiến lược tối ưu hiệu năng và chi phí. Trong một số workload, lưu trữ mã hóa cần cung cấp hiệu năng cao. Tuy nhiên, việc chọn sai loại lưu trữ hoặc cấp phát dư dung lượng có thể làm tăng chi phí.

Amazon EBS gp3 cho phép cấu hình dung lượng lưu trữ và hiệu năng một cách độc lập. Điều này có nghĩa là người dùng có thể chọn dung lượng lưu trữ cần thiết và cấu hình riêng các thông số hiệu năng như IOPS và throughput.

Điều này hữu ích vì có những hệ thống cần hiệu năng cao nhưng không nhất thiết cần dung lượng lưu trữ lớn. Với gp3, tổ chức có thể tránh trả tiền cho dung lượng không cần thiết chỉ để đạt hiệu năng tốt hơn.

Ý chính ở đây là chiến lược mã hóa không nên được thiết kế tách rời khỏi chi phí hạ tầng. Storage, key management, audit logs và access control nên được xem xét cùng nhau khi thiết kế kiến trúc SaaS vừa an toàn vừa tối ưu chi phí.

![Blog 1](/images/3-Blog/Blog-1.png)

## 7. Bài học chính từ bài viết

Bài học quan trọng nhất từ bài viết là mã hóa đa thuê mục cần một thiết kế cân bằng. Bảo mật là quan trọng, nhưng chi phí và vận hành cũng quan trọng không kém.

Nếu mỗi tenant đều có KMS Key riêng, hệ thống có thể trở nên đắt đỏ và khó quản lý. Nếu tất cả tenant dùng chung một key mà không có lớp kiểm soát bổ sung, hệ thống có thể không đủ khả năng cô lập dữ liệu. Vì vậy, cách tiếp cận tốt nhất là kết hợp nhiều kỹ thuật khác nhau.

Các kỹ thuật quan trọng gồm:

- Chia tenant thành các tầng dịch vụ
- Sử dụng KMS Key riêng cho tenant Enterprise
- Sử dụng KMS Key dùng chung cho tenant Standard hoặc Free
- Áp dụng Encryption Context để bảo vệ theo tenant
- Dùng policy động để giảm thao tác thủ công
- Ghi nhận hoạt động KMS bằng CloudTrail
- Tối ưu hiệu năng và chi phí lưu trữ bằng lựa chọn lưu trữ phù hợp

Điều này cho thấy kiến trúc mã hóa cần được thiết kế dựa trên yêu cầu kinh doanh thực tế. Không phải khách hàng nào cũng cần cùng một mô hình bảo mật, và không phải workload nào cũng cần cùng một mức độ cô lập.

## 8. Ứng dụng thực tế

Những ý tưởng trong bài viết có thể được áp dụng cho nhiều hệ thống SaaS cần bảo vệ dữ liệu khách hàng ở quy mô lớn. Một doanh nghiệp cung cấp nền tảng SaaS có thể phục vụ nhiều nhóm khách hàng khác nhau, từ doanh nghiệp nhỏ đến các tổ chức Enterprise lớn. Mỗi nhóm khách hàng có thể có yêu cầu khác nhau về bảo mật, tuân thủ và chi phí.

Đối với khách hàng Enterprise, việc sử dụng KMS Key riêng có thể giúp tăng khả năng cô lập dữ liệu và hỗ trợ tốt hơn cho các yêu cầu tuân thủ. Đối với khách hàng Standard, việc dùng chung KMS Key kết hợp với Encryption Context vẫn có thể đảm bảo phân tách dữ liệu về mặt logic nhưng giúp giảm chi phí.

Điều này cho thấy thiết kế mã hóa không nên áp dụng một mô hình cố định cho tất cả khách hàng, mà cần linh hoạt theo nhu cầu kinh doanh, yêu cầu của tenant và độ nhạy cảm của dữ liệu.

Encryption Context cũng là một kỹ thuật quan trọng vì nó cho phép gắn metadata theo từng tenant vào các thao tác mã hóa và giải mã. Nhờ đó, ngay cả khi nhiều tenant dùng chung một KMS Key, dữ liệu của họ vẫn có thể được phân tách về mặt logic.

Khi kết hợp với CloudTrail logs, hệ thống có thể tăng tính minh bạch, hỗ trợ audit và nâng cao khả năng truy vết. Điều này rất quan trọng với các tổ chức cần chứng minh rằng dữ liệu khách hàng được bảo vệ và truy cập được giám sát đúng cách.

Một điểm thực tế khác là chi phí cloud cần được cân nhắc ngay từ giai đoạn thiết kế kiến trúc. Nếu mỗi tenant đều được cấp một KMS Key riêng mà không có chiến lược rõ ràng, chi phí hàng tháng và độ phức tạp vận hành có thể tăng rất nhanh. Chiến lược quản lý key chú trọng chi phí giúp hệ thống mở rộng hiệu quả hơn.

## 9. Kết luận

Bài viết này hữu ích vì giải thích rằng mã hóa đa thuê mục không chỉ là vấn đề bảo vệ dữ liệu. Đây còn là bài toán thiết kế kiến trúc an toàn, có khả năng mở rộng và tối ưu chi phí.

Bài học quan trọng nhất là các tenant khác nhau có thể cần các mức bảo vệ khác nhau. Chiến lược phân tầng key giúp hệ thống cung cấp mức cô lập cao hơn cho khách hàng Premium, đồng thời giảm chi phí không cần thiết cho nhóm khách hàng Standard.

Encryption Context, policy động, CloudTrail audit và thiết kế lưu trữ chú trọng chi phí là những kỹ thuật quan trọng để xây dựng mô hình mã hóa đa thuê mục hiệu quả hơn. Khi kết hợp các kỹ thuật này, hệ thống có thể tăng cường bảo mật, giảm tải vận hành và kiểm soát chi phí AWS KMS tốt hơn.

Nhìn chung, bài viết đưa ra một hướng thiết kế thực tế cho mã hóa đa thuê mục trên AWS. Nó cho thấy một kiến trúc cloud tốt cần cân bằng giữa bảo mật, chi phí, khả năng mở rộng và sự đơn giản trong vận hành.

## Link bài viết gốc

AWS Architecture Blog:  
**Simplify multi-tenant encryption with a cost-conscious AWS KMS key strategy**

https://aws.amazon.com/vi/blogs/architecture/simplify-multi-tenant-encryption-with-a-cost-conscious-aws-kms-key-strategy/

## Câu hỏi thảo luận

Bạn đã từng thiết kế hệ thống lưu trữ mã hóa cho ứng dụng SaaS đa thuê mục trên AWS chưa? Theo bạn, phần thách thức nhất là đáp ứng tiêu chuẩn cô lập dữ liệu của khách hàng Enterprise hay là tối ưu hóa hóa đơn AWS KMS hàng tháng?