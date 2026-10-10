# [Thực hành] Chuyển đổi CSS có sẵn sang SASS theo chuẩn

Dự án thực hành tái cấu trúc (refactoring) một file CSS truyền thống sang kiến trúc **SASS/SCSS chuẩn hóa**, phân tách thành các biến (variables), mixins, partials và tổ chức cấu trúc thư mục module hóa chuyên nghiệp.

---

## 1. File CSS Ban Đầu (`styles-original.css`)
```css
body {
  font-family: Arial, sans-serif;
  color: #333;
  background: #f4f4f4;
}

.container {
  width: 80%;
  margin: 0 auto;
}

.button {
  background: blue;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}

.card {
  border: 1px solid #ddd;
  padding: 20px;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
}
```

---

## 2. Quá Trình Chuyển Đổi Sang SASS Chuẩn

### 🔹 Bước 1: Định nghĩa Biến (`abstracts/_variables.scss`)
Tập trung toàn bộ giá trị dùng chung (màu sắc, viền, đổ bóng) để dễ bảo trì:
```scss
$primary-color: blue;
$text-color: #333;
$background-color: #f4f4f4;
$border-color: #ddd;
$box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
```

### 🔹 Bước 2: Tạo Mixins Tái Sử Dụng (`abstracts/_mixins.scss`)
Đóng gói các khối thuộc tính thường dùng với tham số linh hoạt:
```scss
@mixin button-style($bg-color) {
  background: $bg-color;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}

@mixin box-shadow {
  box-shadow: $box-shadow;
}
```

### 🔹 Bước 3: Phân chia Partials theo Chức Năng
- **`base/_global.scss`**: Định dạng nền tảng cho `body`.
- **`layout/_container.scss`**: Định dạng bố cục khung bao `.container`.
- **`components/_buttons.scss`**: Định dạng component nút bấm `.button` bằng mixin.
- **`components/_cards.scss`**: Định dạng component thẻ `.card` bằng mixin đổ bóng.

### 🔹 Bước 4: Tập hợp toàn bộ vào `main.scss`
```scss
@import "abstracts/variables";
@import "abstracts/mixins";
@import "base/global";
@import "layout/container";
@import "components/buttons";
@import "components/cards";
```

---

## 3. Cấu Trúc Thư Mục Dự Án

```text
chuyen-doi-css-sang-sass/
├── abstracts/
│   ├── _variables.scss     # Khai báo các biến màu, font, shadow
│   └── _mixins.scss        # Khai báo các mixin tái sử dụng
├── base/
│   └── _global.scss        # Định dạng toàn cục body
├── layout/
│   └── _container.scss     # Định dạng layout container
├── components/
│   ├── _buttons.scss       # Định dạng nút bấm button
│   └── _cards.scss         # Định dạng thẻ card
├── main.scss               # Tệp SCSS chính import toàn bộ partials
├── main.css                # File CSS kết quả được biên dịch từ main.scss
├── main.css.map            # Sourcemap cho CSS
├── styles-original.css     # File CSS ban đầu để đối chiếu
├── index.html              # Trang giao diện trực quan sử dụng CSS biên dịch
├── package.json            # Cấu hình lệnh build và watch
└── README.md               # Tài liệu hướng dẫn
```

---

## 4. Hướng Dẫn Biên Dịch SCSS sang CSS

Chạy lệnh SASS CLI trực tiếp:
```bash
sass main.scss main.css
```

Kích hoạt chế độ theo dõi tự động:
```bash
sass main.scss main.css --watch
```

Hoặc sử dụng npm scripts:
```bash
npm run build
npm run watch
```
