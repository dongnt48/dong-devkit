# Quy tắc base dự án

Quy ước nền tảng để phát triển dự án mới dựa trên EDU CRM và cấu trúc frontend đã thống nhất. Phong cách giao diện xem tại [DESIGN_GUIDE.md](DESIGN_GUIDE.md). Đây là tài liệu hướng dẫn, không phải một bộ source base đã được tách riêng.

## 1. Phạm vi áp dụng và công nghệ

### Quy định bắt buộc

- Chỉ thực hiện yêu cầu hiện tại trong phạm vi đã thống nhất. Không tự gộp cải tiến, sửa lỗi không liên quan, refactor hoặc dọn code vào công việc đang làm.
- Tuân thủ cách tổ chức FE/BE ở mục 2 khi tạo base mới; chỉ tạo module và file có nhu cầu thực tế.
- Kiểm tra dữ liệu và quyền ở backend; bảo vệ secret, dữ liệu người dùng và database.
- Thống nhất contract API, cách đặt tên, phản hồi lỗi và trạng thái giao diện.
- Có migration cho thay đổi database và hướng dẫn triển khai có thể kiểm chứng.

### Công nghệ tham khảo từ EDU CRM

Chọn stack khi khởi tạo dự án và ghi lại trong README. Bảng này không bắt buộc mọi dự án phải cài toàn bộ công cụ.

| Phần | Nền tảng tham khảo |
| --- | --- |
| Frontend | Next.js App Router, React, TypeScript |
| Giao diện | Tailwind CSS, shadcn/ui, Base UI, Lucide |
| Dữ liệu frontend | TanStack Query cho dữ liệu API; TanStack Table khi bảng cần xử lý phức tạp |
| Form | React Hook Form, Zod khi phù hợp |
| Backend | NestJS, TypeScript |
| Database | PostgreSQL, Prisma |
| Cache / job | Redis khi cần cache/rate limit dùng chung; BullMQ dùng Redis để quản lý tác vụ nền |
| Triển khai | Docker Compose, Nginx, HTTPS |

Giữ phiên bản và lockfile nhất quán; không tự nâng phiên bản thư viện khi chỉ làm một tính năng nghiệp vụ.

### Thành phần tùy chọn

- Redis, BullMQ, store toàn cục và thư viện bảng chỉ thêm khi có nhu cầu cụ thể.
- Nhập/xuất, thao tác hàng loạt, lịch sử, tiến trình và báo cáo phụ thuộc yêu cầu nghiệp vụ.
- Không tạo hàng đợi cho thao tác ngắn có thể xử lý trực tiếp trong request.

## 2. Cấu trúc thư mục

### 2.1. Frontend

Cấu trúc chuẩn cho base dự án mới. `auth`, `users` và `dashboard` là các module mẫu; module khác áp dụng cùng cách tổ chức.

```text
my-next-app/
├── public/
│   ├── images/
│   ├── icons/
│   └── assets/
├── src/
│   ├── app/
│   │   ├── (auth)/
│   │   │   ├── login/
│   │   │   │   └── page.tsx
│   │   │   ├── register/
│   │   │   │   └── page.tsx
│   │   │   └── layout.tsx
│   │   ├── (dashboard)/
│   │   │   ├── dashboard/
│   │   │   │   ├── page.tsx
│   │   │   │   └── loading.tsx
│   │   │   ├── users/
│   │   │   │   ├── page.tsx
│   │   │   │   ├── create/
│   │   │   │   │   └── page.tsx
│   │   │   │   └── [id]/
│   │   │   │       ├── page.tsx
│   │   │   │       └── edit/
│   │   │   │           └── page.tsx
│   │   │   ├── settings/
│   │   │   │   └── page.tsx
│   │   │   └── layout.tsx
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── loading.tsx
│   │   ├── error.tsx
│   │   ├── not-found.tsx
│   │   └── globals.css
│   ├── components/
│   │   ├── ui/
│   │   │   ├── button.tsx
│   │   │   ├── input.tsx
│   │   │   ├── select.tsx
│   │   │   ├── dialog.tsx
│   │   │   ├── table.tsx
│   │   │   ├── badge.tsx
│   │   │   └── skeleton.tsx
│   │   ├── common/
│   │   │   ├── header.tsx
│   │   │   ├── sidebar.tsx
│   │   │   ├── footer.tsx
│   │   │   ├── pagination.tsx
│   │   │   ├── data-table.tsx
│   │   │   └── status-badge.tsx
│   │   └── layouts/
│   │       ├── dashboard-layout.tsx
│   │       └── auth-layout.tsx
│   ├── features/
│   │   ├── auth/
│   │   │   ├── components/
│   │   │   │   ├── login-form.tsx
│   │   │   │   └── register-form.tsx
│   │   │   ├── hooks/
│   │   │   │   └── use-auth.ts
│   │   │   ├── services/
│   │   │   │   └── auth.service.ts
│   │   │   ├── schemas/
│   │   │   │   └── auth.schema.ts
│   │   │   ├── types/
│   │   │   │   └── auth.types.ts
│   │   │   └── constants/
│   │   │       └── auth.constants.ts
│   │   ├── users/
│   │   │   ├── components/
│   │   │   │   ├── user-table.tsx
│   │   │   │   ├── user-form.tsx
│   │   │   │   ├── user-detail.tsx
│   │   │   │   └── user-filter.tsx
│   │   │   ├── hooks/
│   │   │   │   ├── use-users.ts
│   │   │   │   └── use-user.ts
│   │   │   ├── services/
│   │   │   │   └── user.service.ts
│   │   │   ├── schemas/
│   │   │   │   └── user.schema.ts
│   │   │   ├── types/
│   │   │   │   └── user.types.ts
│   │   │   └── constants/
│   │   │       └── user.constants.ts
│   │   └── dashboard/
│   │       ├── components/
│   │       │   ├── dashboard-stats.tsx
│   │       │   └── dashboard-chart.tsx
│   │       ├── hooks/
│   │       ├── services/
│   │       │   └── dashboard.service.ts
│   │       └── types/
│   │           └── dashboard.types.ts
│   ├── lib/
│   │   ├── api/
│   │   │   ├── client.ts
│   │   │   ├── endpoints.ts
│   │   │   └── error-handler.ts
│   │   ├── auth/
│   │   │   ├── token.ts
│   │   │   └── permissions.ts
│   │   ├── utils/
│   │   │   ├── cn.ts
│   │   │   ├── date.ts
│   │   │   └── format.ts
│   │   └── env.ts
│   ├── hooks/
│   │   ├── use-debounce.ts
│   │   ├── use-pagination.ts
│   │   ├── use-mobile.ts
│   │   └── use-permission.ts
│   ├── store/
│   │   ├── auth-store.ts
│   │   ├── ui-store.ts
│   │   └── index.ts
│   ├── types/
│   │   ├── api.types.ts
│   │   ├── common.types.ts
│   │   └── pagination.types.ts
│   └── config/
│       ├── site.config.ts
│       ├── navigation.config.ts
│       └── permissions.config.ts
├── .env.local
├── .env.example
├── .gitignore
├── eslint.config.mjs
├── proxy.ts
├── next.config.ts
├── package.json
├── tsconfig.json
└── README.md
```

**Quy tắc tổ chức:**

- `app/`: khai báo route, layout và trạng thái màn hình; ghép các component từ `features/`. Module chuẩn có List (`page.tsx`), Create (`create/page.tsx`), Detail (`[id]/page.tsx`), Edit (`[id]/edit/page.tsx`).
- `(auth)` và `(dashboard)` dùng layout riêng; tên nhóm trong ngoặc không xuất hiện trong URL. Route đăng ký chỉ triển khai khi dự án cần.
- `features/<module>/`: chứa component, hook, service gọi API, schema kiểm tra dữ liệu, type và constant riêng của module.
- `components/ui/`: thành phần cơ bản; `common/`: thành phần dùng chung như bảng, phân trang, trạng thái; `layouts/`: khung giao diện. Component dùng chung không chứa nghiệp vụ riêng của module.
- `lib/`: hạ tầng API, xử lý lỗi, xác thực, helper và đọc cấu hình môi trường; service của từng module sử dụng API client chung.
- `hooks/`, `types/`: chỉ chứa hook và kiểu dữ liệu dùng chung; phần riêng của module đặt trong `features/<module>/`.
- `store/`: trạng thái giao diện và trạng thái phiên đăng nhập khi cần chia sẻ toàn cục; dữ liệu API do TanStack Query quản lý nếu sử dụng, không lưu trùng cache vào store.
- `config/`: cấu hình website, menu và quyền giao diện. `proxy.ts` kiểm tra luồng truy cập; backend vẫn phải kiểm tra quyền cho từng API.
- `public/`: phân loại ảnh vào `images/`, biểu tượng vào `icons/`, tài nguyên tĩnh khác vào `assets/`.

### 2.2. Backend

Cấu trúc chuẩn cho base backend mới. Các module nghiệp vụ trong cây là mẫu tổ chức, lựa chọn theo nhu cầu dự án.

```text
crm-backend/
├── src/
│   ├── main.ts
│   ├── app.module.ts
│   ├── config/
│   │   ├── app.config.ts
│   │   ├── database.config.ts
│   │   └── env.validation.ts
│   ├── common/
│   │   ├── decorators/
│   │   ├── guards/
│   │   ├── interceptors/
│   │   ├── filters/
│   │   ├── pipes/
│   │   ├── exceptions/
│   │   ├── constants/
│   │   └── utils/
│   ├── database/
│   │   ├── migrations/
│   │   ├── seeds/
│   │   └── database.module.ts
│   ├── modules/
│   │   ├── auth/
│   │   │   ├── auth.module.ts
│   │   │   ├── auth.controller.ts
│   │   │   ├── auth.service.ts
│   │   │   ├── dto/
│   │   │   ├── strategies/
│   │   │   └── guards/
│   │   ├── users/
│   │   │   ├── users.module.ts
│   │   │   ├── users.controller.ts
│   │   │   ├── users.service.ts
│   │   │   ├── users.repository.ts
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   └── mappers/
│   │   ├── leads/
│   │   ├── customers/
│   │   ├── quotations/
│   │   ├── bookings/
│   │   ├── documents/
│   │   ├── customs/
│   │   ├── transportation/
│   │   ├── deliveries/
│   │   ├── payments/
│   │   ├── calls/
│   │   └── reports/
│   └── shared/
│       ├── types/
│       ├── interfaces/
│       └── enums/
├── test/
│   ├── e2e/
│   └── unit/
├── .env
├── .env.example
├── .gitignore
├── nest-cli.json
├── tsconfig.json
├── tsconfig.build.json
├── package.json
└── README.md
```

**Quy tắc tổ chức:**

- `main.ts`: khởi động ứng dụng, cấu hình HTTP và các xử lý toàn cục. `app.module.ts`: ghép các module.
- `config/`: đọc và kiểm tra biến môi trường, cấu hình ứng dụng và database; báo rõ cấu hình thiếu khi khởi động.
- `common/`: decorator, guard, interceptor, filter, pipe, exception và tiện ích dùng chung. Guard riêng của đăng nhập đặt trong `modules/auth/guards/`.
- `database/`: kết nối database, migration và seed. Cấu hình công cụ migration trỏ đúng thư mục này; không duy trì hai bộ migration song song. Khi dùng Prisma, khai báo vị trí schema và migration phù hợp trong cấu hình công cụ.
- `modules/<module>/`: đóng gói nghiệp vụ theo mẫu `users/`. Controller tiếp nhận request; service xử lý nghiệp vụ; repository truy cập dữ liệu; DTO kiểm tra đầu vào; entity mô tả dữ liệu; mapper chuyển dữ liệu sang contract trả về.
- `modules/auth/`: đăng nhập, phiên đăng nhập, strategy và guard xác thực. Module khác sử dụng cơ chế xác thực chung.
- `shared/`: type, interface và enum dùng giữa nhiều module; phần chỉ dùng trong một module đặt tại module đó.
- `test/unit/`: kiểm tra xử lý độc lập; `test/e2e/`: kiểm tra luồng API và tích hợp. Cấu hình test phải nhận đúng các thư mục này.
- `.env` chứa cấu hình riêng và được bỏ qua bởi Git; `.env.example` chỉ chứa mẫu cấu hình.
- Chỉ tạo file và lớp khi có trách nhiệm thực tế; không tạo file rỗng để đủ cây thư mục.
- Repository dùng khi cần tách truy vấn dữ liệu khỏi nghiệp vụ; entity/mapper dùng khi cần mô hình hoặc cách chuyển đổi riêng. Không bắt buộc tạo cả ba cho mọi module CRUD đơn giản.

### 2.3. Triển khai

- `deploy/` tại gốc repository chứa cấu hình và hướng dẫn triển khai dùng chung cho frontend/backend.

## 3. Base của một module

- Màn hình chuẩn: **List / Create / Edit / Detail**.
- API chuẩn: **GET danh sách, GET chi tiết, POST tạo, PATCH cập nhật**, thao tác xóa/lưu trữ theo nghiệp vụ.
- Có kiểu dữ liệu, validation, phân quyền, phạm vi truy cập và trạng thái giao diện.
- List có tìm/lọc theo từng trường, sắp xếp và phân trang; quy tắc trình bày theo `DESIGN_GUIDE.md`.
- Nhập/xuất, thao tác hàng loạt, lịch sử và tiến trình chỉ thêm khi module cần.
- Không đưa tên, trường hay trạng thái riêng của giáo dục vào component base.

## 4. API và dữ liệu

- API đặt dưới `/api/v1`; URL và tên trường nhất quán trong mỗi contract.
- Kết quả thông thường dùng `{ data: ... }`; danh sách có thể thêm `meta` phân trang.
- Lỗi dùng `{ error: { code, message, details }, request_id }`; thông báo cho người dùng rõ nguyên nhân.
- Backend kiểm tra dữ liệu độc lập với frontend; từ chối trường không được hỗ trợ.
- Bộ lọc kết hợp theo từng trường; chỉ cho phép sort/filter đã khai báo, không truyền trực tiếp tên cột tùy ý từ client vào truy vấn.
- Phân trang mặc định dùng `page` và `limit`; chốt giới hạn mặc định/tối đa trong contract API. Chỉ dùng cursor khi cần xử lý danh sách lớn hoặc luồng tải liên tục.
- Phân trang có thứ tự ổn định, thêm khóa duy nhất để phân biệt bản ghi cùng giá trị sort. Tổng số và danh sách phải dùng cùng bộ lọc/phạm vi quyền.
- Số tiền lưu bằng kiểu chính xác phù hợp, không tính tiền bằng số thực tùy tiện. Thống nhất cách xử lý ngày, giờ và múi giờ.

## 5. Database

- Thay đổi schema phải có migration; không sửa migration đã áp dụng lên môi trường dùng chung.
- Khai báo quan hệ, unique và index theo nghiệp vụ/truy vấn thực tế.
- Dùng transaction khi nhiều bản ghi phải thay đổi cùng nhau.
- Xóa mềm/lưu trữ khi cần khôi phục hoặc giữ lịch sử; không áp dụng máy móc cho mọi bảng.
- Seed khởi tạo và dữ liệu demo tách riêng; chạy lại không được ghi đè tài khoản hay cấu hình người dùng ngoài mục đích đã xác định.
- Tách database thử nghiệm khỏi dữ liệu khách hàng; sao lưu trước migration production.

## 6. Đăng nhập và phân quyền

- Xác thực và kiểm tra quyền ở backend; ẩn nút trên frontend chỉ hỗ trợ trải nghiệm.
- Mật khẩu lưu dạng hash an toàn; EDU CRM tham khảo Argon2, JWT và phiên refresh có thể thu hồi. Dự án mới ghi rõ cơ chế xác thực đã chọn.
- Bộ quyền chuẩn: **Xem / Tạo mới / Chỉnh sửa / Xóa / Nhập dữ liệu / Xuất dữ liệu**.
- Scope: **Không cấp / Cá nhân / Cấp dưới / Toàn bộ**; xác định rõ trường sở hữu của từng module.
- Trước khi áp dụng scope, xác định ai sở hữu hồ sơ, cấp dưới được tính theo quan hệ nào và cách xử lý hồ sơ chưa có người phụ trách. Chỉ hỗ trợ Cá nhân/Cấp dưới khi nghiệp vụ có các quan hệ đó.
- Nhập cần Tạo mới; Xuất cần Xem; phạm vi phụ thuộc không rộng hơn quyền nền.
- Kiểm tra cả hồ sơ liên kết; bản ghi không có chủ sở hữu không tự được phép truy cập với scope giới hạn.
- Báo cáo và xuất file phải áp dụng cùng giới hạn dữ liệu. Cache cần phân biệt quyền/phạm vi để không trả dữ liệu sai người.
- Phân biệt quyền quản trị hệ thống với quyền nghiệp vụ; không tự thêm quyền ngoài bộ chuẩn khi chưa có yêu cầu.

## 7. Frontend và phản hồi

- Gọi API qua client dùng chung; dùng query key có module, bộ lọc và thông tin cần thiết.
- Sau khi ghi dữ liệu, cập nhật hoặc invalidate các query liên quan.
- Có loading, empty, error, thiếu quyền, đang lưu và thành công; không che lỗi bằng dữ liệu rỗng.
- Khi mất quyền, không tiếp tục hiển thị dữ liệu cache được bảo vệ.
- Form có lỗi theo trường; khóa nút khi xử lý để tránh gửi lặp.
- Mỗi trường tìm/lọc có control riêng theo hướng dẫn thiết kế; thay đổi điều kiện thì về trang đầu.

## 8. Log và tác vụ nền

- Log nghiệp vụ ghi người thực hiện, hành động, thời gian và hồ sơ liên quan.
- Log đăng nhập tách khỏi lịch sử thay đổi nghiệp vụ khi cần quản lý riêng.
- Không ghi mật khẩu, token hoặc secret vào log; không để log debug dư thừa trong production.
- Tác vụ dài như nhập/xuất dùng job khi cần; có trạng thái, tiến độ và nguyên nhân lỗi.
- Job chạy theo quyền người yêu cầu, kiểm tra lại quyền khi xử lý; báo rõ kết quả từng phần.

## 9. Cấu hình và triển khai

- `.env` thật chỉ ở môi trường sử dụng; Git chứa file mẫu với giá trị placeholder.
- Frontend không được nhận secret backend. Tài khoản Điền nhanh chỉ dùng khi chủ động bật cho môi trường demo.
- Có cấu hình local/production, health check và hướng dẫn chạy.
- Triển khai bản có migration theo thứ tự: **build → migrate → cập nhật dịch vụ → kiểm tra health**.
- Không chạy lại seed hoặc xóa volume database như một bước cập nhật mặc định.

### Tương thích và rollback

- Khi frontend/backend được cập nhật riêng, API phải tương thích với phiên bản đang chạy trong thời gian chuyển tiếp; thay đổi phá vỡ contract cần kế hoạch chuyển đổi hoặc phiên bản API mới.
- Migration ưu tiên thêm trường/bảng trước, cập nhật ứng dụng và dữ liệu sau; chỉ xóa hoặc đổi cấu trúc cũ khi phiên bản đang dùng không còn phụ thuộc.
- Trước triển khai, lưu phiên bản image/code cũ và xác định cách khôi phục dịch vụ. Rollback ứng dụng phải tương thích với schema sau migration.
- Thay đổi có nguy cơ mất dữ liệu cần backup và phương án phục hồi đã kiểm tra; không mặc định rollback bằng cách xóa database hoặc chạy migration ngược.

## 10. Hoàn thành một tính năng

- [ ] Đủ màn hình và API theo yêu cầu.
- [ ] Validation, quyền, scope và hồ sơ liên kết đúng.
- [ ] Các trạng thái giao diện và thông báo rõ ràng.
- [ ] Kiểm thử các rủi ro thực tế: dữ liệu sai, thiếu quyền, ngoài scope, lỗi từng phần.
- [ ] Thay đổi code có test phù hợp và đã chạy đạt; thêm/cập nhật test cho hành vi mới hoặc lỗi được sửa. Lint/build không thay thế test.
- [ ] Lint/build đạt; migration và cấu hình mới được ghi trong hướng dẫn.
- [ ] Thay đổi API/database tương thích với quy trình cập nhật; có phương án rollback nếu ảnh hưởng môi trường đang chạy.
- [ ] Không có secret, dữ liệu khách hàng hoặc file local trong commit.

## 11. Quy ước đặt tên

| Thành phần | Quy ước | Ví dụ |
| --- | --- | --- |
| File/thư mục frontend | `kebab-case`; giữ tên đặc biệt của Next.js | `user-form.tsx`, `use-users.ts`, `page.tsx` |
| Component, class, type/interface | `PascalCase` | `UserForm`, `UsersService`, `UserResponse` |
| Biến và hàm | `camelCase`, thể hiện rõ ý nghĩa | `selectedUserId`, `createUser` |
| Hằng số cố định, biến môi trường | `UPPER_SNAKE_CASE` | `MAX_PAGE_SIZE`, `DATABASE_URL` |
| File backend | Tên module và vai trò của file | `users.controller.ts`, `users.service.ts` |
| DTO | Thao tác + đối tượng + `Dto` | `CreateUserDto`, `UpdateUserDto`, `ListUsersQueryDto` |
| Endpoint tài nguyên | Danh từ số nhiều; đường dẫn nhiều từ dùng `kebab-case` | `/api/v1/users`, `/api/v1/login-logs` |
| Trường JSON của API mới | `camelCase`, thống nhất đầu vào/đầu ra | `createdAt`, `ownerId` |
| Bảng/cột database mới | `snake_case`; tên bảng số nhiều | `users`, `login_logs`, `created_at` |

- Dùng tiếng Anh cho tên code; nhãn và thông báo giao diện dùng ngôn ngữ sản phẩm.
- Boolean đặt tên rõ nghĩa như `isActive`, `canExport`; thời điểm dùng hậu tố `At`, khóa liên kết dùng `Id`.
- Tên nghiệp vụ nhất quán giữa FE/BE; không gọi cùng một đối tượng bằng nhiều tên khác nhau.
- Quy ước mới áp dụng cho base mới; dự án đang chạy giữ contract hiện có, không đổi tên hàng loạt chỉ để khớp quy ước. Khi API và database khác cách đặt tên, ánh xạ rõ tại lớp dữ liệu/mapper.

## 12. Đánh giá yêu cầu và lập kế hoạch

Trước khi sửa, đọc code/tài liệu liên quan để xác định phạm vi, phụ thuộc và rủi ro. Đánh giá theo tác động thực tế, không chỉ theo số file hoặc độ dài yêu cầu.

| Mức độ | Dấu hiệu | Cách thực hiện |
| --- | --- | --- |
| Đơn giản | Yêu cầu rõ, thay đổi cục bộ, dùng mẫu có sẵn, dễ hoàn tác; không đổi schema, contract API hay cơ chế quyền | Thông báo ngắn rồi thực hiện trực tiếp, kiểm tra phần bị ảnh hưởng |
| Phức tạp | Có thay đổi kiến trúc, schema/dữ liệu, xác thực/phân quyền, contract API; tích hợp dịch vụ ngoài; nhiều luồng nghiệp vụ phụ thuộc nhau hoặc cần cập nhật theo thứ tự | Khảo sát và lập plan trước khi triển khai |
| Chưa rõ | Thiếu thông tin làm thay đổi kết quả hoặc có nhiều phương án với tác động khác nhau | Hỏi phần cần làm rõ; tiếp tục khảo sát các phần không phụ thuộc câu trả lời |

### Việc đơn giản: làm trực tiếp

- Ví dụ: sửa nhãn/thông báo, chỉnh khoảng cách/màu theo design guide, sửa thứ tự Tab, đổi input thành select theo tập giá trị đã xác định, bổ sung tài liệu.
- Sửa lỗi cục bộ khi đã xác định nguyên nhân và không thay đổi luồng nghiệp vụ quan trọng.
- Không bắt người dùng duyệt plan cho từng chỉnh sửa nhỏ. Không mở rộng phạm vi ngoài yêu cầu.

### Việc phức tạp: lên plan trước

- Ví dụ: thêm module có nhiều màn hình và API; thay đổi mô hình quyền; chuyển đổi dữ liệu; xây dựng nhập/xuất có job; tích hợp Facebook/Zalo; triển khai RAG; tổ chức lại source toàn dự án.
- Plan cần có: mục tiêu và phạm vi, hiện trạng, phương án chọn, các bước theo thứ tự phụ thuộc, thay đổi FE/BE/database, cách kiểm chứng và rủi ro triển khai/rollback nếu có.
- Chia thành các bước có kết quả kiểm tra được; giữ plan ngắn theo độ phức tạp, không thêm thủ tục không cần thiết.
- Nếu người dùng đã yêu cầu triển khai và phạm vi rõ, trình bày plan rồi tiếp tục thực hiện trong phạm vi đã được yêu cầu. Nếu phát sinh phần bổ sung chưa được đồng ý, phải hỏi trước khi làm phần đó; tiếp tục các phần độc lập đã được cho phép.
- Nếu người dùng chỉ yêu cầu lập plan, hoàn thành plan và chưa sửa source.

### Đánh giá lại khi có phát hiện mới

- Việc ban đầu nhỏ nhưng phát hiện ảnh hưởng schema, quyền hoặc nhiều luồng thì cập nhật mức độ và plan trước khi mở rộng sửa đổi.
- Khi phát hiện nhu cầu ngoài phạm vi, nêu rõ để người dùng quyết định; không tự gộp vào công việc đang làm.
- Khi hoàn thành, báo phần đã thay đổi, cách kiểm tra và giới hạn còn lại; không tuyên bố đã kiểm chứng những phần chưa chạy.

### Kiểm thử bắt buộc sau khi thực hiện

- Mọi thay đổi code phải có kiểm thử phù hợp: dùng test hiện có nếu đã bao phủ đầy đủ; thêm hoặc cập nhật test khi có hành vi mới hoặc sửa lỗi chưa được bao phủ.
- Chọn mức test theo tác động: unit cho xử lý độc lập; integration cho API/database và quan hệ dữ liệu; E2E cho luồng người dùng quan trọng hoặc thay đổi đi qua nhiều lớp.
- Sửa lỗi cần test tái hiện lỗi và xác nhận lỗi được khắc phục. Thay đổi quyền cần kiểm tra cả trường hợp được phép, bị từ chối và ngoài phạm vi dữ liệu.
- Chạy test liên quan sau thay đổi; nếu sửa logic dùng chung, chạy thêm các nhóm test phụ thuộc. Sửa các lỗi do thay đổi gây ra trước khi bàn giao.
- Không viết test chỉ để kiểm tra lại cách code được viết; test phải xác nhận hành vi và kết quả mong muốn.
- Với thay đổi chỉ ở tài liệu, kiểm tra nội dung, cấu trúc, ví dụ và liên kết thay vì tạo test code không liên quan.
- Báo rõ lệnh đã chạy, kết quả và phần chưa kiểm thử. Nếu môi trường không chạy được test, nêu nguyên nhân và bước còn thiếu; không coi việc triển khai là đã kiểm chứng hoàn tất.

## 13. Quy tắc sử dụng khi đóng gói thành skill

### Khi sử dụng

- Khi người dùng yêu cầu áp dụng bộ quy tắc này để tạo base, thêm module hoặc chuẩn hóa một phần dự án.
- Không tự coi toàn bộ tài liệu là danh sách tính năng cần triển khai. Cây thư mục chỉ là quy ước tổ chức và ví dụ.

### Quy trình thực hiện

1. Đọc yêu cầu và các hướng dẫn của repository; kiểm tra code liên quan, stack, cấu trúc và thay đổi đang có.
2. Xác định kết quả cần bàn giao và phạm vi đã được người dùng yêu cầu. Phân loại theo mục 12.
3. Chỉ đọc các mục liên quan trong `PROJECT_RULES.md`; đọc thêm `DESIGN_GUIDE.md` khi làm giao diện. Không áp dụng máy móc mọi mục.
4. Làm trực tiếp hoặc lập plan theo mức độ; hỏi trước mọi phần bổ sung ngoài phạm vi.
5. Thực hiện trong phạm vi đã thống nhất; bổ sung/cập nhật test cần thiết và chạy kiểm thử theo mục 12 trước khi bàn giao.
6. Báo phần đã làm, kết quả kiểm tra và phần còn thiếu. Commit/push/triển khai theo yêu cầu của người dùng.

### Ưu tiên và giới hạn

- Tập trung vào kết quả người dùng yêu cầu; chỉ sửa các phần cần thiết để đạt kết quả đó và kiểm thử phần bị ảnh hưởng. Không sửa file khác chỉ vì đang đọc thấy vấn đề.
- Nếu phát hiện vấn đề ngoài phạm vi, ghi nhận ngắn gọn để người dùng quyết định; không triển khai trước khi được đồng ý. Việc đọc code để hiểu phụ thuộc không mở rộng phạm vi được phép sửa.
- Tuân thủ hướng dẫn hệ thống và môi trường; trong phạm vi đó, yêu cầu cụ thể của người dùng và hướng dẫn áp dụng của repository được ưu tiên hơn mẫu trong skill.
- Với dự án đang chạy, giữ quy ước hiện có; chỉ chuyển cấu trúc, đổi stack hoặc chuẩn hóa hàng loạt khi người dùng yêu cầu rõ.
- Không tự thêm tính năng, màn hình, module, trường dữ liệu, quyền, tích hợp, thư viện hoặc dịch vụ chưa được yêu cầu/đồng ý.
- Không tự refactor phần không liên quan, nâng phiên bản hoặc thay đổi cấu hình môi trường để tiện triển khai một yêu cầu khác.
- Nếu phần bổ sung là điều kiện cần để hoàn thành yêu cầu, giải thích cần thêm gì, vì sao, tác động và phương án thay thế rồi hỏi. Chỉ thực hiện phần đó khi người dùng đồng ý; im lặng không phải sự đồng ý.
- Đề xuất cải tiến phải tách rõ khỏi phần đang thực hiện; đề xuất không đồng nghĩa với được phép triển khai.
- Những chỉnh sửa cần thiết trong phạm vi đã thống nhất không phải hỏi lại từng lần. Giữ nguyên thay đổi của người dùng và không đưa secret vào tài liệu hoặc commit.

### Kiểm tra trước khi dùng skill rộng rãi

- Thử với việc nhỏ: chỉ sửa đúng yêu cầu, không tạo plan dài hoặc thêm tính năng.
- Thử với module mới: xác định phạm vi, lập plan khi cần và tổ chức code theo quy tắc đã chọn.
- Thử với dự án có cấu trúc khác: đọc hiện trạng, giữ cấu trúc hiện có và hỏi trước khi đề xuất chuyển đổi.
- Thử với yêu cầu phát sinh thư viện/tính năng mới: phải hỏi và chờ đồng ý trước khi bổ sung.

Khi dùng cho dự án mới, thay module, dữ liệu và nghiệp vụ; giữ các quy ước nền tảng phù hợp. Không mặc định toàn bộ tính năng CRM đều là yêu cầu của dự án mới.
