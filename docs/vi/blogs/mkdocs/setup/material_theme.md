# Material Theme

MkDocs hỗ trợ nhiều giao diện để làm đẹp tài liệu:

- **MkDocs mặc định**: Đơn giản, nhẹ, phù hợp dự án nhỏ.
- **ReadTheDocs**: Giao diện giống tài liệu Python, chuyên nghiệp.
- **Material**: Hiện đại, responsive, có thanh tìm kiếm và nhiều tính năng.

## Cài đặt theme

### Bước 1: Cài đặt theme

1. Cài đặt theme qua `pip`:

```bash
pip install mkdocs-material
```

2. Thêm theme vào file `mkdocs.yml`:

```yaml
theme:
  name: "material"
```

### Bước 2: Cấu hình theme

- **Logo và Favicon**: Thêm logo và favicon vào `extra`:

```yaml
theme:
  name: "material"
  logo: "images/logo.png"
  favicon: "images/favicon.ico"
```

- **Màu sắc**: Thay đổi màu sắc theme:

```yaml
theme:
  name: "material"
  palette:
    primary: "blue"
    accent: "blue"
```

- **Thanh tìm kiếm**: Bật thanh tìm kiếm:

```yaml
theme:
  name: "material"
  features:
    - search
```

- **Sidebar**: Thay đổi vị trí sidebar:

```yaml
theme:
  name: "material"
  features:
    - search
  nav:
    - Home: index.md
    - About: about.md
  sidebar:
    - Home: index.md
    - About:
        - "About MkDocs": about.md
        - "About Material": about-material.md
```

- **Tùy chỉnh khác**: Xem thêm tại [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
