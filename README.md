# LIVORA - NỀN TẢNG THƯƠNG MẠI ĐIỆN TỬ NỘI THẤT TƯƠNG TÁC
> **BÁO CÁO VÀ SOURCE CODE NỘP BÀI ĐỒ ÁN MÔN LẬP TRÌNH WEB NÂNG CAO**  
> **Nhóm thực hiện:** Nhóm 09  

---

## 📌 1. Giới thiệu tổng quan đề tài

**LIVORA** là giải pháp nền tảng thương mại điện tử chuyên ngành nội thất hiện đại, tích hợp công cụ phối cảnh không gian tương tác (Room Planner), quản lý đơn hàng theo chu trình logistics chuẩn (Xác nhận → Phiếu xuất bán → Đang giao → Hoàn thành / Hoàn trả), phân quyền đa vai trò (RBAC) và hệ thống báo cáo quản trị chuyên sâu.

Dự án được xây dựng theo kiến trúc 3 tầng (3-tier Architecture) tách bạch:
* **`livora_user`**: Website dành cho Khách hàng (Client Portal) - Trải nghiệm mua sắm, phối cảnh phòng, theo dõi đơn hàng và tra cứu bằng mã OTP.
* **`livora_admin`**: Website dành cho Quản trị viên (Admin Portal) - Quản lý sản phẩm, đơn hàng, xuất bán kho, xử lý hoàn tiền, chăm sóc khách hàng, phân quyền và dashboard phân tích tài chính.
* **`livora_backend`**: Hệ thống RESTful API Server - Quản lý nghiệp vụ tập trung, kiểm soát xác thực (JWT), kết nối cơ sở dữ liệu MongoDB Atlas, xử lý transaction tính giá đơn hàng và quản lý tài nguyên.

---

## 🌐 2. Đường dẫn trải nghiệm trực tuyến (Live Demo)

* 🛍️ **Website Khách hàng (User):** [https://livora-user.netlify.app](https://livora-user.netlify.app)
* ⚙️ **Website Quản trị (Admin):** [https://livora-admin.netlify.app](https://livora-admin.netlify.app)
* 🚀 **Backend REST API (Render):** [https://livora-backend-t8w8.onrender.com/api/health](https://livora-backend-t8w8.onrender.com/api/health)

---

## 🔐 3. Tài khoản trải nghiệm hệ thống (Demo Accounts)

### Phân hệ Quản trị (`livora_admin`):
| Vai trò (Role) | Tên đăng nhập | Mật khẩu | Quyền hạn và phân hệ phụ trách |
| :--- | :--- | :---: | :--- |
| **Super Admin** | `admin` | `123456` | Toàn quyền quản trị toàn bộ hệ thống, phân quyền và cấu hình |
| **Kế toán** | `ketoan` | `123456` | Xem báo cáo tài chính/doanh thu, duyệt và xử lý phiếu hoàn tiền |
| **Vận hành / Sale** | `vanhanh` | `123456` | Quản lý đơn hàng, duyệt xuất kho bán hàng, voucher và vận chuyển |
| **Nội dung** | `noidung` | `123456` | Quản lý danh mục sản phẩm, danh sách phòng, không gian thiết kế và banner |
| **CSKH** | `cskh` | `123456` | Tiếp nhận và phản hồi liên hệ, kiểm duyệt đánh giá của khách hàng |

### Phân hệ Khách hàng (`livora_user`):
* Người dùng có thể đăng ký tài khoản thành viên mới trực tiếp trên website.
* Hoặc đăng nhập tài khoản mẫu: `test@livora.vn` (Mật khẩu: `123456`).
* Hỗ trợ đặt hàng trực tiếp dạng **Khách vãng lai (Guest)** không cần đăng nhập (xác thực tra cứu và hủy đơn bằng mã OTP).

---

## 🛠️ 4. Công nghệ sử dụng trong dự án

* **Frontend:**
  * Angular 19 (Standalone Components, Signals, Reactive Forms, Router)
  * TypeScript 5.5+
  * HTML5 Canvas (Công cụ phối cảnh tương tác Room Planner)
  * Tailwind CSS & Bootstrap Icons
* **Backend:**
  * Node.js & Express.js
  * RESTful API Architecture
  * JWT (JSON Web Token) & Bcrypt password hashing
  * CORS, Dotenv, Cookie-parser
* **Database & Storage:**
  * MongoDB Atlas (Cloud Database)
  * Mongoose ODM (Schema Validation, Indexes, Population, Transactions)
* **DevOps & Hosting:**
  * Git & GitHub
  * Netlify (Frontend User & Admin SPA Hosting)
  * Render (Backend Node.js API Web Service)

---

## 🚀 5. Hướng dẫn cài đặt và khởi chạy Localhost

### Yêu cầu môi trường:
* **Node.js:** Phiên bản >= 18.x (khuyên dùng Node.js 20.x hoặc 22.x)
* **npm:** Phiên bản >= 9.x
* **Angular CLI:** `npm install -g @angular/cli` (tùy chọn)

---

### Bước 1: Khởi chạy Backend (`livora_backend`)

```bash
cd livora_backend

# 1. Cài đặt các thư viện phụ thuộc
npm install

# 2. Cấu hình biến môi trường
# Tạo file .env dựa trên file .env.example
cp .env.example .env
# Điền chuỗi kết nối MongoDB Atlas của bạn vào MONGODB_URI trong file .env

# 3. Khởi chạy máy chủ Backend
npm run dev
# Máy chủ sẽ lắng nghe tại: http://localhost:5000 (hoặc PORT được cấu hình)
```

---

### Bước 2: Khởi chạy Quản trị viên (`livora_admin`)

Mở một cửa sổ Terminal mới:

```bash
cd livora_admin

# 1. Cài đặt các thư viện
npm install

# 2. Khởi chạy ứng dụng Admin
npm start
# Hoặc: ng serve --port 4201

# Truy cập trình duyệt: http://localhost:4201
```

---

### Bước 3: Khởi chạy Website Khách hàng (`livora_user`)

Mở một cửa sổ Terminal mới:

```bash
cd livora_user

# 1. Cài đặt các thư viện
npm install

# 2. Khởi chạy ứng dụng Khách hàng
npm start
# Hoặc: ng serve --port 4200

# Truy cập trình duyệt: http://localhost:4200
```

---

## 📂 6. Cấu trúc thư mục mã nguồn

```text
LIVORA-SUBMISSION/
├── livora_backend/              # Source code API Server (Node.js/Express)
│   ├── src/
│   │   ├── config/              # Cấu hình CSDL MongoDB, CORS, Seeder mẫu
│   │   ├── controllers/         # Bộ điều khiển nghiệp vụ (20+ controllers)
│   │   ├── middleware/          # Xác thực JWT, phân quyền Admin & Customer
│   │   ├── models/              # Định nghĩa Mongoose Schemas (20+ models)
│   │   ├── routes/              # Định tuyến RESTful API endpoints
│   │   └── services/            # Xử lý tính giá đơn hàng, phí vận chuyển
│   ├── .env.example             # Mẫu cấu hình môi trường
│   ├── package.json
│   └── server.js                # Entry point máy chủ Express
│
├── livora_admin/                # Ứng dụng Quản trị viên (Angular 19)
│   ├── src/app/
│   │   ├── customer_management/ # Quản lý khách hàng & lịch sử chi tiêu
│   │   ├── dashboard/           # Báo cáo doanh thu, sản phẩm, không gian
│   │   ├── homepage/            # Quản trị nội dung trang chủ, banner
│   │   ├── interaction_management/ # Quản lý liên hệ và đánh giá sản phẩm
│   │   ├── order_management/    # Xử lý đơn hàng, phiếu xuất bán, hoàn tiền
│   │   ├── product_management/  # Quản lý danh mục & sản phẩm nội thất
│   │   ├── room_management/     # Quản lý phòng mẫu, không gian và cảm hứng
│   │   └── settings/            # Thiết lập voucher, vận chuyển, phân quyền RBAC
│   ├── angular.json
│   └── package.json
│
├── livora_user/                 # Ứng dụng Khách hàng (Angular 19)
│   ├── src/app/
│   │   ├── features/
│   │   │   ├── home/            # Trang chủ hiển thị danh mục, banner, sản phẩm
│   │   │   ├── login/           # Đăng nhập, đăng ký, quên mật khẩu
│   │   │   ├── module-3/        # Giỏ hàng & luồng thanh toán Checkout VietQR/COD
│   │   │   ├── module-4/        # Tra cứu đơn hàng vãng lai qua mã OTP
│   │   │   ├── module-5/        # Hồ sơ cá nhân, lịch sử đơn hàng, đánh giá
│   │   │   └── rooms/           # Phối cảnh không gian nội thất Canvas 2D/3D
│   │   └── services/            # Tầng dịch vụ giao tiếp RESTful API
│   ├── angular.json
│   └── package.json
│
├── artifact/                    # Tài liệu đặc tả phân tích thiết kế hệ thống
├── .gitignore                   # Cấu hình loại trừ file rác, file nhạy cảm
└── README.md                    # Hướng dẫn tổng quan và vận hành đồ án
```

---

## 🌟 7. Các tính năng nghiệp vụ trọng tâm đã hoàn thiện

1. **Phối cảnh không gian nội thất tương tác (Room Planner):**
   - Lựa chọn không gian phòng mẫu định sẵn (Templates).
   - Kéo thả sản phẩm nội thất trên HTML5 Canvas theo tọa độ không gian.
   - Gợi ý sản phẩm đồng bộ theo danh mục và phong cách phòng (Rule-based).
   - Dự toán tổng chi phí mặt bằng và chuyển đổi sang giỏ hàng/thanh toán.
2. **Quy trình Quản lý Đơn hàng & Logistics chuẩn:**
   - Đặt hàng (Kiểm tra tồn kho khả dụng, tính toán phí vận chuyển động và voucher).
   - Xác nhận đơn → Tự động sinh **Phiếu xuất bán** trong hệ thống.
   - Thao tác xuất kho: Trừ tồn kho sản phẩm, ghi nhận lịch sử và kích hoạt bước vận chuyển.
   - Chuyển trạng thái sang *Đang giao* và *Hoàn thành*.
3. **Quy trình Hủy đơn & Hoàn tiền đa tầng:**
   - Khách vãng lai được phép hủy đơn an toàn thông qua mã OTP gửi về số điện thoại/email.
   - Tự động hoàn lại tồn kho khả dụng và khôi phục lượt dùng voucher.
   - Đơn đã thanh toán trực tuyến tự động sinh yêu cầu hoàn tiền cho Kế toán thẩm định.
   - Nghiệp vụ nhập kho hàng hoàn trả đối với đơn hàng đã giao thành công.
4. **Phân quyền người dùng đa cấp (RBAC):**
   - 5 vai trò quản trị phân định rõ ràng quyền hạn route, chức năng và menu hiển thị.
   - Bảo mật mật khẩu người dùng với thuật toán mã hóa Bcrypt salt rounds.
   - Cơ chế tự động khóa tài khoản khi đăng nhập sai quá số lần quy định.
5. **Dashboard báo cáo quản trị chuyên sâu:**
   - Phân tích chỉ số tài chính: Doanh thu theo mốc thời gian, AOV (Giá trị đơn hàng trung bình).
   - Phân khúc khách hàng RFM và đo lường tỷ lệ chuyển đổi không gian.

---
*Đồ án hoàn thành bởi Nhóm 09 - Môn Lập trình Web Nâng cao.*
