# Phong cách thiết kế EDU CRM

Tài liệu tổng quan để áp dụng phong cách giao diện này cho dự án khác.

## 1. Phong cách chung

- Giao diện quản trị gọn, hiện đại, ưu tiên dữ liệu và thao tác.
- Nền sáng, các vùng nội dung màu trắng, viền mảnh, ít bóng đổ.
- Xanh teal là màu chủ đạo cho nút chính, liên kết và menu đang chọn.
- Font sans-serif; dự án hiện tại dùng Geist.
- Icon nét mảnh, bo góc nhẹ, khoảng cách nhất quán.

## 2. Màu sắc

| Thành phần | Màu |
| --- | --- |
| Chủ đạo | `#087B98` |
| Chủ đạo khi hover | `#066780` |
| Nền nhấn nhẹ | `#E6F5F8` |
| Nền ứng dụng | `#F6F8FC` |
| Card / bảng / form | `#FFFFFF` |
| Chữ chính | `#172033` |
| Chữ phụ | `#667085` |
| Viền | `#E7EAF0` |
| Thành công | `#22C55E` |
| Cảnh báo | `#F59E0B` |
| Lỗi / nguy hiểm | `#EF4444` |

## 3. Bố cục tổng thể

- **Sidebar trái:** logo, nhóm module, menu active và thông tin tài khoản.
- **Header trên:** tên không gian, tài khoản, thông báo, đăng xuất.
- **Nội dung chính:** breadcrumb, tiêu đề, hành động và nội dung màn hình.
- Desktop có sidebar cố định; tablet/mobile dùng menu dạng drawer.
- Form thích ứng theo chiều rộng; bảng cuộn ngang trong vùng chứa khi cần.

## 4. Các màn hình chuẩn của một module

| Màn hình | Nội dung chính |
| --- | --- |
| **List — Danh sách** | Tiêu đề, nút thêm mới, tìm kiếm/bộ lọc, bảng dữ liệu, phân trang |
| **Create — Tạo mới** | Form chia nhóm thông tin, trường bắt buộc, nút Hủy / Tạo mới |
| **Edit — Chỉnh sửa** | Form có dữ liệu hiện tại, nút Hủy / Lưu thay đổi |
| **Detail — Chi tiết** | Thông tin hồ sơ, trạng thái, dữ liệu liên quan, hành động nghiệp vụ |

Tùy nhu cầu có thể thêm **Nhập/Xuất**, **Lịch sử**, **Lưu trữ**. Dashboard, Báo cáo và Cài đặt dùng màn hình riêng phù hợp chức năng.

## 5. Quy tắc giao diện

- Tiêu đề trang khoảng **20–22px**, nội dung **14px**, chữ phụ **12px**.
- Card trắng, bo góc nhẹ, padding khoảng **16–20px**.
- Label nằm trên input; trường bắt buộc có dấu `*`; lỗi hiển thị sát trường.
- Nút chính màu teal; nút phụ outline hoặc nền nhẹ; nút nguy hiểm màu đỏ.
- Trạng thái dùng badge có chữ, nền nhạt và màu theo ý nghĩa.
- Có trạng thái đang tải, không có dữ liệu, lỗi và đang lưu.
- Thông báo bằng tiếng Việt, nêu rõ nguyên nhân và cách xử lý.
- Dùng chung component và phong cách giữa các module.

## 6. Nút thao tác

| Loại nút | Kiểu hiển thị | Ví dụ |
| --- | --- | --- |
| Chính | Nền teal, chữ trắng | Thêm mới, Tạo mới, Lưu thay đổi |
| Phụ | Nền nhẹ hoặc trắng có viền | Hủy, Nhập/Xuất, Áp dụng bộ lọc |
| Nhẹ | Không có nền nổi bật, nền nhạt khi hover | Đóng, thao tác phụ |
| Nguy hiểm | Nền đỏ, chữ trắng | Xóa, xác nhận thao tác nguy hiểm |
| Chỉ icon | Nút gọn, có tooltip/nhãn truy cập | Mở menu, hiện mật khẩu, trang trước/sau |

- Chữ nút **14px**, đậm vừa; icon thường **16–17px**, đặt trước chữ.
- Nút bo góc nhẹ; cao tối thiểu **36px** từ màn `sm`, **44px** trên mobile.
- Màn List: nút Thêm mới nằm phía trên bên phải, cùng nhóm với hành động phụ.
- Màn Create/Edit: cuối form, căn phải, thứ tự **Hủy → Tạo mới/Lưu thay đổi**.
- Khi xử lý: khóa nút, đổi nhãn như “Đang lưu…” để tránh gửi nhiều lần.
- Khi disabled: giảm độ đậm và không cho thao tác; thiếu điều kiện cần có lời giải thích.

## 7. Phân trang

- Đặt bên dưới bảng: **tổng số hồ sơ và số hồ sơ trên trang** bên trái, **điều hướng trang** bên phải; màn nhỏ cho phép xuống dòng.
- Có nút **Trang trước / Trang sau**, số trang hiện tại và các trang liền kề khi hợp lệ.
- Trang đang chọn dùng nền xanh nhạt, chữ teal.
- Có ô nhập số trang, nhấn **Enter** để chuyển; số không hợp lệ hiển thị lỗi ngay tại khu vực phân trang.
- Khóa Trang trước ở trang đầu; khóa Trang sau khi hết dữ liệu.
- Ẩn điều hướng nếu chỉ có một trang.
- Nút phân trang **36 × 36px** từ màn `sm`, **44 × 44px** trên mobile.

Ví dụ khi đang ở trang 3:

```text
Tổng 120 hồ sơ · 20 trên trang này          ‹  2  [3]  4  [Nhập trang]  ›
```

Số liệu trên là minh họa. Số hồ sơ mỗi trang lấy theo cấu hình của module; đây là quy tắc trình bày, không yêu cầu tất cả module có cùng giới hạn dữ liệu.

## 8. Tiến trình theo bước

Dùng ở màn Detail để thể hiện hồ sơ đang ở bước nào trong quy trình nghiệp vụ.

- Đặt trong card trắng có viền mảnh, phía trên phần thông tin chi tiết.
- Đầu card có tiêu đề và mô tả ngắn, ví dụ **“Tiến trình tư vấn”**, **“Giai đoạn 3/5 · Quan tâm”**.
- Mỗi bước gồm một vòng tròn **24px**, tên bước và đường nối mảnh giữa các bước.
- Từ màn `sm`: xếp ngang, chia đều chiều rộng, tên nằm dưới vòng tròn. Mobile: xếp dọc, tên nằm bên phải.

| Trạng thái | Hiển thị |
| --- | --- |
| Đã đi qua | Vòng tròn teal, dấu check trắng; đường nối đã đi qua màu teal |
| Hiện tại | Nhấn tên bước bằng chữ teal đậm, thêm nhãn “Hiện tại” và vòng sáng nhạt |
| Chưa tới | Vòng tròn trắng, viền xám, số thứ tự; tên và đường nối màu nhạt |
| Hoàn tất | Các bước có dấu check; bước cuối thêm nhãn “Hoàn tất” |
| Dừng / không tiếp tục | Thông báo riêng có nguyên nhân; không hiển thị như hoàn tất thành công |

Ví dụ:

```text
Mới → Đã liên hệ → Quan tâm → Tư vấn → Đã ghi danh
```

Tiến trình phản ánh trạng thái hồ sơ, không phải phần trăm tải dữ liệu. Khi áp dụng cho dự án khác, thay tên và số bước theo nghiệp vụ; không mặc định bấm vào bước là được chuyển trạng thái.

## 9. Thanh tìm kiếm / bộ lọc

Quy ước áp dụng cho dự án mới: **mỗi trường cần tìm kiếm hoặc lọc có một ô riêng trên thanh tìm kiếm**, không gom nhiều trường vào một ô tìm kiếm chung.

- Đặt trên bảng List; từng ô có label rõ như Mã hồ sơ, Họ tên, Số điện thoại, Trạng thái, Người phụ trách.
- Trường văn bản dùng input; danh mục/trạng thái dùng select; ngày dùng Từ ngày / Đến ngày.
- Chỉ hiển thị trường phù hợp với module; thông tin được tìm/lọc phải có trên danh sách để đối chiếu kết quả.
- Nhiều điều kiện được kết hợp để thu hẹp kết quả; ô bỏ trống nghĩa là không lọc trường đó.
- Có nút **Tìm kiếm** và **Xóa bộ lọc**; áp dụng hoặc xóa lọc sẽ về trang đầu.
- Desktop chia các ô thành hàng, nhiều trường thì xuống hàng; mobile xếp dọc hoặc 2 cột khi đủ chỗ, không giấu các trường trong menu chung.

Ví dụ:

```text
[Mã hồ sơ] [Họ tên] [Số điện thoại] [Trạng thái ▼]
[Người phụ trách ▼] [Từ ngày] [Đến ngày] [Tìm kiếm] [Xóa bộ lọc]
```

Đây là quy ước thiết kế theo yêu cầu mới; giao diện CRM hiện tại vẫn có ô tìm kiếm chung ở một số module.

## 10. Tabs

- Dùng để chia nội dung liên quan trong cùng màn, ví dụ **Thông tin / Hồ sơ liên quan / Ghi chú / Lịch sử**.
- Đặt dưới tiêu đề hoặc phần thông tin tổng quan; tab đang chọn có chữ teal và gạch dưới teal.
- Tên tab ngắn, rõ; nội dung bên dưới tương ứng với tab đang chọn.
- Mobile cho cuộn ngang thanh tabs; không ép nhãn xuống nhiều dòng.
- Chỉ hiển thị tab có chức năng và quyền truy cập phù hợp.

## 11. Modal xác nhận

- Dùng cho thao tác cần xác nhận như xóa, lưu trữ hoặc chuyển trạng thái có ảnh hưởng nghiệp vụ.
- Khung trắng, bo góc nhẹ, overlay tối; tiêu đề nêu đúng hành động.
- Nội dung có tên/mã hồ sơ và hậu quả cụ thể, tránh chỉ hỏi “Bạn có chắc không?”.
- Nút cuối modal theo thứ tự **Hủy → Xác nhận hành động**; ghi rõ “Xóa hồ sơ”, “Lưu trữ” thay cho nhãn chung khi có thể.
- Nút nguy hiểm màu đỏ; thao tác thông thường màu teal. Đang xử lý thì khóa nút và hiện trạng thái.
- Có nút đóng, hỗ trợ bàn phím và quản lý focus khi áp dụng vào dự án mới.

## 12. Thao tác hàng loạt

- Checkbox ở đầu mỗi hàng; checkbox đầu bảng chọn/bỏ chọn toàn bộ hồ sơ trên trang hiện tại.
- Khi có hồ sơ được chọn, hiện thanh hành động phía trên bảng: **“Đã chọn N hồ sơ”**, các thao tác được hỗ trợ và nút **Bỏ chọn**.
- Chỉ hiện hành động phù hợp với module và quyền người dùng, ví dụ phân công, chuyển trạng thái, lưu trữ hoặc xuất hồ sơ đã chọn.
- Thao tác nguy hiểm cần xác nhận, nêu rõ số hồ sơ bị ảnh hưởng; đang xử lý thì khóa nút.
- Đổi bộ lọc hoặc trang thì bỏ lựa chọn để tránh thao tác nhầm; nếu hỗ trợ chọn xuyên trang phải ghi rõ phạm vi đã chọn.
- Kết quả nêu số thành công/thất bại và nguyên nhân; không báo thành công toàn bộ khi có hồ sơ lỗi.

## 13. Lịch sử hoạt động

- Đặt trong tab **Lịch sử** hoặc section riêng ở màn Detail.
- Mỗi bản ghi có **người thực hiện, thao tác, thời gian**; thêm nội dung thay đổi khi cần.
- Hiển thị mới nhất trước; tên người và hành động là thông tin chính, thời gian dùng chữ nhỏ màu muted.
- Thay đổi quan trọng có thể trình bày **giá trị trước → giá trị sau**; không hiển thị mật khẩu hoặc dữ liệu bí mật.
- Dùng timeline gọn hoặc bảng khi nhiều dữ liệu; lịch sử dài có phân trang/tải thêm.

Ví dụ: **Nguyễn Văn A · Chuyển trạng thái: Mới → Đã liên hệ · 09:30 04/10/2026**.

## 14. Trạng thái giao diện

| Trạng thái | Cách hiển thị |
| --- | --- |
| Đang tải | Skeleton theo bố cục bảng/card; dùng spinner cho thao tác nhỏ |
| Chưa có dữ liệu | Icon nhẹ, tiêu đề rõ, mô tả ngắn; có nút Thêm mới khi được phép |
| Không có kết quả tìm kiếm | Nêu không có hồ sơ khớp điều kiện; gợi ý chỉnh hoặc xóa bộ lọc |
| Lỗi tải dữ liệu | Nêu nguyên nhân và nút Thử lại; không hiển thị như danh sách trống |
| Lỗi nhập liệu | Thông báo sát trường, viền đỏ; hướng dẫn giá trị hợp lệ |
| Thiếu quyền | Giải thích quyền/thao tác còn thiếu và cách liên hệ quản trị viên; không hiển thị dữ liệu ngoài quyền |
| Đang lưu/xử lý | Khóa nút liên quan, đổi nhãn “Đang lưu…” hoặc hiển thị tiến độ |
| Thành công | Toast ngắn gọn, cập nhật dữ liệu hiển thị sau thao tác |

Giữ trạng thái nhất quán giữa các module; không dùng số 0 hoặc thông báo “Chưa có dữ liệu” để thay cho lỗi hay thiếu quyền.

## 15. Áp dụng cho dự án khác

Giữ bộ màu, khung sidebar/header và các mẫu **List / Create / Edit / Detail**. Thay logo, tên sản phẩm, menu, trường dữ liệu và luồng nghiệp vụ theo dự án mới.
