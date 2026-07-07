---
title: "Bản đề xuất"
date: 2026-07-05
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# MedChain AI (Hệ thống bệnh viện AWS Serverless tích hợp Blockchain, AI và thanh toán thật)


### 1. Tóm tắt điều hành

MedChain AI là hệ thống bệnh viện tích hợp Blockchain và AI, được xây dựng trên nền tảng AWS nhằm hỗ trợ các nghiệp vụ số hóa trong bệnh viện như đăng ký bệnh nhân, đặt lịch khám, bác sĩ khám bệnh, quản lý hồ sơ bệnh án, kê đơn thuốc, quản lý xét nghiệm, lập hóa đơn và thanh toán trực tuyến. Hệ thống sử dụng kiến trúc serverless để giảm việc quản trị hạ tầng, dễ mở rộng và phù hợp với quy mô triển khai thực tế trong đồ án.

Nền tảng sử dụng Amazon Cognito để xác thực và phân quyền người dùng, AWS Lambda và API Gateway để xây dựng backend API, Amazon DynamoDB để lưu trữ dữ liệu bệnh viện, Amazon S3 và Amazon CloudFront để triển khai frontend, đồng thời sử dụng Amazon CloudWatch để ghi log và hỗ trợ kiểm tra lỗi. Giao diện web được phát triển bằng React/Vite và triển khai dưới dạng website tĩnh.

Một chức năng quan trọng của MedChain AI là Medical Integrity Ledger, dùng để kiểm tra tính toàn vẹn của hồ sơ bệnh án. Các tài liệu y tế quan trọng như phiếu khám, đơn thuốc, kết quả xét nghiệm, hóa đơn, tài liệu y tế và tóm tắt bệnh án do AI tạo ra sau khi được bác sĩ phê duyệt sẽ được tạo hash và ghi nhận vào ledger. Hệ thống được thiết kế để sử dụng Amazon Managed Blockchain Access Ethereum nhằm neo hash hồ sơ y tế lên blockchain và lưu lại bằng chứng giao dịch như transactionHash, blockNumber, blockchainStatus và thời gian xác nhận.

Thành phần AI được sử dụng để hỗ trợ quy trình y tế, đặc biệt là hỗ trợ tóm tắt thông tin bệnh án và giúp bác sĩ xem lại lịch sử bệnh nhân nhanh hơn. Nội dung do AI tạo ra không được xem là kết luận y khoa cuối cùng. Các tóm tắt AI cần được bác sĩ kiểm tra và phê duyệt trước khi liên kết chính thức vào hồ sơ bệnh án.

Ngoài ra, hệ thống tích hợp thanh toán thật thông qua VNPay/MoMo. Bệnh nhân có thể thanh toán hóa đơn viện phí qua cổng thanh toán, trong khi backend xử lý tạo URL thanh toán, nhận return URL, xác thực IPN/callback, kiểm tra giao dịch, cập nhật trạng thái hóa đơn và lưu lịch sử thanh toán.

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại

Các quy trình quản lý bệnh viện truyền thống thường phụ thuộc nhiều vào giấy tờ, thao tác thủ công và dữ liệu phân tán giữa nhiều bộ phận. Điều này có thể gây ra các vấn đề như:

- Thông tin bệnh nhân, hồ sơ bệnh án, đơn thuốc, xét nghiệm và hóa đơn không được đồng bộ.
- Bệnh nhân khó tự đặt lịch khám, xem hồ sơ bệnh án hoặc theo dõi trạng thái thanh toán trực tuyến.
- Bác sĩ mất thời gian tra cứu lịch sử khám bệnh và các tài liệu y tế liên quan.
- Nhân sự y tế cần một hệ thống tập trung để hỗ trợ lịch hẹn, xét nghiệm, hóa đơn và vận hành bệnh viện.
- Quản trị viên cần nền tảng an toàn để quản lý người dùng, bác sĩ, nhân sự, bệnh nhân, khoa, dịch vụ, thuốc, tin tức và phản hồi.
- Hồ sơ bệnh án là dữ liệu nhạy cảm nên cần cơ chế kiểm tra nếu dữ liệu bị sửa đổi trái phép.
- Thanh toán cần được liên kết với hóa đơn và trạng thái lịch hẹn để hoàn thành quy trình khám bệnh.
- Nội dung do AI tạo ra cần được kiểm soát và phê duyệt bởi bác sĩ trước khi sử dụng chính thức.

#### Giải pháp đề xuất

MedChain AI đề xuất xây dựng một hệ thống bệnh viện AWS serverless nhằm tập trung hóa dữ liệu và các quy trình nghiệp vụ. Người dùng truy cập hệ thống thông qua domain CloudFront. Amazon Cognito xử lý xác thực và phân nhóm người dùng thành Admin, Bác sĩ, Nhân sự y tế và Bệnh nhân. Sau khi đăng nhập, frontend gọi các API được bảo vệ thông qua API Gateway, còn AWS Lambda xử lý nghiệp vụ phía backend.

DynamoDB được sử dụng làm cơ sở dữ liệu chính theo mô hình single-table design. Hệ thống lưu các dữ liệu như người dùng, bệnh nhân, bác sĩ, nhân sự y tế, khoa, lịch hẹn, hồ sơ bệnh án, phiếu khám, đơn thuốc, kết quả xét nghiệm, hóa đơn, giao dịch thanh toán, tin tức, phản hồi, tóm tắt AI và các block của Medical Integrity Ledger. Amazon S3 lưu frontend tĩnh và có thể mở rộng để lưu tài liệu y tế hoặc file upload. CloudWatch hỗ trợ ghi log Lambda và kiểm tra lỗi trong quá trình triển khai.

Đối với quản lý hồ sơ bệnh án, MedChain AI sử dụng CCCD làm mã hồ sơ bệnh án chính. Điều này giúp mỗi bệnh nhân có một hồ sơ nhất quán và giảm tình trạng trùng lặp hoặc sai lệch dữ liệu. Phiếu khám, đơn thuốc, kết quả xét nghiệm, hóa đơn và tóm tắt AI đã được phê duyệt đều được liên kết về cùng một mã hồ sơ bệnh án.

Đối với blockchain, hệ thống tạo hash SHA-256 cho các tài liệu y tế quan trọng và ghi nhận vào Medical Integrity Ledger. Khi bật AMB, các hash được chọn sẽ được neo lên Ethereum thông qua Amazon Managed Blockchain Access Ethereum. Chỉ hash và metadata tối thiểu được gửi lên blockchain. Dữ liệu bệnh án thật vẫn được lưu trong DynamoDB hoặc S3.

Đối với AI, hệ thống hỗ trợ tạo tóm tắt bệnh án nhằm giúp bác sĩ xem lại lịch sử bệnh nhân nhanh hơn. Tóm tắt AI cần được bác sĩ phê duyệt trước khi trở thành một phần chính thức của hồ sơ bệnh án.

Đối với thanh toán thật, hệ thống tích hợp VNPay/MoMo. Backend tạo yêu cầu thanh toán, chuyển hướng bệnh nhân đến cổng thanh toán, xác thực callback hoặc IPN trả về, cập nhật trạng thái hóa đơn, lưu mã giao dịch và ghi nhận lịch sử thanh toán.

#### Lợi ích và hoàn vốn đầu tư

MedChain AI giúp số hóa quy trình bệnh viện và giảm phụ thuộc vào thao tác thủ công. Bệnh nhân có thể đặt lịch khám, xem hồ sơ bệnh án, theo dõi hóa đơn và thanh toán trực tuyến. Bác sĩ có thể xem lịch sử bệnh án, lập phiếu khám, kê đơn thuốc, yêu cầu xét nghiệm và phê duyệt tóm tắt AI. Nhân sự y tế có thể hỗ trợ xét nghiệm, hóa đơn và các nghiệp vụ vận hành. Quản trị viên có thể quản lý dữ liệu hệ thống và tài khoản người dùng từ một giao diện tập trung.

Về mặt kỹ thuật, dự án giúp thực hành nhiều thành phần quan trọng của AWS như kiến trúc serverless, xác thực an toàn, phát triển API, mô hình dữ liệu NoSQL, triển khai frontend, tích hợp thanh toán thật, hỗ trợ AI trong quy trình y tế và kiểm tra toàn vẹn dữ liệu bằng blockchain.

Thành phần blockchain giúp tăng độ tin cậy của dữ liệu y tế bằng cách lưu hash của các hồ sơ quan trọng. Nếu dữ liệu bị sửa trực tiếp trong database mà không thông qua luồng hệ thống, hệ thống có thể tính lại hash và so sánh với giá trị đã lưu trong ledger để phát hiện thay đổi trái phép.

Thành phần AI giúp tăng hiệu quả xử lý thông tin bệnh án, nhưng bác sĩ vẫn là người phê duyệt cuối cùng để đảm bảo an toàn và trách nhiệm y khoa.

Việc tích hợp thanh toán thật giúp hệ thống gần với mô hình bệnh viện thực tế hơn vì hóa đơn được liên kết với giao dịch thanh toán, callback xác thực và trạng thái thanh toán.

### 3. Kiến trúc giải pháp

MedChain AI sử dụng kiến trúc AWS serverless. Frontend được xây dựng bằng React/Vite và triển khai lên Amazon S3 dưới dạng static files. Amazon CloudFront phân phối website qua HTTPS và cải thiện tốc độ truy cập. Người dùng đăng nhập bằng Amazon Cognito. Sau khi đăng nhập, frontend gửi request kèm JWT token đến API Gateway. API Gateway chuyển request đến các AWS Lambda, sau đó Lambda đọc hoặc ghi dữ liệu vào DynamoDB.

DynamoDB lưu dữ liệu bệnh viện chính theo mô hình single-table design. Hệ thống cũng lưu các block của Medical Integrity Ledger trong DynamoDB và lưu thông tin giao dịch blockchain sau khi neo hash thông qua Amazon Managed Blockchain. AWS Secrets Manager được dùng để lưu các cấu hình nhạy cảm như thông tin thanh toán, AMB RPC endpoint và private key. CloudWatch được sử dụng để ghi log backend và hỗ trợ kiểm tra lỗi.

Luồng AI được xử lý thông qua backend service. Dữ liệu y tế được lấy từ DynamoDB, xử lý thành bản tóm tắt an toàn, sau đó bác sĩ xem xét và phê duyệt trước khi lưu vào hồ sơ bệnh án chính thức. Các tóm tắt AI đã được phê duyệt cũng có thể được đưa vào Medical Integrity Ledger để kiểm tra toàn vẹn.

![MedChain AI AWS Architecture](/images/2-Proposal/architecture.png)


#### Dịch vụ AWS sử dụng

- **Amazon Cognito**: Quản lý xác thực người dùng và phân quyền theo vai trò Admin, Bác sĩ, Nhân sự y tế và Bệnh nhân.
- **Amazon API Gateway / HTTP API**: Cung cấp các API endpoint bảo mật cho frontend.
- **AWS Lambda**: Xử lý nghiệp vụ backend như người dùng, lịch hẹn, hồ sơ bệnh án, đơn thuốc, xét nghiệm, hóa đơn, thanh toán, tóm tắt AI và xác thực ledger.
- **Amazon DynamoDB**: Lưu trữ dữ liệu bệnh viện theo mô hình single-table design.
- **Amazon S3**: Lưu frontend tĩnh và tài liệu y tế hoặc file upload.
- **Amazon CloudFront**: Phân phối website frontend qua HTTPS và caching.
- **Amazon CloudWatch**: Ghi log, hỗ trợ giám sát, kiểm tra lỗi và xác thực hệ thống.
- **AWS Secrets Manager**: Lưu các cấu hình nhạy cảm như thông tin VNPay/MoMo, AMB endpoint và private key blockchain.
- **Amazon Managed Blockchain Access Ethereum**: Neo hash hồ sơ y tế lên Ethereum và cung cấp bằng chứng giao dịch blockchain.
- **AI Processing Module**: Hỗ trợ tạo tóm tắt bệnh án và yêu cầu bác sĩ phê duyệt trước khi lưu chính thức.
- **VNPay/MoMo Payment Gateway**: Xử lý thanh toán hóa đơn thật thông qua cổng thanh toán bên ngoài.
- **AWS Root/Admin Account**: Được sử dụng như tài khoản quản trị cao nhất để tạo, triển khai và quản lý toàn bộ tài nguyên AWS trong môi trường workshop.

#### Thiết kế thành phần

- **Ứng dụng frontend**: Ứng dụng React/Vite có giao diện riêng cho Admin, Bác sĩ, Nhân sự y tế và Bệnh nhân.
- **Lớp xác thực**: Amazon Cognito xác thực người dùng và phân nhóm theo vai trò.
- **Lớp API**: API Gateway nhận request từ frontend và chuyển đến Lambda tương ứng.
- **Lớp xử lý nghiệp vụ**: AWS Lambda xử lý đặt lịch, khám bệnh, kê đơn, xét nghiệm, hóa đơn, thanh toán, phê duyệt tóm tắt AI và xác thực ledger.
- **Lớp dữ liệu**: DynamoDB lưu dữ liệu có cấu trúc của bệnh viện, S3 lưu frontend tĩnh và tài liệu y tế.
- **Lớp AI**: Tạo tóm tắt bệnh án từ dữ liệu y tế và yêu cầu bác sĩ phê duyệt trước khi lưu chính thức.
- **Lớp thanh toán**: VNPay/MoMo xử lý tạo yêu cầu thanh toán, return URL, xác thực IPN/callback và cập nhật hóa đơn.
- **Medical Integrity Ledger**: Tạo hash cho các tài liệu y tế quan trọng và lưu các block ledger.
- **Lớp neo blockchain**: Amazon Managed Blockchain Access Ethereum neo các hash được chọn lên Ethereum và lưu transactionHash, blockNumber, blockchainStatus.
- **Lớp giám sát**: CloudWatch Logs giúp kiểm tra lỗi API, kết quả chạy Lambda và các vấn đề tích hợp.

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

Dự án được triển khai qua bốn giai đoạn chính:

1. **Phân tích yêu cầu và thiết kế kiến trúc**  
   Phân tích quy trình nghiệp vụ bệnh viện, xác định vai trò người dùng, thiết kế kiến trúc AWS và lựa chọn các dịch vụ cần thiết cho xác thực, API, lưu trữ dữ liệu, hosting frontend, hỗ trợ AI, thanh toán và blockchain.

2. **Xây dựng hạ tầng AWS và backend lõi**  
   Sử dụng AWS CDK để triển khai Cognito, API Gateway, Lambda, DynamoDB, S3, CloudFront, IAM Role, CloudWatch Logs và các cấu hình môi trường. Phát triển các API đầu tiên cho hồ sơ người dùng, bệnh nhân, bác sĩ, lịch hẹn và hồ sơ bệnh án.

3. **Hoàn thiện nghiệp vụ y tế, AI, thanh toán và blockchain**  
   Triển khai quy trình hồ sơ bệnh án, chuẩn hóa CCCD làm mã hồ sơ bệnh án chính, xây dựng Medical Integrity Ledger, thiết kế neo hash lên AMB, hỗ trợ tạo tóm tắt AI và tích hợp luồng thanh toán thật VNPay/MoMo.

4. **Kiểm thử, triển khai và xác thực cuối**  
   Deploy backend và frontend, seed và kiểm tra dataset, kiểm thử phân quyền người dùng, kiểm tra hiển thị hồ sơ bệnh án, kiểm tra phê duyệt tóm tắt AI, xác thực ledger, kiểm tra callback thanh toán và chuẩn bị tài liệu cuối.

#### Yêu cầu kỹ thuật

- **Frontend**: React, Vite, Axios, routing theo vai trò, giao diện responsive.
- **Backend**: Node.js Lambda, AWS SDK, tích hợp API Gateway.
- **Xác thực**: Amazon Cognito User Pool, JWT token, Cognito groups.
- **Cơ sở dữ liệu**: DynamoDB single-table design với partition key và sort key.
- **Lưu trữ**: S3 cho frontend tĩnh và tài liệu y tế.
- **Phân phối nội dung**: CloudFront cho truy cập frontend.
- **Triển khai**: AWS CDK, AWS CLI, PowerShell scripts, S3 sync, CloudFront invalidation.
- **AI**: Tạo tóm tắt bệnh án với cơ chế bác sĩ phê duyệt.
- **Thanh toán**: VNPay/MoMo payment flow với return URL và IPN/callback.
- **Blockchain**: Medical Integrity Ledger và AMB Access Ethereum.
- **Bảo mật**: IAM Role, Secrets Manager, Cognito authorization và nguyên tắc least privilege.
- **Giám sát**: CloudWatch Logs để debug Lambda và xác thực hệ thống.

### 5. Lộ trình & Mốc triển khai

- **Tuần 1 - Lên kế hoạch và thiết kế kiến trúc**  
  Phân tích yêu cầu dự án, xác định quy trình bệnh viện, thiết kế kiến trúc AWS và lập kế hoạch vai trò người dùng, cơ sở dữ liệu, AI, thanh toán và blockchain.

- **Tuần 2 - Thiết lập hạ tầng và hệ thống lõi**  
  Triển khai hạ tầng AWS bằng CDK, cấu hình Cognito, API Gateway, Lambda, DynamoDB, S3, CloudFront và đưa frontend lên AWS.

- **Tuần 3 - Hồ sơ bệnh án, AI, thanh toán và blockchain**  
  Chuẩn hóa hồ sơ bệnh án theo CCCD, xây dựng Medical Integrity Ledger, thiết kế AMB transaction anchoring, chuẩn bị hỗ trợ tóm tắt AI và triển khai luồng thanh toán VNPay/MoMo.

- **Tuần 4 - Kiểm thử và hoàn thiện**  
  Kiểm thử production deployment, reset và verify dataset, backfill ledger, kiểm tra blockchain validation, rà soát phê duyệt AI summary, kiểm tra callback thanh toán và hoàn thiện tài liệu.

### 6. Ước tính ngân sách

Chi phí cuối cùng phụ thuộc vào số lượng request, dung lượng dữ liệu lưu trữ, lưu lượng CloudFront, mức sử dụng AI, số lần kiểm thử thanh toán và mức độ sử dụng AMB. Chi phí cần được kiểm tra lại bằng AWS Pricing Calculator trước khi triển khai chính thức.

#### Chi phí hạ tầng

- **AWS Lambda**: Phụ thuộc vào số lượng request và thời gian chạy.
- **API Gateway / HTTP API**: Phụ thuộc vào số lượng request API.
- **DynamoDB**: Phụ thuộc vào dung lượng lưu trữ và số lượng read/write request.
- **Amazon S3**: Phụ thuộc vào dung lượng frontend, tài liệu y tế và số request.
- **Amazon CloudFront**: Phụ thuộc vào dữ liệu truyền tải và số request.
- **Amazon Cognito**: Phù hợp với số lượng người dùng nhỏ trong phạm vi demo.
- **CloudWatch Logs**: Phụ thuộc vào dung lượng log và thời gian lưu log.
- **Secrets Manager**: Phát sinh chi phí nếu lưu secret cho thanh toán và blockchain.
- **Amazon Managed Blockchain**: Có thể phát sinh chi phí nếu dùng Ethereum Mainnet node, token accessor hoặc nhiều request.
- **AI Processing**: Phụ thuộc vào nhà cung cấp AI, số request và lượng văn bản y tế được xử lý.
- **VNPay/MoMo**: Kiểm thử sandbox thường không phát sinh phí giao dịch, còn thanh toán thật phụ thuộc vào cấu hình merchant và chính sách nhà cung cấp.

Với phạm vi đồ án, hệ thống nên sử dụng dataset nhỏ, số lượng tài khoản giới hạn, thời gian lưu log ngắn, kiểm soát mức sử dụng AI và kiểm soát kỹ việc sử dụng AMB. Nếu dùng Ethereum Mainnet, nhóm cần theo dõi chi phí request và phí gas có thể phát sinh.

### 7. Đánh giá rủi ro

#### Ma trận rủi ro

- **Không đồng bộ hồ sơ bệnh án**: Ảnh hưởng cao, xác suất trung bình.  
  Các module có thể dùng mã hồ sơ khác nhau nếu không chuẩn hóa CCCD.

- **Sai phân quyền người dùng**: Ảnh hưởng cao, xác suất trung bình.  
  Người dùng có thể truy cập dữ liệu ngoài phạm vi vai trò nếu backend không kiểm tra quyền đầy đủ.

- **Rủi ro nội dung AI**: Ảnh hưởng cao, xác suất trung bình.  
  Tóm tắt AI có thể chưa đầy đủ hoặc chưa chính xác nếu không được bác sĩ kiểm tra.

- **Lỗi callback thanh toán**: Ảnh hưởng cao, xác suất trung bình.  
  Trạng thái hóa đơn có thể không cập nhật đúng nếu return URL hoặc IPN xác thực sai.

- **Lỗi xác thực blockchain**: Ảnh hưởng trung bình, xác suất trung bình.  
  Ledger có thể báo invalid nếu reset dataset nhưng chưa xóa và backfill ledger lại.

- **Lộ dữ liệu nhạy cảm**: Ảnh hưởng cao, xác suất thấp.  
  Dữ liệu bệnh án thật không được lưu trực tiếp trên blockchain hoặc trả về qua API công khai.

- **Vượt chi phí AWS**: Ảnh hưởng trung bình, xác suất trung bình.  
  AMB, CloudWatch Logs, CloudFront, AI usage, WAF và Ethereum transaction có thể tạo chi phí ngoài dự kiến.

#### Chiến lược giảm thiểu

- Sử dụng CCCD làm mã hồ sơ bệnh án duy nhất.
- Áp dụng Cognito groups và kiểm tra phân quyền ở backend.
- Lưu thông tin nhạy cảm trong AWS Secrets Manager.
- Không lưu dữ liệu bệnh án thật trực tiếp lên Ethereum.
- Yêu cầu bác sĩ phê duyệt tóm tắt AI trước khi lưu vào hồ sơ bệnh án chính thức.
- Xác thực chữ ký VNPay/MoMo và số tiền thanh toán trước khi cập nhật hóa đơn.
- Xóa và tạo lại ledger sau khi reset dataset.
- Dùng CloudWatch Logs để kiểm tra lỗi và đặt thời gian lưu log hợp lý.
- Thiết lập AWS Budget alerts để theo dõi chi phí.

#### Kế hoạch dự phòng

- Nếu chưa dùng được thanh toán thật, dùng sandbox VNPay/MoMo để kiểm thử nhưng vẫn giữ đúng cấu trúc luồng thanh toán thật.
- Nếu chi phí AMB quá cao, giữ Medical Integrity Ledger trong DynamoDB và chỉ bật AMB cho một số giao dịch minh họa.
- Nếu kết quả AI chưa đáng tin cậy, giới hạn AI ở mức bản nháp và yêu cầu bác sĩ phê duyệt.
- Nếu CloudFront vẫn hiển thị bản frontend cũ, thực hiện invalidation và xóa cache trình duyệt.
- Nếu dataset sai, reset và verify lại dataset bằng script.
- Nếu blockchain validation báo invalid sau reset, xóa ledger cũ và chạy backfill ledger lại.

### 8. Kết quả kỳ vọng

#### Cải tiến kỹ thuật

Dự án kỳ vọng xây dựng được một hệ thống bệnh viện AWS serverless hoàn chỉnh với xác thực người dùng, phân quyền theo vai trò, quản lý hồ sơ bệnh án, đặt lịch khám, đơn thuốc, xét nghiệm, hóa đơn, thanh toán thật, tóm tắt bệnh án bằng AI và kiểm tra toàn vẹn hồ sơ bệnh án.

Hệ thống thể hiện cách kết hợp nhiều dịch vụ AWS để xây dựng một ứng dụng y tế thực tế. Đồng thời, dự án chứng minh cách sử dụng blockchain một cách phù hợp bằng cách chỉ lưu hash và metadata, không lưu dữ liệu bệnh án nhạy cảm trực tiếp lên blockchain. AI được sử dụng để hỗ trợ bác sĩ, không thay thế quyết định y khoa.

#### Giá trị dài hạn

MedChain AI có thể được mở rộng thành một hệ thống bệnh viện hoàn chỉnh hơn trong tương lai. Các hướng phát triển tiếp theo gồm tích hợp VNPay/MoMo production đầy đủ, nâng cấp tóm tắt bệnh án bằng AI, hỗ trợ gợi ý y khoa cho bác sĩ, gửi thông báo SMS/email, xây dựng dashboard phân tích dữ liệu, tích hợp mobile app và tăng cường blockchain anchoring bằng smart contract.