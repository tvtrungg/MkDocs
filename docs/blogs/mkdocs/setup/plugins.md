# Plugins

## Plugin là gì?

Plugin là các module Python mở rộng chức năng của MkDocs, từ tối ưu hóa hiệu suất đến thêm thông tin động. Chúng được cài qua PIP và cấu hình trong `mkdocs.yml`.

### Cài đặt Plugin

#### 1. Cài đặt plugin qua `pip`:

```bash
pip install <plugin-name>
```

#### 2. Thêm plugin vào file `mkdocs.yml`:

```yaml
plugins:
  - <plugin-name>
```

### Các plugin phổ biến

#### [1. mkdocs-minify-plugin](https://pypi.org/project/mkdocs-minify-plugin/)

- Chức năng: Tối ưu hóa hiệu suất trang web, nén HTML và CSS để tăng tốc độ tải.
- Cài đặt:

```bash
pip install mkdocs-minify-plugin
```

- Cấu hình:

```yaml
plugins:
  - minify
```

- Có thể kiểm tra sự khác biệt trước và sau khi sử dụng plugin này bằng cách sử dụng lệnh `mkdocs build`, so sánh thư mục `site/` trước và sau khi cài đặt.

#### 2. mkdocs-git-revision-date-plugin

- Chức năng: Hiển thị ngày cập nhật của trang dựa trên Git commit.
- Cài đặt:

```bash
pip install mkdocs-git-revision-date-plugin
```

- Cấu hình:

```yaml
plugins:
  - git-revision-date
```

#### [3. mkdocs-awesome-pages-plugin](https://pypi.org/project/mkdocs-awesome-pages-plugin/)


- Chức năng: Tự động tạo điều hướng từ cấu trúc thư mục `docs/`.
- Cài đặt:

```bash
pip install mkdocs-awesome-pages-plugin
```

- Cấu hình:

```yaml
plugins:
  - awesome-pages
```

- Ví dụ:

```text
docs/
├── index.md
├── setup/
│   └── install.md
└── usage/
    ├── extensions.md
    └── plugins.md
```

Menu sẽ tự động tạo ra các mục `Setup` và `Usage` từ cấu trúc thư mục.

#### 4. mkdocs-redirects

- Chức năng: Tạo chuyển hướng từ URL cũ sang URL mới.
- Cài đặt:

```bash
pip install mkdocs-redirects
```

- Cấu hình:

```yaml
plugins:
  - redirects
```

- Thêm chuyển hướng vào file `mkdocs.yml`:

```yaml
redirects:
  - from: /old-url
    to: /new-url
```

- Khi truy cập `/old-url`, trình duyệt sẽ tự động chuyển hướng sang `/new-url`.
