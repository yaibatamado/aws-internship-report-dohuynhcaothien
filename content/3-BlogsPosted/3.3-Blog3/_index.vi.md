---
title: "Blog 3"
date: 2026-07-05
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Mở rộng hỗ trợ bệnh nhân ung thư: Cách New York Cancer and Blood Specialists nâng cao trải nghiệm khách hàng với AWS và Pronetx, hiện là một phần của Caylent

Trong lĩnh vực y tế, hỗ trợ bệnh nhân không chỉ là một hoạt động chăm sóc khách hàng thông thường. Đây còn là một phần quan trọng trong quá trình cung cấp dịch vụ chăm sóc sức khỏe. Khi bệnh nhân liên hệ với cơ sở y tế, tốc độ phản hồi và độ chính xác của thông tin có thể ảnh hưởng trực tiếp đến trải nghiệm, sự an tâm và trong một số trường hợp là sự an toàn của người bệnh.

Khi các tổ chức y tế mở rộng quy mô, việc quản lý số lượng lớn cuộc gọi của bệnh nhân theo cách thủ công trở nên ngày càng khó khăn. Nhân viên có thể phải xử lý lịch hẹn, câu hỏi y tế, thư thoại khẩn cấp, yêu cầu theo ngôn ngữ khác nhau và định tuyến đến đúng chuyên khoa cùng một lúc. Nếu tổng đài không được thiết kế tốt, bệnh nhân có thể phải chờ lâu, cuộc gọi có thể bị chuyển sai bộ phận và nhân viên y tế dễ bị quá tải.

Bài viết AWS **“Scaling oncology patient support: How New York Cancer and Blood Specialists transformed customer experience with AWS and Pronetx, now part of Caylent”** trình bày một case study thực tế về cách New York Cancer and Blood Specialists, hay NYCBS, cải thiện hệ thống hỗ trợ bệnh nhân bằng các dịch vụ AWS.

NYCBS là một trong những đơn vị cung cấp dịch vụ điều trị ung thư và huyết học lớn tại Mỹ. Để nâng cao trải nghiệm liên lạc của bệnh nhân, NYCBS đã hợp tác với AWS và Pronetx, hiện là một phần của Caylent, để chuyển đổi từ mô hình tổng đài cũ sang kiến trúc tổng đài đám mây sử dụng Amazon Connect.

Giải pháp này không chỉ đơn giản là thay thế hệ thống nghe gọi. Nó kết hợp công nghệ tổng đài cloud, microservices, dịch vụ AI/ML, tự động hóa, định tuyến đa ngôn ngữ và các kiểm soát bảo mật phù hợp với ngành y tế nhằm cải thiện khả năng xử lý cuộc gọi và hỗ trợ bệnh nhân ở quy mô lớn.

## 1. Thách thức khi mở rộng hỗ trợ bệnh nhân

Các tổng đài trong lĩnh vực y tế thường phải xử lý số lượng lớn cuộc gọi từ bệnh nhân. Bệnh nhân có thể gọi để đặt lịch hẹn, hỏi thông tin điều trị, theo dõi kết quả, yêu cầu hỗ trợ đơn thuốc hoặc để lại thư thoại khẩn cấp ngoài giờ làm việc.

Đối với các đơn vị điều trị ung thư, yêu cầu này càng nhạy cảm hơn. Bệnh nhân ung thư có thể cần phản hồi nhanh vì sự chậm trễ có thể ảnh hưởng đến quá trình phối hợp điều trị và tâm lý người bệnh. Một thư thoại bị bỏ sót, một cuộc gọi phản hồi chậm hoặc một lần định tuyến sai có thể tạo áp lực cho bệnh nhân và làm tăng khối lượng công việc cho nhân viên y tế.

Trước khi hiện đại hóa, mô hình tổng đài truyền thống hoặc mô hình multi-tenant cũ có thể không đủ linh hoạt. Hệ thống khó tùy chỉnh workflow, khó tích hợp với các hệ thống y tế, khó tự động xử lý thư thoại và khó ưu tiên các trường hợp khẩn cấp. Khi lưu lượng cuộc gọi tăng, các quy trình thủ công trở thành điểm nghẽn.

Bài viết cho thấy NYCBS cần một giải pháp thông minh và có khả năng mở rộng hơn để hỗ trợ hơn 250.000 cuộc gọi mỗi năm và định tuyến bệnh nhân qua nhiều hàng đợi và chuyên khoa khác nhau.

## 2. Sử dụng Amazon Connect làm nền tảng tổng đài chính

Dịch vụ trung tâm trong kiến trúc này là **Amazon Connect**. Amazon Connect là dịch vụ tổng đài đám mây giúp tổ chức xây dựng các workflow giao tiếp và chăm sóc khách hàng linh hoạt.

Trong case study của NYCBS, tổ chức đã chuyển từ mô hình multi-tenant cũ sang một instance Amazon Connect chuyên dụng. Điều này giúp đơn vị y tế có nhiều quyền kiểm soát hơn, linh hoạt hơn và dễ mở rộng hơn.

Giải pháp hỗ trợ hơn 100 hàng đợi cho các chuyên khoa và nhu cầu hỗ trợ bệnh nhân khác nhau. Các hàng đợi này giúp định tuyến cuộc gọi đến đúng nhóm phụ trách dựa trên các yếu tố như khoa, ngôn ngữ, mức độ khẩn cấp hoặc loại dịch vụ.

Việc sử dụng Amazon Connect mang lại nhiều lợi ích:

- Quản lý tổng đài trên nền tảng cloud
- Định tuyến cuộc gọi linh hoạt
- Dễ tích hợp với các dịch vụ AWS
- Hỗ trợ tự động hóa và các dịch vụ AI
- Dễ mở rộng khi lưu lượng cuộc gọi tăng
- Cải thiện khả năng quan sát hoạt động tổng đài

Thay vì chỉ phụ thuộc vào thao tác định tuyến thủ công, hệ thống có thể sử dụng các flow tự động và quy tắc xử lý để chuyển cuộc gọi hiệu quả hơn.

## 3. Microservice quản lý Contact Trace Record

Một phần quan trọng khác trong kiến trúc là microservice dùng để quản lý **Contact Trace Record**, hay CTR. Contact Trace Record chứa thông tin chi tiết về một tương tác khách hàng, ví dụ như trạng thái cuộc gọi, thông tin định tuyến, thời lượng cuộc gọi và mã kết quả xử lý.

Hệ thống sử dụng các dịch vụ AWS như:

- Amazon API Gateway
- AWS Lambda
- Amazon DynamoDB

Amazon API Gateway cung cấp API endpoint để các thành phần giao tiếp với nhau. AWS Lambda xử lý logic nghiệp vụ mà không cần quản lý máy chủ. Amazon DynamoDB lưu các dữ liệu như disposition codes và thông tin liên quan đến cuộc gọi để truy xuất nhanh.

Cách tiếp cận microservice giúp hệ thống tổng đài linh hoạt hơn. Thay vì đưa toàn bộ logic vào một ứng dụng lớn, từng chức năng có thể được xử lý bởi các dịch vụ cloud nhỏ hơn. Điều này cải thiện khả năng mở rộng, bảo trì và tích hợp với các hệ thống khác.

Ví dụ, khi một cuộc gọi kết thúc, hệ thống có thể ghi nhận kết quả cuộc gọi, lưu disposition code và cung cấp thông tin này cho báo cáo hoặc quy trình xử lý tiếp theo. Nhờ đó, đội ngũ y tế có thể hiểu rõ hơn về các tương tác với bệnh nhân.

## 4. Xử lý thư thoại bằng AI/ML

Một trong những phần thú vị nhất của giải pháp là quy trình xử lý thư thoại bằng AI/ML. Trong các tổng đài truyền thống, nhân viên có thể phải nghe lại từng thư thoại và nhập ghi chú thủ công vào hệ thống. Quy trình này tốn thời gian và dễ phát sinh sai sót.

Trong kiến trúc dựa trên AWS, bản ghi thư thoại được lưu trữ an toàn trong Amazon S3. Khi có thư thoại mới được tải lên, hệ thống có thể kích hoạt một workflow xử lý tự động.

Luồng đơn giản có thể mô tả như sau:

```text
Bệnh nhân để lại thư thoại
→ Bản ghi được lưu trong Amazon S3
→ Amazon Transcribe chuyển giọng nói thành văn bản
→ AWS Lambda xử lý nội dung transcript
→ Case hoặc task được tạo tự động
→ Nhân viên có thể xem và phản hồi nhanh hơn
```

Amazon Transcribe chuyển âm thanh giọng nói thành văn bản. Sau khi thư thoại được chuyển thành transcript, các hàm Lambda có thể xử lý nội dung và tạo case tự động. Điều này giúp giảm nhập liệu thủ công và đảm bảo tin nhắn của bệnh nhân không bị bỏ sót.

Đối với hỗ trợ y tế, đây là điểm rất có giá trị. Một bệnh nhân để lại tin nhắn ngoài giờ có thể được chuyển thành thông tin có thể xử lý trước khi nhân viên nghe lại thủ công. Điều này giúp thông tin được truyền liên tục giữa các ca trực và cho phép nhóm tiếp theo phản hồi nhanh hơn.

## 5. Hội thoại thông minh với Amazon Lex và Amazon Polly

Kiến trúc cũng sử dụng các dịch vụ hội thoại thông minh như **Amazon Lex** và **Amazon Polly**.

Amazon Lex giúp xây dựng giao diện hội thoại và chatbot. Dịch vụ này có thể hiểu ngôn ngữ tự nhiên và hướng dẫn người dùng qua các luồng tương tác. Trong môi trường tổng đài, Lex có thể hỗ trợ xử lý cuộc gọi tự động, cung cấp tùy chọn tự phục vụ và định tuyến thông minh.

Amazon Polly chuyển đổi văn bản thành giọng nói. Điều này hữu ích khi xây dựng các phản hồi giọng nói trong hệ thống IVR. Thay vì phải ghi âm thủ công mọi thông báo, hệ thống có thể tạo giọng nói từ văn bản.

Khi kết hợp, Amazon Lex và Amazon Polly giúp cải thiện lớp tự động hóa của tổng đài.

Một số tình huống sử dụng gồm:

- Tự động chào bệnh nhân
- Hỏi bệnh nhân chọn hoặc mô tả nhu cầu
- Định tuyến cuộc gọi theo ý định
- Cung cấp phản hồi tự động
- Hỗ trợ các câu hỏi phổ biến
- Giảm khối lượng công việc lặp lại cho nhân viên

Các dịch vụ này không thay thế nhân viên y tế. Thay vào đó, chúng hỗ trợ xử lý các tương tác lặp lại và giúp nhân viên tập trung vào những nhu cầu phức tạp hoặc khẩn cấp hơn.

## 6. Định tuyến đa ngôn ngữ và ưu tiên thông minh

Một tính năng quan trọng khác trong case study là định tuyến đa ngôn ngữ. Bệnh nhân có thể muốn giao tiếp bằng nhiều ngôn ngữ khác nhau. Nếu bệnh nhân bị chuyển đến nhóm không hỗ trợ ngôn ngữ của họ, trải nghiệm sẽ trở nên khó chịu và kém hiệu quả.

Giải pháp hỗ trợ định tuyến theo nhiều ngôn ngữ, gồm tiếng Anh, tiếng Tây Ban Nha, tiếng Nga và tiếng Quan Thoại. Điều này giúp bệnh nhân kết nối với đúng nhóm hỗ trợ nhanh hơn.

Hệ thống cũng hỗ trợ ưu tiên theo mức độ khẩn cấp. Trong y tế, không phải cuộc gọi nào cũng có cùng mức độ quan trọng. Một câu hỏi thông thường có thể không cần xử lý ngay, nhưng một vấn đề khẩn cấp liên quan đến điều trị ung thư có thể cần được định tuyến nhanh hơn.

Bằng cách sử dụng ưu tiên hàng đợi và quy tắc định tuyến, hệ thống có thể giúp các ca khẩn cấp được chuyển đến nhân viên phù hợp nhanh hơn. Điều này cải thiện hỗ trợ bệnh nhân và giúp đội ngũ y tế tập trung vào các tương tác quan trọng nhất trước.

Luồng định tuyến đơn giản có thể mô tả như sau:

```text
Nhận cuộc gọi từ bệnh nhân
→ Xác định ngôn ngữ và loại yêu cầu
→ Kiểm tra mức độ khẩn cấp
→ Chuyển đến hàng đợi phù hợp
→ Ưu tiên các ca khẩn cấp
→ Kết nối bệnh nhân với nhân viên phù hợp
```

Kiểu định tuyến thông minh này đặc biệt quan trọng trong y tế vì giao tiếp với bệnh nhân thường có yếu tố thời gian.

## 7. Bảo mật y tế và yêu cầu HIPAA

Vì giải pháp xử lý thông tin liên quan đến y tế, bảo mật và tuân thủ là yếu tố bắt buộc. Các hệ thống y tế có thể xử lý dữ liệu nhạy cảm, bao gồm thông tin cá nhân và thông tin sức khỏe được bảo vệ.

Bài viết nhấn mạnh tầm quan trọng của kiến trúc bảo mật có khả năng đáp ứng các yêu cầu tuân thủ trong y tế như HIPAA. Điều này có nghĩa là dữ liệu phải được bảo vệ ở mọi giai đoạn, bao gồm bản ghi âm, transcript, API call, lưu trữ và quyền truy cập.

Các thực hành bảo mật quan trọng gồm:

- Mã hóa dữ liệu nhạy cảm
- Kiểm soát quyền truy cập chặt chẽ
- Quản lý secret an toàn
- Giám sát hoạt động hệ thống
- Bảo vệ bản ghi âm và transcript
- Sử dụng audit log cho tuân thủ và điều tra

AWS KMS có thể được dùng để mã hóa dữ liệu. AWS Secrets Manager có thể lưu các cấu hình nhạy cảm một cách an toàn. Kiểm soát truy cập và giám sát cũng rất quan trọng để giảm rủi ro truy cập trái phép.

Trong y tế, một sai sót nhỏ trong cấu hình quyền có thể dẫn đến lộ thông tin cá nhân nhạy cảm. Vì vậy, hệ thống tổng đài cloud cần được thiết kế với bảo mật ngay từ đầu.

## 8. Giám sát thời gian thực và chất lượng cuộc gọi

Một tổng đài cần được giám sát liên tục. Ngay cả khi kiến trúc được thiết kế tốt, sự cố vẫn có thể xảy ra. Ví dụ, cuộc gọi có thể bị định tuyến sai, chất lượng mạng có thể giảm hoặc nhân viên có thể gặp vấn đề về âm thanh.

Bài viết đề cập đến nhu cầu giám sát thời gian thực và tích hợp bên thứ ba như Operata để theo dõi hiệu năng tổng đài và chất lượng cuộc gọi.

Giám sát thời gian thực giúp đội ngũ vận hành phát hiện lỗi sớm. Nó có thể cung cấp khả năng quan sát về:

- Chất lượng cuộc gọi
- Hiệu năng hàng đợi
- Trải nghiệm của nhân viên tổng đài
- Sự cố kết nối
- Độ trễ
- Cuộc gọi thất bại hoặc bị bỏ
- Lỗi định tuyến

Đối với nhà cung cấp dịch vụ y tế, việc giám sát này rất quan trọng vì các vấn đề giao tiếp có thể ảnh hưởng trực tiếp đến sự hài lòng của bệnh nhân và hiệu quả vận hành.

## 9. Thời gian triển khai và quy trình thực hiện

Case study cũng cho thấy dạng chuyển đổi này không thể thực hiện ngay lập tức. Dự án cần một quy trình triển khai có cấu trúc và kéo dài khoảng 13 tuần.

Quy trình gồm các giai đoạn như:

- Khám phá yêu cầu
- Lập kế hoạch kiến trúc
- Xây dựng
- Tích hợp
- Kiểm thử
- Acceptance testing
- Triển khai

Điều này rất quan trọng vì hệ thống y tế yêu cầu lập kế hoạch và xác thực cẩn thận. Việc chuyển đổi tổng đài không thể xem là thay thế nhanh một công cụ đơn lẻ. Hệ thống cần được kiểm thử để đảm bảo định tuyến, bảo mật, xử lý thư thoại, hỗ trợ ngôn ngữ và các tích hợp hoạt động chính xác.

Quy trình triển khai có cấu trúc giúp giảm rủi ro gián đoạn dịch vụ và đảm bảo giải pháp cuối cùng đáp ứng yêu cầu vận hành cũng như tuân thủ.

![Blog 3](/images/3-Blog/Blog-3.png)


## 10. Bài học chính từ bài viết

Bài học chính từ bài viết là một tổng đài cloud có thể làm được nhiều hơn việc nhận và chuyển cuộc gọi. Khi kết hợp với các dịch vụ AWS và khả năng AI/ML, nó có thể trở thành một nền tảng hỗ trợ bệnh nhân thông minh.

Các bài học quan trọng gồm:

- Amazon Connect có thể đóng vai trò lõi của tổng đài cloud có khả năng mở rộng.
- API Gateway, Lambda và DynamoDB có thể hỗ trợ quản lý contact record theo hướng microservice.
- Amazon S3 và Amazon Transcribe có thể tự động hóa xử lý thư thoại.
- Amazon Lex và Amazon Polly có thể cải thiện trải nghiệm hội thoại và IVR.
- Định tuyến đa ngôn ngữ giúp tăng khả năng tiếp cận cho nhiều nhóm bệnh nhân.
- Hàng đợi ưu tiên giúp các ca y tế khẩn cấp được xử lý nhanh hơn.
- Yêu cầu bảo mật liên quan đến HIPAA cần được xem xét ngay từ đầu.
- Giám sát thời gian thực là cần thiết để duy trì chất lượng cuộc gọi.
- Infrastructure as Code và CI/CD giúp triển khai đáng tin cậy và cập nhật tính năng trong tương lai.

Case study này cho thấy các dịch vụ cloud có thể cải thiện cả hiệu quả vận hành và trải nghiệm bệnh nhân.

## 11. Ứng dụng thực tế

Những ý tưởng trong bài viết có thể được áp dụng cho nhiều tổ chức y tế và chăm sóc khách hàng. Bất kỳ tổ chức nào phải xử lý số lượng lớn cuộc gọi, thư thoại, yêu cầu hỗ trợ hoặc ca khẩn cấp đều có thể hưởng lợi từ kiến trúc tổng đài cloud.

Trong y tế, cách tiếp cận này đặc biệt hữu ích vì giao tiếp với bệnh nhân thường nhạy cảm và có yếu tố thời gian. Tự động hóa bằng AI/ML có thể giảm khối lượng công việc hành chính, nhưng cần được triển khai cẩn thận với các kiểm soát bảo mật mạnh.

Ví dụ, tự động chuyển thư thoại thành văn bản có thể giúp nhân viên phản hồi nhanh hơn. Định tuyến thông minh có thể kết nối bệnh nhân đến đúng bộ phận. Hỗ trợ đa ngôn ngữ có thể cải thiện khả năng tiếp cận. Ưu tiên hàng đợi có thể giúp các ca khẩn cấp được chú ý sớm hơn.

Tuy nhiên, tự động hóa nên hỗ trợ con người, không thay thế hoàn toàn con người. Trong y tế, sự thấu cảm, đánh giá chuyên môn và kiểm tra của con người vẫn rất cần thiết. Giá trị của AI và cloud automation là giảm các tác vụ lặp lại để nhân viên tập trung vào hoạt động chăm sóc bệnh nhân có giá trị cao hơn.

## 12. Kết luận

Bài viết này hữu ích vì cho thấy cách các dịch vụ AWS có thể chuyển đổi một tổng đài y tế thành hệ thống hỗ trợ bệnh nhân thông minh và có khả năng mở rộng. Amazon Connect cung cấp nền tảng giao tiếp, trong khi các dịch vụ như Lambda, API Gateway, DynamoDB, S3, Transcribe, Lex và Polly bổ sung khả năng tự động hóa và trí tuệ nhân tạo.

Case study của NYCBS chứng minh rằng cloud automation và AI/ML không nhất thiết làm giảm sự thấu cảm trong y tế. Ngược lại, nếu được thiết kế đúng, chúng có thể loại bỏ các công việc hành chính lặp lại và giúp nhân viên y tế phản hồi bệnh nhân nhanh hơn, chính xác hơn.

Đồng thời, bài viết cũng nhắc rằng tự động hóa trong y tế cần được lập kế hoạch cẩn thận. Bảo mật, tuân thủ, giám sát, kiểm thử và khả năng vận hành đều là yếu tố bắt buộc. Một giải pháp thành công cần cân bằng giữa trải nghiệm bệnh nhân, độ tin cậy kỹ thuật và bảo vệ dữ liệu y tế.

## Link bài viết gốc

AWS Architecture Blog:  
**Scaling oncology patient support: How New York Cancer and Blood Specialists transformed customer experience with AWS and Pronetx, now part of Caylent**

https://aws.amazon.com/vi/blogs/architecture/scaling-oncology-patient-support-how-new-york-cancer-and-blood-specialists-transformed-customer-experience-with-aws-and-pronetx-now-part-of-caylent/

## Câu hỏi thảo luận

Bạn đánh giá thế nào về việc đưa AI/ML vào quy trình trực tổng đài và xử lý dữ liệu bệnh nhân trong ngành y tế? Liệu rào cản về bảo mật HIPAA có phải là lý do khiến nhiều doanh nghiệp còn e dè khi áp dụng các công nghệ này?