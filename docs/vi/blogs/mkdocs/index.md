---
title: "MkDocs"
---

# Welcome to MkDocs

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

MkDocs là một **static site generator** (trình tạo trang web tĩnh) mạnh mẽ, được viết bằng Python, chuyên dùng để xây dựng tài liệu kỹ thuật, hướng dẫn sử dụng hoặc wiki nội bộ. Nó sử dụng cú pháp **Markdown** – một ngôn ngữ đánh dấu nhẹ, dễ viết và dễ đọc – để tạo nội dung, sau đó chuyển đổi thành các trang HTML tĩnh. MkDocs đặc biệt phù hợp cho các lập trình viên, kỹ sư phần mềm và doanh nghiệp muốn tạo tài liệu chuyên nghiệp mà không cần backend phức tạp.

## Tại sao nên sử dụng MkDocs?

- **Nhẹ và nhanh**: Không yêu cầu cơ sở dữ liệu hay server phức tạp, chỉ cần HTML tĩnh.
- **Dễ học**: Chỉ cần biết Markdown cơ bản là có thể bắt đầu.
- **Tùy chỉnh cao**: Hỗ trợ theme (giao diện), plugin (bổ sung tính năng), và tích hợp với GitHub Pages.
- **Miễn phí và mã nguồn mở**: Được cộng đồng phát triển, không chi phí bản quyền.

## MkDocs hoạt động như thế nào?

1. Bạn viết nội dung bằng Markdown trong thư mục `docs/`.
2. Cấu hình dự án qua file `mkdocs.yml`.
3. Chạy lệnh `mkdocs build` để tạo HTML tĩnh hoặc `mkdocs serve` để xem trước local.
4. Triển khai lên GitHub Pages hoặc bất kỳ web server nào với `mkdocs gh-deploy`.

## Project basic layout

```text
my-docs/
├── docs/
│   ├── index.md        # The documentation homepage.
|   └── ...             # Other markdown pages, images and other file
└── mkdocs.yml          # The configuration file.
```

## Commands

- `mkdocs new [dir-name]` - Create a new project.
- `mkdocs serve` - Start the live-reloading docs server.
- `mkdocs build` - Build the documentation site.
- `mkdocs -h` - Print help message and exit.

## Lợi ích trong doanh nghiệp

- Tạo tài liệu API, hướng dẫn sản phẩm, hoặc wiki nội bộ một cách nhanh chóng.
- Dễ bảo trì và cập nhật nhờ tích hợp với Git.
- Giao diện chuyên nghiệp với theme như **Material for MkDocs**.

Bắt đầu hành trình của bạn với MkDocs bằng cách xem [Hướng dẫn cài đặt](setup/install.md)!
