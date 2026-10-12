# Acceptance Criteria & Definition of Done – Tính năng "Mượn sách trực tuyến"

**Họ tên:** Nguyễn Tấn Du  **MSSV:** N25DTCN011  **Môn:** IT206 – Software Development Process using Agile/Scrum

---

## 1. Giả định chung

- **Giả định:** Mỗi độc giả được mượn tối đa **5 cuốn** cùng lúc (tính cả sách đang mượn và sách đang được giữ chỗ chờ nhận).
- **Giả định:** Thời gian giữ sách là **48 giờ**, tính từ lúc đặt mượn (Story 1) hoặc từ lúc nhận thông báo sách đã có sẵn (Story 2).
- **Giả định:** Thông báo được gửi qua **email** và hiển thị trong **tài khoản** của độc giả, trong vòng **5 phút** kể từ khi sách có sẵn.
- **Giả định:** Độc giả đặt trước theo hàng chờ, ai đặt trước được ưu tiên trước (FIFO).

---

## 2. Bảng Acceptance Criteria

### Story 1 – Đặt mượn online một cuốn sách đang có sẵn

| Story | AC# | Loại | Given | When | Then |
|---|---|---|---|---|---|
| 1 | 1.1 | Happy | Độc giả đã đăng nhập, cuốn "Lập trình Python" còn ít nhất 1 bản có sẵn, và độc giả chưa đạt giới hạn mượn | Độc giả chọn "Đặt mượn" cho cuốn này | Hiển thị thông báo "Đặt mượn thành công", trạng thái đặt mượn là "Chờ nhận" **And** hiển thị hạn nhận sách là 48 giờ kể từ lúc đặt **And** số bản có sẵn của cuốn sách giảm đi 1 |
| 1 | 1.2 | Negative | Cuốn "Lập trình Python" có 0 bản có sẵn | Độc giả chọn "Đặt mượn" cho cuốn này | Hệ thống từ chối, hiển thị "Sách hiện không còn bản có sẵn" **And** không tạo đặt mượn nào cho độc giả |
| 1 | 1.3 | Negative | Độc giả đã có một đặt mượn đang "Chờ nhận" cho cuốn "Lập trình Python" | Độc giả chọn "Đặt mượn" cho cùng cuốn này lần nữa | Hệ thống từ chối, hiển thị "Bạn đã đặt mượn cuốn này rồi" **And** số bản có sẵn không thay đổi |
| 1 | 1.4 | Edge | Cuốn "Lập trình Python" chỉ còn đúng 1 bản, và độc giả A vừa đặt mượn thành công bản đó | Độc giả B chọn "Đặt mượn" cho cùng cuốn ngay sau đó | Độc giả B bị từ chối với thông báo "Sách hiện không còn bản có sẵn" **But** đặt mượn của độc giả A vẫn giữ nguyên trạng thái "Chờ nhận" |
| 1 | 1.5 | Edge | Độc giả đã đặt mượn thành công và đang ở trạng thái "Chờ nhận" | Đủ 48 giờ kể từ lúc đặt mà độc giả chưa đến nhận | Đặt mượn chuyển sang trạng thái "Đã hết hạn" **And** sách trở lại trạng thái có sẵn cho độc giả khác |

### Story 2 – Nhận thông báo khi sách đặt trước đã có sẵn

| Story | AC# | Loại | Given | When | Then |
|---|---|---|---|---|---|
| 2 | 2.1 | Happy | Độc giả đã đặt trước cuốn đang hết bản và đang đứng **đầu hàng chờ** | Một bản của cuốn này được trả lại thư viện | Độc giả nhận thông báo trong vòng 5 phút, nêu rõ tên sách và hạn nhận (48 giờ) **And** bản sách được giữ riêng cho độc giả này |
| 2 | 2.2 | Negative | Độc giả A đứng **thứ 2** trong hàng chờ của một cuốn sách | Bản duy nhất của cuốn này được trả lại và đang giữ cho người đứng đầu hàng chờ | Độc giả A không nhận thông báo "sách đã có sẵn" **And** vị trí trong hàng chờ của A vẫn được hiển thị |
| 2 | 2.3 | Negative | Độc giả đã hủy đặt trước cuốn sách | Một bản của cuốn này được trả lại thư viện | Độc giả không nhận thông báo nào về cuốn sách này |
| 2 | 2.4 | Edge | Độc giả đứng đầu hàng chờ đã nhận thông báo và sách đang được giữ cho họ | Đủ 48 giờ kể từ lúc gửi thông báo mà độc giả chưa đến nhận | Giữ chỗ chuyển sang "Đã hết hạn" **And** độc giả kế tiếp trong hàng chờ nhận thông báo sách đã có sẵn |

### Story 3 – Giới hạn số sách mượn cùng lúc

| Story | AC# | Loại | Given | When | Then |
|---|---|---|---|---|---|
| 3 | 3.1 | Happy | Độc giả đang mượn/giữ chỗ 2 cuốn (giới hạn 5 cuốn) | Độc giả đặt mượn thêm 1 cuốn còn sách | Đặt mượn thành công **And** hiển thị "Bạn đã mượn 3/5 cuốn" |
| 3 | 3.2 | Edge (giá trị biên) | Độc giả đang mượn/giữ chỗ 4 cuốn | Độc giả đặt mượn cuốn thứ 5 | Đặt mượn thành công **And** hiển thị "Bạn đã mượn 5/5 cuốn" |
| 3 | 3.3 | Negative / Ràng buộc nghiệp vụ | Độc giả đang mượn/giữ chỗ đủ 5 cuốn | Độc giả đặt mượn cuốn thứ 6 | Hệ thống từ chối, hiển thị "Bạn đã đạt giới hạn tối đa 5 cuốn, vui lòng trả sách trước khi mượn thêm" **And** không tạo đặt mượn mới |
| 3 | 3.4 | Edge | Độc giả đang mượn/giữ chỗ đủ 5 cuốn | Độc giả trả 1 cuốn tại quầy | Số sách của độc giả hiển thị "4/5 cuốn" **And** độc giả đặt mượn được thêm 1 cuốn |
| 3 | 3.5 | Edge | Độc giả đang giữ chỗ đủ 5 cuốn, trong đó có 1 cuốn đã quá 48 giờ chưa nhận | Đủ 48 giờ và giữ chỗ hết hạn | Số sách của độc giả giảm còn "4/5 cuốn" **And** độc giả đặt mượn được thêm 1 cuốn |

---

## 3. Câu hỏi làm rõ cho Product Owner

**Story 1**
1. Một độc giả được giữ tối đa bao nhiêu thời gian? 48 giờ có tính cả ngày nghỉ, ngày lễ và ngoài giờ mở cửa của thư viện không?
2. Nếu độc giả muốn hủy đặt mượn trước khi hết 48 giờ thì có được phép không, và có bị hạn chế gì không?
3. Thư viện có nhiều bản của cùng một cuốn thì độc giả có được đặt mượn nhiều bản của cùng một đầu sách không?

**Story 2**
1. Thông báo được gửi qua kênh nào (email, SMS, thông báo trong ứng dụng) và cần gửi trong bao lâu sau khi sách có sẵn?
2. Hàng chờ đặt trước xử lý theo thứ tự nào (ai đặt trước thì được trước)? Có độc giả nào được ưu tiên không (giảng viên, sinh viên năm cuối...)?
3. Có cần nhắc lại cho độc giả khi sắp hết hạn giữ chỗ không (VD: còn 6 giờ)?

**Story 3**
1. **Giả định: tối đa 5 cuốn/độc giả.** Con số giới hạn chính xác là bao nhiêu? Có khác nhau giữa các nhóm độc giả (sinh viên, giảng viên) không?
2. Sách đang được giữ chỗ chờ nhận có được tính vào giới hạn không, hay chỉ tính sách đã nhận về?
3. Thủ thư có quyền ngoại lệ để cho một độc giả mượn vượt giới hạn trong trường hợp đặc biệt không?

---

## 4. Definition of Done (áp dụng cho MỌI Product Backlog Item)

Một Product Backlog Item chỉ được coi là **Done** khi thỏa mãn **tất cả** các tiêu chí sau:

- [ ] Code đã được **review** bởi ít nhất 1 thành viên khác trong nhóm và mọi góp ý đã được xử lý.
- [ ] Code tuân thủ **coding convention** của nhóm và không còn cảnh báo lỗi từ công cụ kiểm tra tĩnh (linter).
- [ ] **Unit test** đã được viết cho phần code mới, tất cả test đều **pass**, độ phủ test đạt tối thiểu 80% cho phần code mới.
- [ ] Các test tích hợp/hồi quy hiện có **vẫn pass**, không gây lỗi cho tính năng khác.
- [ ] Tính năng đã được **tích hợp (merge)** vào nhánh chính và **build thành công** trên CI.
- [ ] Tính năng đã được **triển khai lên môi trường staging/test** và chạy ổn định.
- [ ] Tài liệu liên quan (tài liệu kỹ thuật, hướng dẫn sử dụng, release note) đã được **cập nhật**.
- [ ] Không còn **bug nghiêm trọng (critical/major)** nào chưa xử lý đối với item này.
- [ ] **Product Owner** đã xem demo và **chấp nhận** item trong Sprint Review.

---

## 5. Câu hỏi: Story 1 đã đạt đủ các AC nhưng code chưa được review theo DoD, vậy Story 1 đã Done chưa?

**Chưa Done.** Done chỉ đạt khi Story thỏa mãn *cả* Acceptance Criteria của story *và* toàn bộ Definition of Done của nhóm; việc code chưa được review nghĩa là DoD chưa đạt, nên Story 1 chưa thể coi là hoàn thành.
