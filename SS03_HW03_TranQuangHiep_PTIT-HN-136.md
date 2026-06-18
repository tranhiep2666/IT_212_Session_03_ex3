Bạn là một Senior System Analyst kiêm Software Architect.

Ngữ cảnh:

* Hệ thống đã index mã nguồn của module Cart trong dự án Guai-api.
* Hãy phân tích implementation hiện tại của phương thức `CartService.addToCart(...)`.
* Thực hiện đồng thời 2 nhiệm vụ: (1) phát hiện lỗ hổng logic nghiệp vụ; (2) chuyển hóa các phát hiện thành Business Rules theo chuẩn SRS.

Yêu cầu phân tích:

1. Đọc toàn bộ luồng xử lý của phương thức addToCart().
2. Xác định các trường hợp dữ liệu đầu vào hoặc nghiệp vụ chưa được kiểm soát.
3. Chỉ rõ:

    * Điều kiện gây lỗi.
    * Hậu quả nghiệp vụ.
    * Mức độ ảnh hưởng.
    * Đề xuất cách xử lý.

Đặc biệt kiểm tra các tình huống:

* quantity <= 0
* quantity âm
* quantity bằng 0
* quantity quá lớn
* Tổng số lượng sản phẩm trong giỏ hàng sau khi cộng thêm vượt quá tồn kho hiện có.
* Sản phẩm hết hàng.
* Race condition khi nhiều request cùng thêm sản phẩm vào giỏ hàng.

Định dạng kết quả phần 1:

## Logic Gap Analysis

| ID | Logic Gap | Scenario | Impact | Recommendation |
| -- | --------- | -------- | ------ | -------------- |

Sau khi hoàn thành phân tích lỗi, sinh tiếp tài liệu SRS.

Định dạng kết quả phần 2:

# Business Rules - Cart Management

Đối với mỗi quy tắc, trình bày theo mẫu:

### BR-XXX: <Tên quy tắc>

**Description**
<Mô tả nghiệp vụ>

**Condition**
<Điều kiện áp dụng>

**Rule**
<Quy tắc bắt buộc>

**System Response**
<Phản hồi hệ thống>

**Priority**
High / Medium / Low

Yêu cầu tối thiểu phải sinh các quy tắc:

1. Kiểm tra sản phẩm tồn tại.
2. Số lượng thêm vào giỏ hàng phải > 0.
3. Không cho phép quantity âm.
4. Không cho phép quantity bằng 0.
5. Tổng số lượng trong giỏ hàng không được vượt quá tồn kho khả dụng.
6. Không cho phép thêm sản phẩm hết hàng.
7. Hệ thống phải trả về thông báo lỗi nghiệp vụ rõ ràng khi vi phạm quy tắc.
8. Hệ thống phải đảm bảo tính nhất quán dữ liệu khi có nhiều request đồng thời.

Kết thúc bằng mục:

# SRS Change Impact

Liệt kê:

* Các service cần sửa.
* Repository cần bổ sung.
* API contract cần thay đổi.
* Validation cần bổ sung.
* Test cases cần cập nhật.

Chỉ sử dụng thông tin suy luận từ code và nghiệp vụ Cart/Inventory. Không tạo giả định ngoài phạm vi nếu không có căn cứ.

