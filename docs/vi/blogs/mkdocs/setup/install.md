# Hướng dẫn cài đặt MkDocs

## Yêu cầu hệ thống

Trước khi bắt đầu, hãy đảm bảo máy tính của bạn đáp ứng các yêu cầu sau:

- **Python**: Phiên bản 3.6 trở lên (tải từ [python.org](https://www.python.org/downloads/)).
- **PIP**: Trình quản lý gói Python (thường đi kèm với Python).
- **Trình soạn thảo văn bản**: VS Code, Sublime Text, hoặc bất kỳ editor nào bạn thích.

## Các bước cài đặt

### Bước 1: Cài đặt Python

1. Kiểm tra xem Python và pip đã cài chưa:

```bash
python --version # Hoặc python3 --version
pip --version
```

2. Nếu chưa cài, tải Python từ [python.org](https://www.python.org/downloads/) và cài đặt.

### Bước 2: Cài đặt MkDocs

```bash
pip install mkdocs # hoặc `pip3 install mkdocs`
mkdocs --version
```

### Step 3: Create a new project

```bash
mkdocs new my-project
cd my-project
```

- Lệnh này tạo file `mkdocs.yml` và thư mục `docs/` với `index.md`.

### Step 4: Local test run

```bash
mkdocs serve
```

- Mở trình duyệt và truy cập `http://localhost:8000` để xem trước trang web mặc định

### Step 5: Build static site

```bash
mkdocs build
```

- Kiểm tra thư mục `site/`để xem HTML tĩnh đã tạo.

### Step 6: Deploy to GitHub Pages

1. Initialize a Git repository:

```bash
git init
git add .
git commit -m "Initial commit"
```

2. Push to GitHub:

```bash
git remote add origin <URL>
git push -u origin main
```

3. Deploy to GitHub Pages:

```bash
mkdocs gh-deploy
```

- Truy cập `https://<username>.github.io/<repo>` để xem trang web đã triển khai.
- Xem thêm tại [MkDocs Deploying](https://www.mkdocs.org/user-guide/deploying-your-docs/).
