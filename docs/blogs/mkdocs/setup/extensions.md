# Markdown Extensions

MkDocs hỗ trợ mở rộng cú pháp Markdown để tạo nội dung phong phú:

- **Code highlight**: Tô màu cú pháp code.
- **Table**: Tạo bảng dễ dàng.
- **Table of contents**: Tự động tạo mục lục.
- **Footnotes**: Thêm chú thích dưới trang.
- **Math**: Hiển thị công thức toán học.

## Cài đặt Extensions

Cài đặt các extension cần thiết qua `pip`:

```bash
pip install mkdocs-material
pip install pymdown-extensions
```

### Cấu hình Extensions

Thêm các extension vào file `mkdocs.yml`:

```yaml
markdown_extensions:
  - pymdownx.highlight    # Code highlight 
  - pymdownx.superfences  # Table
  - pymdownx.details      # Details
  - pymdownx.emoji        # Emoji
  - pymdownx.tasklist     # Task list
  - tables                # Table of contents
  - toc                   # Footnotes
  - ...
```
