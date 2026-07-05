# Module Quản lý kho mỹ phẩm (Odoo 7)

**TRƯỜNG ĐẠI HỌC CÔNG NGHỆ SÀI GÒN**

**KHOA CÔNG NGHỆ THÔNG TIN**

---

## BÀI TẬP NHÓM GIỮA KỲ MÔN: TRIỂN KHAI DỰ ÁN THÔNG TIN

### Tên đề tài: Xây dựng module Quản lý kho mỹ phẩm

- **Giáo viên hướng dẫn:** Ths. Nguyễn Lạc An Thư
- **Sinh viên thực hiện:**
  - Nguyễn Thị Kim Tỏa (DH52201581) - [GitHub](https://github.com/Kimtoa1905)
  - Nguyễn Quốc Tịnh (DH52201580) - [GitHub](https://github.com/quoctinh-dev)
- **Lớp:** D22_TH02

---

## Giới thiệu

Module `ql_kho_mypham` là một giải pháp quản lý kho được xây dựng trên nền tảng OpenERP 7, chuyên biệt cho việc quản lý các sản phẩm mỹ phẩm. Module cung cấp các chức năng cốt lõi từ quản lý danh mục, sản phẩm cho đến các nghiệp vụ kho hàng ngày như nhập, xuất và báo cáo tồn kho.

## Các chức năng chính

Module cung cấp một bộ công cụ toàn diện để quản lý kho mỹ phẩm:

- **Quản lý Danh mục:** Phân loại sản phẩm một cách khoa học (ví dụ: Skin Care, Make Up).
- **Quản lý Sản phẩm:** Quản lý thông tin chi tiết của từng sản phẩm như mã, tên, hình ảnh, và danh mục.
- **Quản lý Phiếu kho:**
  - Tạo và quản lý **phiếu nhập kho** để ghi nhận hàng hóa vào kho.
  - Tạo và quản lý **phiếu xuất kho** để ghi nhận hàng hóa bán ra hoặc sử dụng.
  - Quản lý vòng đời phiếu kho với các trạng thái (Nháp, Hoàn tất).
- **Báo cáo tồn kho:** Cung cấp cái nhìn tổng quan về số lượng tồn kho của tất cả sản phẩm, giúp đưa ra quyết định kinh doanh kịp thời.

## Các ràng buộc toàn vẹn (RBTV) nổi bật

Hệ thống được xây dựng với nhiều ràng buộc nghiệp vụ chặt chẽ để đảm bảo tính chính xác và toàn vẹn của dữ liệu:

### 1. Quản lý Danh mục & Sản phẩm (Master Data)
- **Tên phải là duy nhất:** Tên danh mục không được trùng lặp (không phân biệt hoa thường).
- **Chuẩn hóa dữ liệu:** Tên danh mục và sản phẩm được tự động chuẩn hóa (viết hoa chữ cái đầu, xóa khoảng trắng thừa) trước khi lưu.
- **Bảo vệ dữ liệu tham chiếu:** Không cho phép xóa danh mục hoặc sản phẩm nếu đã phát sinh giao dịch liên quan.
- **Sinh mã tự động:** Mã sản phẩm được sinh tự động theo một chuỗi đã định nghĩa (ví dụ: `SP0001`), đảm bảo tính duy nhất và nhất quán.

### 2. Nghiệp vụ Kho (Stock Operations)
- **Không xuất âm kho:** Hệ thống sẽ ngăn chặn việc hoàn tất phiếu xuất nếu số lượng xuất lớn hơn tồn kho hiện tại.
- **Tính toàn vẹn của phiếu kho:**
  - Một sản phẩm chỉ xuất hiện một lần trên một phiếu.
  - Phiếu kho đã "Hoàn tất" sẽ không thể sửa hoặc xóa.
  - Không cho phép hoàn tất một phiếu rỗng (không có sản phẩm).
- **Cập nhật tồn kho chính xác:** Tồn kho chỉ được cập nhật khi phiếu kho ở trạng thái "Hoàn tất". Các phiếu ở trạng thái "Nháp" không ảnh hưởng đến số lượng tồn.
- **Sinh số phiếu tự động:** Số phiếu nhập/xuất được sinh tự động theo chuỗi riêng biệt (ví dụ: `PN0001`, `PX0001`).

## Hướng dẫn cài đặt

Để cài đặt module vào hệ thống OpenERP 7, vui lòng thực hiện các bước sau:

1.  **Sao chép module:**
    - Sao chép toàn bộ thư mục `ql_kho_mypham` vào thư mục `addons` của máy chủ OpenERP.

2.  **Khởi động lại máy chủ:**
    - Khởi động lại dịch vụ OpenERP Server để máy chủ nhận diện module mới.

3.  **Cập nhật danh sách module (Chế độ nhà phát triển):**
    - Đăng nhập vào OpenERP với tài khoản quản trị.
    - Kích hoạt chế độ nhà phát triển (Developer Mode).
    - Vào menu `Cài đặt (Settings)` > `Cập nhật danh sách Apps (Update Apps List)`.
    - Một hộp thoại sẽ hiện ra, nhấn `Cập nhật (Update)`.

4.  **Cài đặt module:**
    - Vào menu `Cài đặt (Settings)` > `Apps`.
    - Bỏ bộ lọc `Apps` mặc định và tìm kiếm với từ khóa `Quan Ly Kho My Pham`.
    - Nhấn nút `Cài đặt (Install)` trên module.

5.  **Kiểm tra:**
    - Sau khi cài đặt thành công, một menu mới có tên **"Quản lý kho mỹ phẩm"** sẽ xuất hiện trên thanh menu chính.

## Cấu trúc Module

Module được tổ chức theo cấu trúc chuẩn của OpenERP 7 để đảm bảo tính rõ ràng và dễ bảo trì:

```
ql_kho_mypham/
├── __init__.py             # Khởi tạo module, import thư mục models
├── __openerp__.py          # File cấu hình chính của module
├── sequence.xml            # Định nghĩa các chuỗi sinh mã tự động
├── demo/
│   └── demo_data.xml       # Dữ liệu mẫu để kiểm thử
├── models/
│   ├── __init__.py
│   ├── category.py         # Model quản lý danh mục
│   ├── product.py          # Model quản lý sản phẩm
│   ├── stock_document.py   # Model quản lý phiếu kho
│   └── stock_document_line.py # Model quản lý chi tiết phiếu kho
├── security/
│   ├── ir.model.access.csv # Phân quyền truy cập vào các model
│   └── security.xml        # Định nghĩa các nhóm người dùng (roles)
├── static/
│   └── description/
│       └── icon.png        # Icon của module
└── views/
    ├── category_view.xml
    ├── product_view.xml
    ├── stock_document_view.xml
    ├── stock_report_view.xml
    └── menu.xml            # Định nghĩa cấu trúc menu
```

## Phân quyền người dùng

Module định nghĩa 2 nhóm người dùng chính để kiểm soát quyền truy cập:

- **Nhân viên kho (`group_stock_user`):**
  - Có quyền xem dữ liệu (danh mục, sản phẩm).
  - Có quyền tạo và sửa phiếu kho ở trạng thái "Nháp".
  - Không có quyền xóa phiếu kho.
- **Quản lý kho (`group_stock_manager`):**
  - Kế thừa toàn bộ quyền của Nhân viên kho.
  - Có toàn quyền (tạo, đọc, sửa, xóa) trên tất cả các đối tượng của module.

## Dữ liệu mẫu (Demo Data)

Khi cài đặt, module sẽ tự động tạo ra một bộ dữ liệu mẫu bao gồm:
- Danh mục sản phẩm (`Skin Care`, `Make Up`).
- Sản phẩm (`Kem Dưỡng Ẩm`, `Son Lì`).
- Một phiếu nhập kho đã hoàn tất.
- Một phiếu xuất kho đã hoàn tất.

Dữ liệu này giúp người dùng mới có thể nhanh chóng trải nghiệm và kiểm thử các chức năng của hệ thống.

## Tài liệu tham khảo

1.  Lab Triển Khai Hệ Thống Thông Tin – Tài liệu giảng dạy môn Triển khai hệ thống thông tin, Trường Đại học Công Nghệ Sài Gòn.
2.  Odoo 7 Documentation.
