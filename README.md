# SQl_homework
bài tập sql sever
-- Bảng SinhVien
CREATE TABLE SinhVien (
    MaSV CHAR(10) PRIMARY KEY,
    HoTen NVARCHAR(50),
    NgaySinh DATE,
    GioiTinh BIT,  -- 1: Nam, 0: Nữ
    DiaChi NVARCHAR(100),
    MaLop CHAR(10) -- FK tham chiếu Lop
);

-- Bảng Lop
CREATE TABLE Lop (
    MaLop CHAR(10) PRIMARY KEY,
    TenLop NVARCHAR(50),
    MaGVCN CHAR(10) -- FK tham chiếu GVCN
);

-- Bảng GVCN (Giáo viên chủ nhiệm)
CREATE TABLE GVCN (
    MaGVCN CHAR(10) PRIMARY KEY,
    HoTen NVARCHAR(50),
    SoDienThoai VARCHAR(15)
);

-- Bảng LopSV (Quan hệ giữa SinhVien và Lop)
CREATE TABLE LopSV (
    MaLop CHAR(10),
    MaSV CHAR(10),
    PRIMARY KEY (MaLop, MaSV),
    FOREIGN KEY (MaLop) REFERENCES Lop(MaLop),
    FOREIGN KEY (MaSV) REFERENCES SinhVien(MaSV)
);

-- Bảng GiaoVien
CREATE TABLE GiaoVien (
    MaGV CHAR(10) PRIMARY KEY,
    HoTen NVARCHAR(50),
    MaBoMon CHAR(10) -- FK tham chiếu BoMon
);

-- Bảng BoMon (Bộ môn)
CREATE TABLE BoMon (
    MaBoMon CHAR(10) PRIMARY KEY,
    TenBoMon NVARCHAR(50),
    MaKhoa CHAR(10) -- FK tham chiếu Khoa
);

-- Bảng Khoa
CREATE TABLE Khoa (
    MaKhoa CHAR(10) PRIMARY KEY,
    TenKhoa NVARCHAR(50)
);

-- Bảng MonHoc
CREATE TABLE MonHoc (
    MaMH CHAR(10) PRIMARY KEY,
    TenMH NVARCHAR(50),
    SoTinChi INT
);

-- Bảng LopHP (Lớp học phần)
CREATE TABLE LopHP (
    MaLopHP CHAR(10) PRIMARY KEY,
    MaMH CHAR(10), -- FK tham chiếu MonHoc
    MaGV CHAR(10), -- FK tham chiếu GiaoVien
    FOREIGN KEY (MaMH) REFERENCES MonHoc(MaMH),
    FOREIGN KEY (MaGV) REFERENCES GiaoVien(MaGV)
);

-- Bảng DKMH (Đăng ký môn học)
CREATE TABLE DKMH (
    MaSV CHAR(10),
    MaLopHP CHAR(10),
    Diem FLOAT CHECK (Diem >= 0 AND Diem <= 10),
    PRIMARY KEY (MaSV, MaLopHP),
    FOREIGN KEY (MaSV) REFERENCES SinhVien(MaSV),
    FOREIGN KEY (MaLopHP) REFERENCES LopHP(MaLopHP)
);
