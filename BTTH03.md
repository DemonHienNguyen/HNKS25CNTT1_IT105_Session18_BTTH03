
[1.2 Scope]

- Hệ thống hỗ trợ khách hàng doanh nghiệp đặt tour trọn gói cho nhóm từ 10 người trở lên.

[2.4 Constraints]

- Actor chính: Nhân viên đặt tour (phía khách hàng doanh nghiệp), Điều phối viên RikkeiTravel.
- Use Case: Tạo yêu cầu đặt tour, Duyệt báo giá, Xác nhận thanh toán.

[3.2 Functional Requirements]

- REQ-21: Hệ thống phải phản hồi báo giá cho khách hàng doanh nghiệp một cách nhanh chóng sau khi nhận yêu cầu.
- REQ-22: Khi khách hàng xác nhận thanh toán đủ 100% giá trị hợp đồng, hệ thống tự động chuyển trạng thái đơn sang "Đã xác nhận".
- REQ-23 (trang 8): Điều phối viên có thể chỉnh sửa báo giá bất kỳ lúc nào, kể cả sau khi khách hàng đã xác nhận thanh toán.
- REQ-24 (trang 19): Sau khi khách hàng xác nhận thanh toán, mọi thông tin báo giá được khóa, không ai được chỉnh sửa.
- REQ-25: Tính năng xuất báo giá ra file PDF có thể được cân nhắc bổ sung sau, tùy nguồn lực đội phát triển.

[1.3 Definitions]

- Sơ đồ ERD lưu trữ Yêu cầu đặt tour - Báo giá - Hợp đồng.

**Bước 1 — Tự lập bảng lỗi phát hiện được** (tự xác định số dòng cần thiết, không giới hạn số lỗi tối thiểu, nhưng phải tìm đủ cả 2 nhóm lỗi: sai cấu trúc IEEE 830 và vi phạm đặc tính vàng, tối thiểu 3 đặc tính vàng khác nhau):

| **STT** | **Nội dung lỗi**                                                                                              | **Phân loại lỗi (Sai vị trí IEEE 830 / Vi phạm đặc tính vàng nào)** | **Vị trí đúng hoặc cách khắc phục**                                                                                                                                                                                                      |
| ------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| *1*         | Mục 2.4 chứa danh sách Actor và Use Case                                                                          | Sai vị trí IEEE 830                                                                | Chuyển danh sách các Actor và Use Case sang mục 2.1 Bối cảnh sản phẩm (Product Perspective) vì 2.4 chỉ bắt phải rằng buộc và yêu cầu bắt buộc                                                                                     |
| 2             | Mục 1.3 chứa Sơ đồ ERD                                                                                           | Sai vị trí IEEE 830                                                                | Chuyển sơ đồ ERD lưu trữ yêu cầu đặt Tour - Báo giá - Hợp đồng sang danh mục 3.4 Yêu cầu Cơ sở dữ liệu (Database Requirements: Sơ đồ ERD & Từ điển dữ liệu) vì mục 1.3 chỉ là định nghĩa và các từ viết tắt |
| 3             | REQ-21: Chứa từ "một cách nhanh chóng"                                                                           | Vi phạm đặc tính Verifiable (Có thể kiểm chứng)                             | Chuyển chữ "Một cách nhanh chóng" sang thành một thời gian [Giờ/Phút/Giây] cụ thể để kiểm nghiệm viên có thể kiểm thử                                                                                                            |
| 4             | REQ-22: Hệ thống chuyển trạng thái sang "Đã xác nhận" nhưng không hề đề cập cách xác nhận như nào | Vi phạm đặc tính Unambiguous (Không mơ hồ)                                   | Cần phải làm rõ hệ thống tự nhận biết qua cổng thanh toán thì hệ thống mới đổi trạng thái                                                                                                                                           |
| 5             | REQ-23 + REQ-24 mâu thuẫn với nhau                                                                                | Vi phạm đặc tính Consistent (Nhất quán)                                       | Hãy loại bỏ sự mâu thuẫn giữa REQ-23 và REQ-24. Về mặt nghiệp vụ sau khi thanh toán 100% hóa đơn thì phải được khóa                                                                                                            |
| 6             | REQ-25: Tính năng xuất PDF "Có thể được cân nhắc bổ sung sau này, tùy nguồn lực"                       | Vi phạm đặc tính Ranked (Được xếp hạng)                                    | Phải chuyển sang dạng yêu cầu tùy chọn hoặc loại bỏ hẳn khỏi Scope phiên bản hiện tại                                                                                                                                                  |

**Bước 2 — Đề xuất bản chỉnh sửa hoàn chỉnh**


[1.2 Scope]

- Hệ thống hỗ trợ khách hàng doanh nghiệp đặt tour trọn gói cho nhóm từ 10 người trở lên.

[2.1 Product Perspective]

- Actor chính: Nhân viên đặt tour (phía khách hàng doanh nghiệp), Điều phối viên RikkeiTravel.
- Use Case: Tạo yêu cầu đặt tour, Duyệt báo giá, Xác nhận thanh toán.

[3.2 Functional Requirements]

- REQ-21: Sau khi nhận yêu cầu đặt tour đầy đủ thông tin từ khách hàng, hệ thống phải gửi thông báo điều hướng đến màn hình xử lý của điều phối viên trong 5 giây và gửi lại báo giá cho khách hàng trong vòng 30 phút làm việc
- REQ-22: Khi hệ thống nhận được phản hồi khách hàng xác nhận đã thanh toán đủ 100% giá trị hợp đồng từ cổng thanh toán trực tuyến thì hệ thống phải tự động cập nhật trạng thái đơn hàng sang "Đã xác nhận" ngay lập tức
- REQ-24 (trang 19): Ngay sau khi khách trạng thái đơn chuyển dang "Đã xác nhận" Hệ thống sẽ thực hiện khóa toàn bộ dữ liệu của báo giá đó, không có bất ký đối tượng nào được phép chỉnh sửa thông tin báo giá này
- REQ-25: Tính năng xuất báo giá ra file PDF được phân loại vào danh mục yêu cầu cao, sẽ không thực hiện trong phiên bản đầu và được chuyển sang xem xét ở giai đoạn tiếp theo

[3.4 Database Requirements]

- Sơ đồ ERD lưu trữ Yêu cầu đặt tour - Báo giá - Hợp đồng.
