# Getting started with VueJS

[[_TOC_]]

## I. Câu hỏi chung

### 1. Document Object Model (DOM)

Mô hình đối tượng tài liệu (DOM) là giao diện lập trình cho phép lập trình viên tương tác với các tài liệu dạng HTML và XML. Cây DOM là một cấu trúc phân cấp biểu thị trang web dưới dạng một cây các đối tượng (object). Mỗi nút (node) trong cây là một object, mỗi nhánh kết thúc bằng một node. Mối quan hệ (parent, children, sibling) giữa các node quyết định cấu trúc của cây DOM.

**Vai trò của DOM:**

- Truy cập và thao tác nội dung: DOM cho phép lập trình viên truy cập và thao tác nội dung của tài liệu, bao gồm văn bản, hình ảnh, liên kết, v.v.
Thay đổi giao diện: DOM cho phép lập trình viên thay đổi giao diện của tài liệu bằng cách thay đổi thuộc tính CSS của các phần tử HTML.
Tạo các ứng dụng web động: DOM là nền tảng cho các ứng dụng web động, cho phép lập trình viên tạo các trang web tương tác và có khả năng phản hồi.
Lợi ích của DOM:

- Độc lập với ngôn ngữ lập trình: DOM có thể được sử dụng với nhiều ngôn ngữ lập trình khác nhau, bao gồm JavaScript, Java, Python, C#, v.v.
Dễ sử dụng: DOM cung cấp một API đơn giản và dễ sử dụng để truy cập và thao tác tài liệu.
Mạnh mẽ: DOM cung cấp một bộ tính năng mạnh mẽ cho phép lập trình viên tạo các ứng dụng web phức tạp.

### 2. Cách thức Vue thao tác với DOM

**Virtual DOM:** Vue duy trì một bản sao của cấu trúc DOM thực tế trong bộ nhớ. DOM ảo là một cây đối tượng, phản ánh các phần tử HTML và thuộc tính của chúng.

**Reactivity System:** Vue theo dõi các thay đổi trong dữ liệu của thành phần. Khi dữ liệu thay đổi, Vue tự động cập nhật những thay đổi đó vào DOM ảo.

**Diffing:** Khi dữ liệu thay đổi, Vue tạo ra một cây DOM ảo mới và so sánh với DOM ảo cũ để xác định tập hợp tối thiểu các thay đổi cần thiết. Quá trình này gọi là diffing.

**Patching:** Vue chỉ áp dụng các thay đổi cần thiết cho DOM thực. Cách tiếp cận tối ưu này giúp giảm thiểu thao tác DOM, giúp cập nhật nhanh hơn và hiệu quả hơn.

## II. Một số thông tin về Nuxt 2

### 1. Cấu trúc project

Cấu trúc 1 Vue project cơ bản gồm:

```md
project
├── components
│   ├── ComponentA.vue
│   ├── ComponentB.vue
├── pages
│   ├── index.vue
│   ├── custom-page.vue
├── static
│   ├── favicon.ico
├── nuxt.config.js
├── package.json
├── ...
```

- Thư mục `pages`: chứa các views và routes của app.
- Thư mục `components`: chứa các tệp Vue components. Để tự động import custom component vào các page mà không cần import thủ công trong thẻ `<script>`, chỉ định `components: true` trong file `nuxt.config.js`.
- Thư mục `static`: được ánh xạ trực tiếp đến thư mục gốc (root) của máy chủ và chứa các tệp phải giữ nguyên tên hoặc gần như sẽ không thay đổi (vd: favicon.ico).
- File `nuxt.config.js`: là điểm cấu hình duy nhất cho Nuxt, có thể thêm module hoặc ghi đè cài đặt mặc định.
- File `package.json`: chứa các scripts và dependencies.

### 2. Cách thức routing trong Nuxt 2

Nuxt tự động tạo cấu hình `vue-router` dựa trên các tệp trong thư mục `pages`. Do đó không cần tạo tệp cấu hình (ví dụ `router.js`) thủ công nữa.

Để điều hướng giữa các trang, có thể sử dụng `<NuxtLink>` component hoặc thẻ `<a>`. NuxtLink có sẵn trong Nuxt, không cần import. Hai thẻ sử dụng tương đương nhau, nhưng nếu liên kết tới web ngoài nên dùng thẻ `<a>`.

```vue
<NuxtLink to="/">Internal link</NuxtLink>
<a href="https://v2.nuxt.com">External link</a>
```

## III. Hướng dẫn chạy code môi trường dev

**Bước 0 (optional):** Cài node và package manager

- Cài `nodejs`

```shell
sudo apt install -y nodejs
```

- Cài `yarn`

```shell
npm install --global yarn
```

- Version node và package manager sử dụng trên local:
  - **Nodejs:** 21.7.3
  - **Yarn:** 1.22.22

**Bước 1:** tạo project bằng câu lệnh

```shell
yarn create nuxt-app <project_name>
```

Trong quá trình tạo có 1 số options có thể không cần chọn và bỏ qua

![image](/imgs/yarn-create-options.png)

Chuyển thư mục làm việc vào project

```shell
cd <package_name>
```

**Bước 2 (optional):** Cài thêm module bổ sung

```shell
yarn add <package_name>
```

Ví dụ cài thêm module về `validate form` có version `3` (đối với Vue 2):

```shell
yarn add vee-validate@3
```

**Bước 3:** chạy chương trình

```shell
yarn dev
```

Truy cập vào `localhost:3000` hoặc nếu port 3000 đã dùng, một port khác sẽ được chọn random.
