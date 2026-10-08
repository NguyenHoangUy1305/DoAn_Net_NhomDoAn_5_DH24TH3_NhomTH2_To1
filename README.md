# 🏥 HỆ THỐNG QUẢN LÝ BỆNH NHÂN & ĐƠN THUỐC BỆNH VIỆN (.NET WINFORMS)

<p align="center">
  <img src="https://img.shields.io/badge/.NET_Framework-4.8-512BD4?style=for-the-badge&logo=dotnet&logoColor=white" alt=".NET Framework 4.8" />
  <img src="https://img.shields.io/badge/C%23-10.0-239120?style=for-the-badge&logo=csharp&logoColor=white" alt="C#" />
  <img src="https://img.shields.io/badge/UI-Windows_Forms-0078D7?style=for-the-badge&logo=windows&logoColor=white" alt="Windows Forms" />
  <img src="https://img.shields.io/badge/Database-SQL_Server-CC292B?style=for-the-badge&logo=microsoftsqlserver&logoColor=white" alt="SQL Server" />
  <img src="https://img.shields.io/badge/ORM-Entity_Framework_6.5-68217A?style=for-the-badge" alt="Entity Framework" />
</p>

---

## 📌 1. TỔNG QUAN ĐỀ TÀI
* **Môn học:** Lập trình .NET (TIE501)
* **Đơn vị đào tạo:** Khoa Công nghệ Thông tin – Trường Đại học An Giang (ĐHQG TP.HCM)
* **Giảng viên hướng dẫn:** ThS. Nguyễn Ngọc Minh
* **Sinh viên thực hiện:**
  - **Nguyễn Hoàng Uy** (MSSV: `DTH235812`) – Lớp: DH24TH3
  - **Tạ Nguyễn Thành Tín** (MSSV: `DTH235787`) – Lớp: DH24TH3

Ứng dụng **Quản lý bệnh nhân** là giải pháp phần mềm máy tính (Desktop App) phục vụ quy trình số hóa toàn diện tại các phòng khám và cơ sở y tế. Hệ thống giải quyết triệt để các khó khăn của mô hình quản lý sổ sách truyền thống: thất lạc hồ sơ bệnh án, tính toán tiền thuốc thủ công sai sót, khó khăn khi tra cứu lịch sử khám bệnh và kiểm kê tồn kho dược phẩm.

---

## 🏗️ 2. KIẾN TRÚC & CÔNG NGHỆ ÁP DỤNG

| Thành phần | Công nghệ / Thư viện | Mô tả chi tiết |
| :--- | :--- | :--- |
| **Platform** | .NET Framework 4.8 | Nền tảng phát triển ứng dụng Windows tiêu chuẩn doanh nghiệp |
| **Language** | C# | Lập trình hướng đối tượng (OOP), quản lý sự kiện và luồng dữ liệu |
| **Giao diện (UI)** | Windows Forms (WinForms) | Kiến trúc Form MDI, giao diện phân hệ trực quan, dễ thao tác |
| **Truy cập CSDL** | ADO.NET & Entity Framework 6.5.1 | Phối hợp `SqlConnection`, `SqlDataAdapter`, `DataTable` và ORM EDMX |
| **Hệ quản trị CSDL**| Microsoft SQL Server | Thiết kế quan hệ chuẩn hóa 3NF, khóa ngoại toàn vẹn dữ liệu |

---

## 🗄️ 3. THIẾT KẾ CƠ SỞ DỮ LIỆU (RELATIONAL SCHEMA)

Database: `ChuongTrinh_QuanLyBenhNhan` bao gồm **10 bảng thực thể quan hệ chặt chẽ**:

1. **`BenhNhan`**: Thông tin hành chính bệnh nhân (`MaBN` PK, `HoTenBN`, `GioiTinhBN`, `TuoiBN`, `SDTBN`, `NgaySinh`, `DiaChiBN`, `MaBenh` FK).
2. **`ChiTietBenhNhan`**: Hồ sơ bệnh án từng lần khám (`MaCTBN` PK, `MaBN` FK, `MaNV` FK, `MaBenh` FK, `NgayKham`, `ChanDoan`, `KetQua`).
3. **`DonThuoc`**: Đơn thuốc chỉ định (`MaDT` PK, `MaBN` FK, `MaNV` FK, `NgayLap`, `TongTien`).
4. **`ChiTietDonThuoc`**: Dòng thuốc trong đơn (`MaDT` PK/FK, `MaThuoc` PK/FK, `SoLuong`, `HuongDanUong`, `NgayKhamBenh`, `NgayTaiKham`).
5. **`Thuoc`**: Kho dược phẩm (`MaThuoc` PK, `TenThuoc`, `DonViTinh`, `DonGia`, `CongDung`).
6. **`MacBenh`**: Danh mục nhóm bệnh lý chẩn đoán (`MaBenh` PK, `TenBenh`, `TrieuChung`).
7. **`Khoa`**: Phòng ban / Chuyên khoa y tế (`MaKhoa` PK, `TenKhoa`).
8. **`ChucVu`**: Chức danh cán bộ nhân viên (`MaCV` PK, `TenCV`).
9. **`NhanVien`**: Bác sĩ, dược sĩ, y tá (`MaNV` PK, `HoTenNV`, `GioiTinhNV`, `SDT`, `DiaChi`, `MaKhoa` FK, `MaCV` FK).
10. **`DangNhap`**: Phân quyền tài khoản bảo mật (`TaiKhoan` PK, `MatKhau`, `MaNV` FK, `Quyen`).

---

## ⚙️ 4. PHÂN HỆ NGHIỆP VỤ CỐT LÕI

* **Phân hệ Tiếp nhận & Hồ sơ Bệnh nhân:**
  - Tiếp nhận bệnh nhân mới, tự động sinh mã hoặc kiểm tra trùng lặp thông tin CCCD/SĐT.
  - Tra cứu nhanh tiền sử bệnh án và các đợt khám điều trị trước đó.
* **Phân hệ Khám bệnh & Chẩn đoán:**
  - Phân bổ bệnh nhân vào từng chuyên khoa khám cụ thể.
  - Ghi nhận triệu chứng lâm sàng, bác sĩ phụ trách đưa ra chẩn đoán và kết luận bệnh.
* **Phân hệ Kê đơn thuốc Điện tử:**
  - Lập đơn thuốc liên kết trực tiếp với kho dược phẩm.
  - Chọn tên thuốc từ ComboBox thông minh, tự động hiển thị đơn vị tính và đơn giá.
  - Nhập số lượng và hướng dẫn liều dùng (sáng/trưa/chiều/tối).
  - Tự động cộng dồn thành tiền và lên lịch hẹn ngày tái khám.
* **Phân hệ Quản lý Kho Dược & Nhân sự:**
  - Quản lý danh mục thuốc, quy cách đóng gói và điều chỉnh bảng giá viện phí.
  - Quản trị nhân viên y tế theo chức vụ và phòng khoa.

---

## 📂 5. CẤU TRÚC THƯ MỤC DỰ ÁN

```text
DoAnNet/
├── Chương trình quản lý bệnh nhân (.NET).docx   # Báo cáo đồ án chi tiết (Word)
├── DoAnNet/
│   ├── packages/                                  # Thư viện NuGet (EntityFramework 6.5.1)
│   └── QuanLyBenhNhan/
│       ├── QuanLyBenhNhan.sln                     # File giải pháp Visual Studio
│       └── QuanLyBenhNhan/
│           ├── CSDL/
│           │   └── DOANCSDL.sql                   # Kịch bản khởi tạo CSDL SQL Server đầy đủ
│           ├── App.config                         # Chuỗi kết nối ConnectionStrings
│           ├── Program.cs                         # Điểm khởi chạy ứng dụng (Main Entry Point)
│           ├── Functions.cs                       # Helper kết nối DB và xử lý ADO.NET tập trung
│           ├── frmMain.cs                         # Form chính điều hướng (Dashboard MDI)
│           ├── frmDMBenhNhan.cs                   # Form quản lý bệnh nhân
│           ├── frmChiTietBenhNhan.cs              # Form chi tiết bệnh án & khám bệnh
│           ├── frmDMDonThuoc.cs                   # Form lập và tra cứu đơn thuốc
│           ├── frmChiTietDonThuoc.cs              # Form chi tiết dòng thuốc và hướng dẫn uống
│           ├── frmDMThuoc.cs                      # Form danh mục kho thuốc
│           ├── frmDMNhanVien.cs                   # Form quản lý nhân sự y tế
│           ├── frmDMKhoa.cs                       # Form quản lý chuyên khoa
│           ├── frmDMChucVu.cs                     # Form quản lý chức vụ
│           └── frmDMMacBenh.cs                    # Form danh mục mã bệnh
└── README.md
```

---

## 🚀 6. HƯỚNG DẪN CÀI ĐẶT & CHẠY LOCAL

### Yêu cầu hệ thống:
* **Hệ điều hành:** Windows 10 / 11.
* **Môi trường phát triển:** Visual Studio 2019 hoặc Visual Studio 2022 (cài đặt workload *.NET desktop development*).
* **Cơ sở dữ liệu:** Microsoft SQL Server (bản Express hoặc Developer) + SQL Server Management Studio (SSMS).

### Các bước cài đặt:
1. **Clone mã nguồn về máy:**
   ```bash
   git clone https://github.com/NguyenHoangUy1305/DoAn_Net_NhomDoAn_5_DH24TH3_NhomTH2_To1.git
   ```
2. **Khởi tạo Cơ sở dữ liệu:**
   - Mở SSMS và kết nối vào SQL Server cục bộ.
   - Mở file `DoAnNet/QuanLyBenhNhan/QuanLyBenhNhan/CSDL/DOANCSDL.sql`.
   - Bấm **Execute (F5)** để tự động tạo Database `ChuongTrinh_QuanLyBenhNhan` và toàn bộ 10 bảng dữ liệu mẫu.
3. **Cấu hình chuỗi kết nối:**
   - Mở file `Functions.cs` và `App.config`, kiểm tra lại tên Server của bạn:
     ```csharp
     string connectionString = @"Data Source=.\SQLEXPRESS;Initial Catalog=ChuongTrinh_QuanLyBenhNhan;Integrated Security=True";
     ```
4. **Khởi chạy ứng dụng:**
   - Mở `QuanLyBenhNhan.sln` bằng Visual Studio.
   - Bấm **F5** hoặc chọn **Start Debugging** để khởi chạy chương trình.

---

## 👨‍💻 7. NHÓM TÁC GIẢ
* **Nguyễn Hoàng Uy** – *Full-stack Windows Forms & CSDL* – [`NguyenHoangUy1305`](https://github.com/NguyenHoangUy1305)
* **Tạ Nguyễn Thành Tín** – *Thiết kế Giao diện & Nghiệp vụ Bệnh án* – [`Thanh-Tin`](https://github.com/Thanh-Tin)

*Khoa Công nghệ Thông tin – Trường Đại học An Giang (ĐHQG TP.HCM)*
