# Dong DevKit

Bộ skill hướng dẫn tổ chức frontend/backend và thiết kế giao diện, áp dụng theo phạm vi người dùng yêu cầu.

## Cài project-base cho Codex

Cần Node.js/npm để chạy lệnh:

```sh
npx skills add dongnt48/dong-devkit --skill project-base --agent codex --global
```

Lệnh cài skill vào phạm vi người dùng để sử dụng cho nhiều dự án. Bỏ `--global` nếu muốn cài cho dự án hiện tại.

## Sử dụng

```text
$project-base Tạo module khách hàng gồm list, create, edit và detail.
```

Skill đọc hiện trạng trước, làm trực tiếp với việc đơn giản và lập plan với việc phức tạp. Chỉ thực hiện phạm vi đã thống nhất, hỏi trước phần bổ sung và kiểm thử trước khi bàn giao.

## Nội dung

- [SKILL.md](skills/project-base/SKILL.md): điều kiện sử dụng và quy trình.
- [PROJECT_RULES.md](skills/project-base/references/PROJECT_RULES.md): cấu trúc FE/BE, API, dữ liệu, quyền, test và triển khai.
- [DESIGN_GUIDE.md](skills/project-base/references/DESIGN_GUIDE.md): bố cục, màu sắc và các mẫu giao diện.

Đây là skill hướng dẫn, không phải bộ source ứng dụng. Module và công nghệ mẫu chỉ áp dụng khi phù hợp yêu cầu.

CLI cài đặt: [vercel-labs/skills](https://github.com/vercel-labs/skills).
