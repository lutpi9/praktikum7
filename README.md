# Tugas Praktikum { Pertemuan ke 15 } <img src=https://logos-download.com/wp-content/uploads/2016/05/MySQL_logo_logotype.png width="130px" >


|**Nama**|**NIM**|**Kelas**|**Matkul**|
|----|---|-----|------|
|Lutpiah Ainus Shiddik|312310474|TI.23.A.5|Basis Data|



## Soal Praktikum 7
<img width="550" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/0a3a0a03-fa11-4d2b-9786-67bff96c320c">

> **Keterangan** : Terdapat 5 tabel yang terdiri dari tabel Perusahaan, Departemen, Karyawan, Project dan Project Detail.

### *Script SQL berdasarkan Tabel Perusahaan*
```
sql
CREATE TABLE Perusahaan(
id_p VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
alamat VARCHAR(45) DEFAULT NULL
);

INSERT INTO Perusahaan (id_p, nama, alamat) VALUES
('P01', 'Kantor Pusat', NULL),
('P02', 'Cabang Bekasi', NULL);
SELECT * FROM Perusahaan;
```
## Output Tabel Perusahaan :
<img width="278" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/f9f2bc81-918f-4332-8d30-afc80c9ad586">



### *Script SQL berdasarkan Tabel Departemen*
```
sql
CREATE TABLE Departemen(
id_dept VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
id_p VARCHAR(10) NOT NULL,
manajer_nik VARCHAR(10) DEFAULT NULL
);

INSERT INTO Departemen (id_dept, nama, id_p, manajer_nik) VALUES
('D01', 'Produksi', 'P02', 'N01'),
('D02', 'Marketing', 'P01', 'N03'),
('D03', 'RnD', 'P02', NULL),
('D04', 'Logistik', 'P02', NULL);
SELECT * FROM Departemen;
```
## Output Tabel Departemen :
<img width="277" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/81fe9ca4-09cf-40fd-82aa-84a3cc7e24b7">



### *Script SQL berdasarkan Tabel Karyawan*
```
sql
CREATE TABLE Karyawan(
nik VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
id_dept VARCHAR(10) NOT NULL,
sup_nik VARCHAR(10) DEFAULT NULL,
gaji_pokok INT
);

INSERT INTO Karyawan (nik, nama, id_dept, sup_nik, gaji_pokok) VALUES
('N01', 'Ari', 'D01', NULL, 2000000),
('N02', 'Dina', 'D01', NULL, 2500000),
('N03', 'Rika', 'D03', NULL, 2400000),
('N04', 'Ratih', 'D01', 'N01', 3000000),
('N05', 'Riko', 'D01', 'N01', 2800000),
('N06', 'Dani', 'D02', NULL, 2100000),
('N07', 'Anis', 'D02', 'N06', 5000000),
('N08', 'Dika', 'D02', 'N06', 4000000),
('N09', 'Raka', 'D03', 'N06', 2000000);
SELECT * FROM Karyawan;
```
## Output Tabel Karyawan :
<img width="281" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/8fdd35ad-8046-4fc1-9e73-2c42f874a477">



### *Script SQL berdasarkan Tabel Project*
```
sql
CREATE TABLE Project(
id_proj VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
tgl_mulai DATETIME,
tgl_selesai DATETIME,
status TINYINT(1)
);

INSERT INTO Project (id_proj, nama, tgl_mulai, tgl_selesai, status) VALUES
('PJ01', 'A', '2019-01-10', '2019-03-10', '1'),
('PJ02', 'B', '2019-02-15', '2019-04-10', '1'),
('PJ03', 'C', '2019-03-21', '2019-05-10', '1');
SELECT * FROM Project;
```
## Output Tabel Project :
<img width="403" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/705f8983-915c-4222-b5a0-5c8b79593182">



### *Script SQL berdasarkan Tabel Project Detail*
```
sql
CREATE TABLE Project_detail(
id_proj VARCHAR(10) NOT NULL,
nik VARCHAR(10) NOT NULL
);

INSERT INTO Project_detail (id_proj, nik) VALUES
('PJ01', 'N01'),
('PJ01', 'N02'),
('PJ01', 'N03'),
('PJ01', 'N04'),
('PJ01', 'N05'),
('PJ01', 'N07'),
('PJ01', 'N08'),
('PJ02', 'N01'),
('PJ02', 'N03'),
('PJ02', 'N05'),
('PJ03', 'N03'),
('PJ03', 'N07'),
('PJ03', 'N08');
SELECT * FROM Project_detail;
```
## Output Tabel Project Detail :
<img width="295" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/bd7ca5e7-c381-4dd5-9930-68b7d886ee0d">





## Latihan Praktikum 7

## 1. Tampilkan data karyawan yang bekerja pada departemen yang sama dengan karyawan yang bernama Dika
*Script :*

```
sql
SELECT nik, nama, id_dept FROM Karyawan WHERE id_dept = (SELECT id_dept FROM Karyawan WHERE nama = 'Dika');
```

# *Outputnya :*

<img width="721" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/672e681b-67f3-4da4-80ce-f48d07db16ac">


## 2. Tampilkan data karyawan yang gajinya lebih besar dari rata-rata gaji semua karyawan. Urutkan menurun berdasarkan besaran gaji
*Script :*

```
sql
SELECT nik, nama, id_dept, gaji_pokok FROM karyawan WHERE gaji_pokok > (SELECT AVG(gaji_pokok) FROM Karyawan) ORDER BY gaji_pokok DESC;
```

# *Outputnya :*

<img width="880" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/cfe82f3c-6758-4b7d-8555-48d16133fa71">


## 3. Tampilkan nik dan nama karyawan untuk semua karyawan yang bekerja di departmen yang sama dengan karyawan dengan nama yang mengandung huruf 'K'.
*Script :*

```
sql
SELECT nik, nama FROM Karyawan WHERE id_dept IN (SELECT id_dept FROM Karyawan WHERE nama LIKE '%K%');
```

# *Outputnya :*

<img width="686" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/6d62f0c9-0ec3-4c9f-9f9f-df359b432548">


## 4. Tampilkan data karyawan yang bekerja pada departemen yang ada di Kantor pusat.
*Script :*

```
sql
SELECT karyawan.nik, karyawan.nama, karyawan.id_dept FROM karyawan JOIN departemen ON karyawan.id_dept = departemen.id_dept WHERE departemen.id_p = 'P01';
```

# *Outputnya :*

<img width="947" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/783b2c13-5493-46c3-b600-192a38d475be">


## 5. Tampilkan nik dan nama karyawan untuk semua karyawan yang bekerja di departmen yang sama dengan karyawan dengan nama yang mengandung huruf 'K' dan yang gajinya lebih besar dari rata-rata gaji semua karyawan
*Script :*

```
sql
SELECT DISTINCT k1.nik, k1.nama FROM karyawan k1 JOIN karyawan k2 ON k1.id_dept = k2.id_dept WHERE k1.gaji_pokok > (SELECT AVG(gaji_pokok) FROM karyawan WHERE nama LIKE '%K%');
```

# *Outputnya :*

<img width="948" alt="image" src="https://github.com/lutpi9/praktikum7/assets/147919251/71948442-de95-4407-92c8-09799fe66989">


## *SELESAI*
