---
name: project-base
description: Apply the user's frontend/backend base rules and CRM design conventions when creating a project base, adding modules, or standardizing a requested part of a project. Use when the user invokes project-base or requests these conventions; preserve the structure and stack of existing projects unless migration is requested.
---

# Project Base

Áp dụng quy tắc kỹ thuật và giao diện trong các tài liệu đi kèm cho đúng yêu cầu người dùng. Đây là hướng dẫn, không phải bộ source scaffold hay danh sách tính năng bắt buộc.

## Phạm vi

- Chỉ thực hiện yêu cầu và phần đã được đồng ý. Không tự thêm tính năng, màn hình, trường, quyền, thư viện, dịch vụ hoặc sửa lỗi/refactor không liên quan.
- Nếu cần phần bổ sung chưa được cho phép, giải thích lý do, tác động và phương án thay thế; hỏi và chờ đồng ý trước khi thực hiện phần đó. Tiếp tục các phần độc lập đã được cho phép.
- Đề xuất không phải sự cho phép; im lặng không phải sự đồng ý. Không hỏi lại những bước cần thiết đã nằm trong phạm vi được thống nhất.
- Tuân thủ hướng dẫn hệ thống/môi trường. Trong phạm vi đó, yêu cầu cụ thể của người dùng và hướng dẫn repository được ưu tiên hơn các mẫu của skill.

## Đọc tài liệu theo công việc

- [PROJECT_RULES.md](references/PROJECT_RULES.md): đọc mục liên quan đến cấu trúc, module, API, database, quyền, test hoặc triển khai. Các mục 12–13 quy định cách đánh giá yêu cầu và giới hạn phạm vi.
- [DESIGN_GUIDE.md](references/DESIGN_GUIDE.md): đọc khi tạo/sửa giao diện; áp dụng bố cục màn hình, màu sắc, nút, bộ lọc riêng theo trường, phân trang, tiến trình và trạng thái phù hợp.
- Không đọc toàn bộ tài liệu nếu chỉ cần một mục. Hai tài liệu nằm trong thư mục skill, không phụ thuộc việc repository đích có các file cùng tên.

## Cách thực hiện

1. Kiểm tra yêu cầu, hướng dẫn repository, code liên quan, stack và thay đổi hiện có. Xác định kết quả bàn giao và phạm vi.
2. Đánh giá tác động, không chỉ số file:
   - **Đơn giản:** rõ yêu cầu, sửa cục bộ, dễ hoàn tác, không đổi schema/contract/cơ chế quyền → thực hiện trực tiếp.
   - **Phức tạp:** đổi kiến trúc, schema, quyền, API, tích hợp hoặc nhiều luồng phụ thuộc → trình bày plan trước khi triển khai, gồm phạm vi, bước thực hiện, kiểm thử và rủi ro cập nhật.
   - **Chưa rõ:** hỏi quyết định ảnh hưởng kết quả; tiếp tục khảo sát phần không phụ thuộc câu trả lời.
3. Nếu chỉ được yêu cầu plan, bàn giao plan. Nếu được yêu cầu triển khai và phạm vi rõ, tiếp tục thực hiện theo plan; hỏi trước phần phát sinh ngoài phạm vi.
4. Với base mới, dùng cây FE/BE trong tài liệu. Với dự án hiện có, giữ cấu trúc/stack và contract hiện tại trừ khi người dùng yêu cầu chuyển đổi. Chỉ tạo module/file có trách nhiệm thực tế; không thêm toàn bộ module mẫu hay công cụ tùy chọn.
5. Kiểm thử và bàn giao theo phần dưới. Commit, push, cài đặt và triển khai theo yêu cầu, không suy ra từ yêu cầu chỉnh code.

## Kiểm thử và bàn giao

- Thay đổi code phải có test phù hợp: chạy test hiện có nếu đủ bao phủ; thêm/cập nhật test cho hành vi mới hoặc lỗi chưa được bao phủ. Kiểm tra quyền phải có trường hợp cho phép, từ chối và ngoài scope.
- Chọn unit/integration/E2E theo tác động. Khi sửa logic dùng chung, kiểm tra các luồng phụ thuộc; lint/build không thay thế test.
- Với thay đổi tài liệu, kiểm tra nội dung, cấu trúc, ví dụ và liên kết; không tạo test code không liên quan.
- Báo thay đổi, lệnh kiểm tra và kết quả thực tế. Nếu chưa chạy được test, nêu nguyên nhân và phần cần kiểm chứng; không tuyên bố đã hoàn tất kiểm chứng.
- Bảo vệ secret và thay đổi có sẵn của người dùng. Không seed lại, xóa dữ liệu hoặc thay đổi môi trường ngoài phạm vi được phép.
