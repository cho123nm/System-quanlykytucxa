# 🏠 Hệ Thống Quản Lý Ký Túc Xá (Hostel Management System)

Hệ thống quản lý ký túc xá toàn diện được xây dựng bằng PHP và MySQL, hỗ trợ quản lý sinh viên, nhân viên, điểm danh, thanh toán và nhiều chức năng khác.

## 📋 Mục Lục

- [Tính Năng](#-tính-năng)
- [Phân Quyền](#-phân-quyền)
- [Cài Đặt](#-cài-đặt)
- [Cấu Trúc Thư Mục](#-cấu-trúc-thư-mục)
- [Hướng Dẫn Sử Dụng](#-hướng-dẫn-sử-dụng)
- [Công Nghệ](#-công-nghệ)

---

## ✨ Tính Năng

### 🔐 Hệ Thống Phân Quyền

- **4 cấp độ người dùng**: Admin, Supervisor, Employee, Student
- Phân quyền chi tiết theo từng chức năng
- Bảo mật session và authentication

### 👥 Quản Lý Sinh Viên

- Nhập học sinh viên mới
- Quản lý thông tin cá nhân
- Phân bổ phòng ở
- Quản lý đặt cọc
- Xem danh sách sinh viên

### 👨‍💼 Quản Lý Nhân Viên

- Thêm/sửa/xóa nhân viên
- Quản lý lương
- Phân công công việc
- Theo dõi hiệu suất

### ✅ Hệ Thống Điểm Danh

- **Sinh viên tự điểm danh** hàng ngày
- **Xin nghỉ phép** trực tuyến
- Xem lịch sử điểm danh
- Thống kê tỷ lệ có mặt
- Admin/Employee quản lý điểm danh
- Chặn điểm danh trùng lặp

### 🏠 Quản Lý Phòng Ở

- Xem thông tin phòng của mình
- Danh sách bạn cùng phòng
- Thông tin tòa nhà
- Tiền phòng hàng tháng
- Phân bổ chỗ ở

### 💰 Quản Lý Thanh Toán

- Thanh toán sinh viên
- Duyệt thanh toán
- Thanh toán nhà cung cấp
- Quản lý chi phí
- Tạo hóa đơn

### 📢 Thông Báo

- Tạo thông báo (Admin/Supervisor)
- Xem thông báo (Tất cả)
- Thông báo theo thời gian thực

### 🔧 Cài Đặt Hệ Thống

- Quản lý người dùng
- Cài đặt phí
- Cài đặt thời gian
- Quản lý tòa nhà/phòng

---

## 👤 Phân Quyền

### 🔴 Admin (UG001)

**Quyền cao nhất - Quản lý toàn bộ hệ thống**

- ✅ Tất cả chức năng của Supervisor
- ✅ Quản lý người dùng
- ✅ Cài đặt hệ thống
- ✅ Thiết lập phí, giá, thời gian
- ✅ Quản lý tòa nhà và phòng

### 🟡 Supervisor (UG002)

**Giám sát viên - Quản lý vận hành**

- ✅ Quản lý sinh viên
- ✅ Quản lý nhân viên
- ✅ Điểm danh
- ✅ Thanh toán và hóa đơn
- ✅ Tạo thông báo
- ❌ Cài đặt hệ thống

### 🔵 Employee (UG003)

**Nhân viên - Thực hiện công việc hàng ngày**

- ✅ Điểm danh sinh viên
- ✅ Xem thông báo
- ❌ Quản lý sinh viên
- ❌ Quản lý thanh toán

### 🟢 Student (UG004)

**Sinh viên - Quản lý thông tin cá nhân**

- ✅ Tự điểm danh hàng ngày
- ✅ Xin nghỉ phép
- ✅ Xem lịch sử điểm danh
- ✅ Xem thông tin phòng ở
- ✅ Xem bạn cùng phòng
- ✅ Xem thanh toán của mình
- ✅ Xem thông báo
- ❌ Không có quyền quản lý

---

## 🚀 Cài Đặt

### Yêu Cầu Hệ Thống

- PHP 7.4 trở lên
- MySQL 5.7 trở lên
- Apache/Nginx Web Server
- XAMPP/WAMP (khuyến nghị cho Windows)

### Các Bước Cài Đặt

1. **Clone Repository**

```bash
git clone https://github.com/cho123nm/System-quanlykytucxa.git
cd System-quanlykytucxa
```

2. **Cấu Hình Database**

- Tạo database mới tên `hms`
- Import file `hms (2).sql` vào database

```sql
CREATE DATABASE hms;
USE hms;
SOURCE hms (2).sql;
```

3. **Cấu Hình Kết Nối**

- Mở file `inc/dbPlayer.php`
- Cập nhật thông tin database:

```php
private $db_host = "localhost";
private $db_name = "hms";
private $db_user = "root";
private $db_pass = "";
```

4. **Chạy Script Fix Database**

- Mở phpMyAdmin
- Chạy script sau để chặn điểm danh trùng:

```sql
-- Xóa bản ghi trùng lặp
DELETE t1 FROM attendence t1
INNER JOIN attendence t2
WHERE t1.serial > t2.serial
AND t1.userId = t2.userId
AND DATE(t1.date) = DATE(t2.date);

-- Thêm UNIQUE constraint
ALTER TABLE attendence
ADD UNIQUE KEY unique_user_date (userId, date);
```

5. **Khởi Động Server**

- Đặt folder vào `C:\xampp\htdocs\hostex`
- Truy cập: `http://localhost/hostex`

### Tài Khoản Mặc Định

**Admin:**

- Username: `admin`
- Password: `admin123`

**Sinh viên:**

- Username: `U0012`
- Password: `123456`

---

## 📁 Cấu Trúc Thư Mục

```
hostex/
├── dist/                   # CSS, JS, Fonts, Images
│   ├── css/               # Bootstrap, Font Awesome, Custom CSS
│   ├── js/                # jQuery, DataTables, Custom JS
│   ├── fonts/             # Font files
│   └── images/            # Logo, backgrounds
│
├── files/                 # Upload files
│   └── photos/            # Ảnh sinh viên, nhân viên
│
├── inc/                   # Core PHP Classes
│   ├── dbPlayer.php       # Database handler
│   ├── sessionManager.php # Session management
│   ├── handyCam.php       # Helper functions
│   ├── fileUploader.php   # File upload handler
│   └── fpdf.php           # PDF generator
│
├── site/                  # Landing page assets
│   ├── css/
│   ├── js/
│   ├── fonts/
│   └── images/
│
├── ui/                    # Main application pages
│   ├── attendence/        # Điểm danh
│   │   ├── student_checkin.php    # Sinh viên tự điểm danh
│   │   ├── request_leave.php      # Xin nghỉ phép
│   │   ├── my_attendance.php      # Lịch sử điểm danh
│   │   ├── add.php                # Admin thêm điểm danh
│   │   └── list_simple.php        # Danh sách điểm danh
│   │
│   ├── studentManage/     # Quản lý sinh viên
│   │   ├── studentlist.php        # Danh sách sinh viên
│   │   ├── admission.php          # Nhập học
│   │   ├── my_room.php            # Thông tin phòng ở
│   │   ├── seatalocation.php      # Phân bổ chỗ ở
│   │   └── deposit.php            # Quản lý đặt cọc
│   │
│   ├── employee/          # Quản lý nhân viên
│   │   ├── view.php               # Danh sách nhân viên
│   │   ├── add.php                # Thêm nhân viên
│   │   ├── salaryadd.php          # Thêm lương
│   │   └── salaryview.php         # Xem lương
│   │
│   ├── stdpayment/        # Thanh toán sinh viên
│   │   ├── view.php               # Danh sách thanh toán
│   │   ├── approvallist.php       # Duyệt thanh toán
│   │   └── my_payments.php        # Thanh toán của tôi
│   │
│   ├── payment/           # Thanh toán NCC
│   ├── bill/              # Quản lý hóa đơn
│   ├── cost/              # Quản lý chi phí
│   ├── notice/            # Thông báo
│   ├── setting/           # Cài đặt hệ thống
│   ├── setup/             # Thiết lập
│   └── usr/               # Thông tin người dùng
│
├── index.php              # Trang đăng nhập
├── dashboard.php          # Trang chủ
├── main.php               # Layout chính
├── footer.php             # Footer
├── logout.php             # Đăng xuất
├── page_403.php           # Trang lỗi 403
└── hms (2).sql            # Database schema
```

---

## 📖 Hướng Dẫn Sử Dụng

### Dành Cho Sinh Viên

#### 1. Điểm Danh Hàng Ngày

1. Đăng nhập vào hệ thống
2. Vào menu **Điểm danh** → **Điểm danh ngay**
3. Nhấn nút **"Điểm danh ngay"**
4. Hệ thống sẽ ghi nhận và hiển thị thông báo thành công
5. Chỉ được điểm danh 1 lần/ngày

#### 2. Xin Nghỉ Phép

1. Vào menu **Điểm danh** → **Xin nghỉ phép**
2. Chọn ngày nghỉ
3. Nhập lý do nghỉ
4. Nhấn **"Gửi đơn xin nghỉ"**

#### 3. Xem Thông Tin Phòng Ở

1. Vào menu **Phòng ở của tôi**
2. Xem thông tin:
   - Tòa nhà và số phòng
   - Tiền phòng/tháng
   - Danh sách bạn cùng phòng
   - Thông tin liên hệ bạn cùng phòng

### Dành Cho Admin/Supervisor

#### 1. Quản Lý Sinh Viên

- **Thêm sinh viên mới**: Quản lý sinh viên → Nhập học mới
- **Phân phòng**: Quản lý sinh viên → Phân bổ chỗ ở
- **Xem danh sách**: Quản lý sinh viên → Danh sách sinh viên

#### 2. Quản Lý Điểm Danh

- **Xem danh sách**: Điểm danh → Danh sách điểm danh
- **Thêm điểm danh**: Điểm danh → Thêm điểm danh
- **Thống kê**: Xem tỷ lệ có mặt, nghỉ phép, vắng không phép

#### 3. Quản Lý Thanh Toán

- **Duyệt thanh toán**: Thanh toán sinh viên → Duyệt thanh toán
- **Tạo hóa đơn**: Quản lý hóa đơn → Tạo hóa đơn

---

## 💻 Công Nghệ

### Backend

- **PHP 7.4+** - Server-side scripting
- **MySQL** - Database management
- **FPDF** - PDF generation

### Frontend

- **HTML5/CSS3** - Markup & styling
- **Bootstrap 3** - Responsive framework
- **jQuery** - JavaScript library
- **DataTables** - Table plugin
- **Font Awesome** - Icons
- **Morris.js** - Charts

### Libraries & Tools

- **Session Management** - Custom PHP session handler
- **Database Layer** - Custom PDO wrapper
- **File Upload** - Custom file handler
- **Date Picker** - Bootstrap Datepicker
- **Calendar** - Custom calendar widget

---

## 🔒 Bảo Mật

- ✅ Session-based authentication
- ✅ Role-based access control (RBAC)
- ✅ SQL injection prevention
- ✅ XSS protection
- ✅ CSRF token (recommended to add)
- ✅ Password hashing (recommended to upgrade)

---

## 📝 Ghi Chú

### Tính Năng Đã Bỏ

- ❌ Quản lý bữa ăn (đã bỏ để đơn giản hóa)

### Tính Năng Mới

- ✅ Điểm danh tự động cho sinh viên
- ✅ Xin nghỉ phép trực tuyến
- ✅ Xem thông tin phòng ở
- ✅ Chặn điểm danh trùng lặp
- ✅ Trang lỗi 403

### Cải Tiến

- ✅ Giao diện thân thiện hơn
- ✅ Phân quyền rõ ràng
- ✅ Thống kê chi tiết
- ✅ Responsive design

---

## 🐛 Báo Lỗi

Nếu bạn phát hiện lỗi, vui lòng tạo issue trên GitHub:
https://github.com/cho123nm/System-quanlykytucxa/issues

---

## 📄 License

MIT License - Tự do sử dụng cho mục đích học tập và thương mại.

---

## 👨‍💻 Tác Giả

**devTV**

- GitHub: [@cho123nm](https://github.com/cho123nm)
- Date: 15/11/2025

---

## 🙏 Cảm Ơn

Cảm ơn bạn đã sử dụng Hệ Thống Quản Lý Ký Túc Xá!

Nếu thấy hữu ích, hãy cho repo một ⭐ trên GitHub!
