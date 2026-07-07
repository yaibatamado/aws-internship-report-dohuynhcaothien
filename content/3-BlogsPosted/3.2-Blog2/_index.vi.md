---
title: "Blog 2"
date: 2026-07-05
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---


# Tạo trải nghiệm xác thực hiệu quả với Amazon Cognito và Authsignal

Trong các ứng dụng số hiện nay, xác thực người dùng là một phần rất quan trọng trong hành trình sử dụng hệ thống. Xác thực giúp bảo vệ tài khoản người dùng, thông tin cá nhân, dữ liệu tài chính và các tài nguyên nhạy cảm khác. Tuy nhiên, bảo mật mạnh đôi khi lại làm trải nghiệm người dùng trở nên phức tạp và khó chịu.

Nhiều ứng dụng sử dụng xác thực đa yếu tố, hay MFA, để tăng cường bảo mật. MFA có thể bao gồm SMS OTP, email OTP, ứng dụng xác thực, sinh trắc học, passkey hoặc khóa bảo mật phần cứng. Mặc dù MFA giúp tăng mức độ bảo vệ, việc bắt buộc người dùng xác thực nhiều lớp ở mọi lần đăng nhập hoặc mọi thao tác có thể tạo ra trải nghiệm không tốt.

Bài viết AWS **“Creating great authentication experiences with Amazon Cognito and Authsignal”** giải thích cách Amazon Cognito và Authsignal có thể kết hợp để tạo ra trải nghiệm xác thực tốt hơn. Ý tưởng chính là cân bằng giữa bảo mật và tính tiện lợi bằng cách sử dụng xác thực thích ứng, tín hiệu rủi ro, xác thực liên tục và các phương thức xác thực linh hoạt.

Thay vì áp dụng cùng một yêu cầu xác thực cho mọi người dùng và mọi tình huống, hệ thống có thể đánh giá rủi ro rồi áp dụng mức xác thực phù hợp vào đúng thời điểm.

## 1. Thách thức của trải nghiệm xác thực

Xác thực có hai mục tiêu thường cạnh tranh với nhau:

- Bảo vệ ứng dụng khỏi truy cập trái phép.
- Giữ trải nghiệm người dùng đơn giản và thuận tiện.

Nếu xác thực quá yếu, kẻ tấn công có thể truy cập vào tài khoản người dùng. Nếu xác thực quá nghiêm ngặt, người dùng thật có thể cảm thấy phiền và rời bỏ ứng dụng. Ví dụ, nếu người dùng phải nhập OTP mỗi lần mở ứng dụng, quy trình sẽ trở nên chậm và lặp lại quá nhiều lần.

Vấn đề này trở nên rõ hơn khi ứng dụng mở rộng. Một hệ thống lớn có thể phục vụ nhiều người dùng trên nhiều thiết bị, vị trí và thói quen sử dụng khác nhau. Một số lần đăng nhập có rủi ro thấp, trong khi một số lần khác lại đáng nghi ngờ. Nếu mọi lần đăng nhập đều bị xem là rủi ro như nhau, hệ thống sẽ tạo ra rào cản không cần thiết.

Cách tiếp cận tốt hơn là đánh giá theo ngữ cảnh. Hệ thống nên đặt ra các câu hỏi:

- Đây có phải thiết bị quen thuộc không?
- Vị trí đăng nhập có bình thường không?
- Hành vi người dùng có quen thuộc không?
- Hành động này có rủi ro thấp hay cao?
- Số tiền giao dịch có bất thường không?
- Người dùng có đang truy cập dữ liệu nhạy cảm không?

Dựa trên các thông tin này, hệ thống có thể quyết định cho người dùng tiếp tục bình thường hoặc yêu cầu thêm một bước xác thực.

## 2. Xác thực thích ứng là gì?

Xác thực thích ứng là chiến lược xác thực thay đổi dựa trên mức độ rủi ro. Thay vì yêu cầu cùng một bước bảo mật cho mọi tình huống, hệ thống phân tích ngữ cảnh và quyết định mức xác thực cần thiết.

Ví dụ, nếu người dùng đăng nhập từ thiết bị quen thuộc, tại vị trí thường dùng và vào thời điểm bình thường, hệ thống có thể cho phép đăng nhập với ít ma sát hơn. Ngược lại, nếu cùng người dùng đó đăng nhập từ thiết bị mới, vị trí bất thường hoặc thời điểm khác thường, hệ thống có thể yêu cầu MFA.

Ví dụ đơn giản:

```text
Đăng nhập rủi ro thấp:
Thiết bị quen + vị trí thường dùng + hành vi bình thường
→ Cho phép truy cập với ít rào cản

Đăng nhập rủi ro cao:
Thiết bị lạ + vị trí bất thường + hành vi không bình thường
→ Yêu cầu xác thực bổ sung
```

Cách tiếp cận này cải thiện cả bảo mật và trải nghiệm người dùng. Người dùng ở tình huống rủi ro thấp không bị làm phiền không cần thiết, còn các tình huống rủi ro cao sẽ được bảo vệ mạnh hơn.

Xác thực thích ứng đặc biệt hữu ích cho các ứng dụng cần bảo mật mạnh nhưng vẫn quan tâm đến tỷ lệ chuyển đổi, giữ chân người dùng và sự hài lòng khi sử dụng.

## 3. Các tín hiệu rủi ro trong xác thực

Tín hiệu rủi ro là những thông tin theo ngữ cảnh giúp hệ thống hiểu một lần xác thực là bình thường hay đáng nghi ngờ. Những tín hiệu này có thể đến từ thiết bị, mạng, hành vi người dùng, thông tin giao dịch hoặc ngữ cảnh ứng dụng.

Các tín hiệu rủi ro phổ biến gồm:

### Tín hiệu thiết bị

Tín hiệu thiết bị giúp xác định người dùng có đang dùng thiết bị quen thuộc hay không. Hệ thống có thể kiểm tra fingerprint của trình duyệt, ID thiết bị, hệ điều hành, loại trình duyệt hoặc lịch sử sử dụng thiết bị.

Nếu người dùng đăng nhập từ thiết bị đã sử dụng nhiều lần trước đó, rủi ro có thể thấp hơn. Nếu người dùng đăng nhập từ thiết bị hoàn toàn mới, hệ thống có thể xem request này là rủi ro cao hơn.

### Tín hiệu vị trí

Tín hiệu vị trí giúp phát hiện các mẫu truy cập bất thường. Ví dụ, nếu người dùng vừa đăng nhập ở Việt Nam rồi vài phút sau lại đăng nhập ở một quốc gia rất xa, hệ thống có thể xem đây là dấu hiệu đáng ngờ.

Trường hợp này thường được gọi là impossible travel. Nó cho thấy tài khoản có thể đã bị xâm nhập hoặc một trong các lần đăng nhập không thuộc về người dùng thật.

### Tín hiệu hành vi

Tín hiệu hành vi bao gồm tốc độ đăng nhập, tần suất đăng nhập, thời điểm truy cập, cách di chuyển trong ứng dụng và các thói quen sử dụng khác. Nếu người dùng thường đăng nhập trong giờ làm việc nhưng đột nhiên đăng nhập nhiều lần lúc nửa đêm, hệ thống có thể tăng điểm rủi ro.

Phân tích hành vi giúp hệ thống xác thực thông minh hơn vì nó không chỉ kiểm tra danh tính tại một thời điểm. Hệ thống còn quan sát cách người dùng thường tương tác với ứng dụng.

### Tín hiệu giao dịch

Một số hành động có mức rủi ro cao hơn các hành động khác. Ví dụ, xem trang thông tin công khai có thể là rủi ro thấp, nhưng đổi mật khẩu, thêm phương thức thanh toán mới hoặc thực hiện giao dịch giá trị lớn là hành động rủi ro cao.

Tín hiệu giao dịch giúp hệ thống quyết định có cần xác thực nâng cấp hay không. Một giao dịch thông thường có thể tiếp tục mà không bị gián đoạn, còn giao dịch có giá trị cao hoặc bất thường có thể yêu cầu xác minh bổ sung.

## 4. Xác thực liên tục sau bước đăng nhập

Một sai lầm phổ biến trong thiết kế xác thực là chỉ kiểm tra danh tính người dùng tại thời điểm đăng nhập. Sau khi người dùng đăng nhập thành công, hệ thống có thể cho phép thực hiện mọi hành động mà không cần xác minh thêm. Điều này có thể gây rủi ro.

Bài viết giải thích ý tưởng xác thực liên tục. Điều này có nghĩa là hệ thống có thể đánh giá rủi ro trong suốt phiên làm việc của người dùng, không chỉ ở lúc đăng nhập.

Đối với hành động rủi ro thấp, người dùng có thể tiếp tục bình thường. Đối với hành động nhạy cảm hoặc rủi ro cao, hệ thống có thể yêu cầu xác thực mạnh hơn.

Ví dụ:

```text
Xem thông tin tài khoản thông thường
→ Không cần xác thực thêm

Đổi mật khẩu
→ Yêu cầu MFA hoặc passkey

Thêm phương thức thanh toán mới
→ Yêu cầu xác thực bổ sung

Truy cập dữ liệu nhạy cảm
→ Yêu cầu xác thực mạnh hơn

Thực hiện giao dịch giá trị cao
→ Yêu cầu step-up authentication
```

Mô hình này tăng cường bảo mật vì hệ thống có thể bảo vệ các hành động quan trọng ngay cả khi người dùng đã đăng nhập. Đồng thời, nó cũng cải thiện trải nghiệm vì người dùng không bị yêu cầu xác thực thêm cho mọi thao tác nhỏ.

## 5. Amazon Cognito là nền tảng định danh

Amazon Cognito được sử dụng để quản lý xác thực và định danh người dùng trong ứng dụng. Dịch vụ này cung cấp user pool, đăng ký, đăng nhập, xác thực bằng token và các khả năng quản lý người dùng.

Trong kiến trúc xác thực, Cognito có thể đóng vai trò là nền tảng định danh. Nó lưu trữ và quản lý tài khoản người dùng, xử lý quy trình đăng nhập ban đầu và phát hành token để ứng dụng sử dụng trong các request.

Amazon Cognito hữu ích vì cung cấp các tính năng định danh được quản lý sẵn, giúp đội ngũ phát triển không cần xây dựng toàn bộ hệ thống xác thực từ đầu. Ứng dụng có thể tích hợp Cognito để xử lý đăng ký, đăng nhập, đặt lại mật khẩu và quản lý phiên đăng nhập an toàn.

Tuy nhiên, yêu cầu xác thực ngày càng phức tạp. Nhiều doanh nghiệp cần xác thực thích ứng, quyết định dựa trên rủi ro, step-up authentication và nhiều phương thức xác thực khác nhau. Đây là nơi Authsignal có thể mở rộng trải nghiệm xác thực.

## 6. Authsignal là bộ phân tích rủi ro và rules engine

Authsignal cung cấp khả năng điều phối xác thực và hỗ trợ quyết định dựa trên rủi ro. Dịch vụ này có thể kết hợp với Amazon Cognito để giúp ứng dụng tạo các luồng xác thực thích ứng và liên tục.

Một tính năng quan trọng là rules engine. Rules engine cho phép quản trị viên cấu hình các luật bảo mật dựa trên ngữ cảnh và yêu cầu kinh doanh. Thay vì viết cứng toàn bộ logic xác thực trong ứng dụng, tổ chức có thể định nghĩa rule linh hoạt hơn.

Ví dụ, quản trị viên có thể tạo các rule như:

```text
Nếu người dùng đăng nhập từ thiết bị mới
→ Yêu cầu MFA

Nếu số tiền giao dịch vượt ngưỡng quy định
→ Yêu cầu xác thực mạnh hơn

Nếu người dùng đổi mật khẩu
→ Yêu cầu step-up authentication

Nếu người dùng dùng thiết bị tin cậy và vị trí rủi ro thấp
→ Cho phép truy cập với ít rào cản
```

Điều này giúp các nhóm không chuyên kỹ thuật linh hoạt hơn vì họ có thể điều chỉnh luật bảo mật mà không cần yêu cầu lập trình viên sửa code mỗi lần.

Authsignal cũng hỗ trợ nhiều phương thức xác thực khác nhau. Tùy theo mức độ rủi ro và ngữ cảnh người dùng, hệ thống có thể chọn OTP, passkey, sinh trắc học hoặc các tùy chọn xác minh khác.

## 7. Amazon Cognito và Authsignal phối hợp như thế nào?

Sự kết hợp giữa Amazon Cognito và Authsignal tạo ra một kiến trúc xác thực mạnh và linh hoạt hơn.

Một luồng đơn giản có thể mô tả như sau:

```text
Người dùng thao tác
→ Amazon Cognito xử lý định danh và phiên người dùng
→ Authsignal đánh giá rủi ro và luật nghiệp vụ
→ Hệ thống quyết định phương thức xác thực cần thiết
→ Người dùng hoàn thành xác minh nếu cần
→ Ứng dụng cho phép hoặc từ chối hành động
```

Amazon Cognito quản lý lớp định danh người dùng, còn Authsignal bổ sung khả năng ra quyết định thích ứng và điều phối xác thực. Nhờ đó, hệ thống có thể cân bằng tốt hơn giữa bảo mật tài khoản và sự tiện lợi cho người dùng.

Sự kết hợp này hữu ích vì không phải mọi hành động của người dùng đều cần cùng một mức bảo mật. Hệ thống có thể đơn giản với các thao tác rủi ro thấp và nghiêm ngặt hơn với các thao tác rủi ro cao.

## 8. Phương thức xác thực và trải nghiệm người dùng

Một trải nghiệm xác thực tốt nên cung cấp nhiều tùy chọn xác minh. Người dùng ở các khu vực khác nhau hoặc nhóm người dùng khác nhau có thể ưa thích các phương thức khác nhau.

Các phương thức xác thực phổ biến gồm:

- SMS OTP
- Email OTP
- Ứng dụng xác thực
- WhatsApp OTP
- Push notification
- Passkeys
- Sinh trắc học
- Khóa bảo mật phần cứng
- Liveness detection

Mỗi phương thức đều có ưu và nhược điểm riêng. SMS OTP quen thuộc nhưng có thể bị ảnh hưởng bởi tấn công SIM swap. Email OTP dễ sử dụng nhưng phụ thuộc vào độ an toàn của tài khoản email. Passkey và sinh trắc học có thể mang lại mức bảo vệ mạnh hơn và trải nghiệm mượt hơn, nhưng mức độ áp dụng còn phụ thuộc vào thiết bị và thói quen người dùng.

Bài viết nhấn mạnh rằng xác thực không nên là một mô hình cố định. Tổ chức cần có khả năng điều chỉnh phương thức xác thực dựa trên rủi ro, chi phí và nhu cầu người dùng.

Ví dụ, doanh nghiệp có thể chọn WhatsApp OTP ở một số khu vực để giảm chi phí hoặc cải thiện khả năng gửi mã. Đối với hành động rủi ro cao, hệ thống có thể yêu cầu phương thức mạnh hơn như passkey, sinh trắc học hoặc khóa bảo mật phần cứng.

![Blog 2](/images/3-Blog/Blog-2.png)

## 9. Lợi ích của xác thực thích ứng và xác thực liên tục

Xác thực thích ứng và xác thực liên tục đem lại nhiều lợi ích quan trọng.

Thứ nhất, chúng giảm ma sát cho người dùng. Người dùng không bị ép thực hiện MFA cho mọi hành động rủi ro thấp. Điều này giúp ứng dụng dễ sử dụng hơn và cải thiện trải nghiệm tổng thể.

Thứ hai, chúng tăng cường bảo mật. Hệ thống có thể yêu cầu xác minh mạnh hơn khi rủi ro cao hơn. Nhờ đó, mức bảo mật được tăng đúng lúc cần thiết.

Thứ ba, chúng hỗ trợ sự linh hoạt trong kinh doanh. Rule có thể được điều chỉnh dựa trên mẫu gian lận, hành vi người dùng, yêu cầu tuân thủ hoặc chính sách doanh nghiệp.

Thứ tư, chúng cải thiện khả năng kiểm soát vận hành. Với rules engine và authentication timeline, quản trị viên có thể theo dõi hoạt động xác thực và cập nhật policy dựa trên dữ liệu sử dụng thực tế.

Cuối cùng, chúng hỗ trợ phòng chống gian lận tốt hơn. Các lần đăng nhập đáng ngờ, thiết bị lạ, vị trí bất thường và giao dịch rủi ro cao có thể tự động kích hoạt xác minh mạnh hơn.

## 10. Bài học chính từ bài viết

Bài học chính từ bài viết là xác thực không nên được thiết kế như một quy trình cố định và cứng nhắc. Một trải nghiệm xác thực tốt cần thay đổi dựa trên ngữ cảnh người dùng, mức độ rủi ro và yêu cầu kinh doanh.

Các bài học quan trọng gồm:

- Bảo mật mạnh không phải lúc nào cũng đồng nghĩa với nhiều rào cản.
- MFA nên được áp dụng thông minh, không nên áp dụng máy móc.
- Risk signals giúp hệ thống quyết định khi nào cần yêu cầu xác thực thêm.
- Xác thực nên tiếp tục sau đăng nhập đối với các hành động nhạy cảm.
- Amazon Cognito có thể cung cấp nền tảng định danh.
- Authsignal có thể cung cấp rule thích ứng và điều phối xác thực.
- Các phương thức xác thực khác nhau nên được chọn theo rủi ro và nhu cầu người dùng.
- Một hệ thống xác thực tốt cần cân bằng bảo mật, trải nghiệm, chi phí và tính linh hoạt.

## 11. Ứng dụng thực tế

Những ý tưởng trong bài viết có thể được áp dụng cho nhiều ứng dụng yêu cầu cả bảo mật mạnh và trải nghiệm người dùng mượt mà. Ví dụ gồm ứng dụng y tế, ngân hàng, thương mại điện tử, nền tảng SaaS quản trị và ứng dụng doanh nghiệp.

Đối với hành động rủi ro thấp, ứng dụng có thể cho phép người dùng tiếp tục mà không cần xác minh thêm. Đối với hành động rủi ro cao, ứng dụng có thể yêu cầu xác thực mạnh hơn. Điều này tạo ra trải nghiệm cân bằng hơn.

Thay vì xem mọi người dùng và mọi thao tác là giống nhau, xác thực thích ứng cho phép hệ thống đưa ra quyết định thông minh hơn. Điều này giúp doanh nghiệp giảm ma sát nhưng vẫn bảo vệ các hành động và dữ liệu nhạy cảm.

Xác thực liên tục cũng rất quan trọng vì bảo mật không nên dừng lại sau khi đăng nhập. Một phiên làm việc có thể trở nên rủi ro về sau, đặc biệt khi người dùng thực hiện các hành động nhạy cảm. Step-up authentication giúp bảo vệ những thời điểm quan trọng này.

## 12. Kết luận

Bài viết này hữu ích vì cho thấy thiết kế xác thực không chỉ là thêm nhiều lớp bảo mật. Điều quan trọng là áp dụng đúng lớp bảo mật vào đúng thời điểm.

Một hệ thống xác thực tốt cần bảo vệ tài khoản nhưng không làm mọi tương tác trở nên khó khăn. Amazon Cognito và Authsignal có thể phối hợp để hỗ trợ mục tiêu này bằng cách kết hợp quản lý định danh, đánh giá rủi ro, ra quyết định dựa trên rule và các phương thức xác thực linh hoạt.

Nhìn chung, bài viết đưa ra một hướng thiết kế thực tế để xây dựng trải nghiệm xác thực tốt hơn. Nó cho thấy trải nghiệm bảo mật tốt nhất không phải lúc nào cũng là trải nghiệm nghiêm ngặt nhất, mà là trải nghiệm có khả năng thích ứng với rủi ro, hành vi người dùng và nhu cầu kinh doanh.

## Link bài viết gốc

AWS Partner Network Blog:  
**Creating great authentication experiences with Amazon Cognito and Authsignal**

https://aws.amazon.com/blogs/apn/creating-great-authentication-experiences-with-amazon-cognito-and-authsignal/

## Câu hỏi thảo luận

Bạn đã từng thiết kế hệ thống xác thực cân bằng giữa bảo mật và trải nghiệm người dùng chưa? Theo bạn, phần thách thức nhất là giảm rào cản đăng nhập cho người dùng bình thường hay tăng cường bảo vệ cho các hành động rủi ro cao?