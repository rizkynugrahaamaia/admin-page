# Admin Page untuk Manajemen Pembelian
Aplikasi ini adalah halaman admin sederhana yang dirancang untuk mengelola pembelian produk dan stok. Admin dapat melihat daftar produk, menambah pembelian baru, membatalkan pembelian, serta melacak jumlah stok. Aplikasi ini dibangun menggunakan Node.js, Express.js, MySQL, dan EJS untuk templating.

## Prasyarat

Sebelum memulai, pastikan Anda telah menginstal:

Node.js (versi 14 atau lebih tinggi)
MySQL (versi 5.7 atau lebih tinggi)
Editor kode (contoh: VS Code)
Git (opsional, untuk mengkloning repositori)

## Setup Database

Jalankan MySQL: Pastikan server MySQL Anda aktif.
Buat Database: Buka klien MySQL (misalnya MySQL Workbench atau baris perintah) dan jalankan perintah berikut untuk membuat database dan tabel:

```bash
CREATE DATABASE toko_db;
USE toko_db;

CREATE TABLE Produk (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(255),
    price DECIMAL(10,2)
);

INSERT INTO Produk (product_name, price) VALUES
('Laptop', 1000.00),
('Mouse', 20.00),
('Keyboard', 50.00),
('Monitor', 150.00),
('Printer', 200.00),
('Headphones', 30.00),
('Webcam', 40.00),
('Speaker', 60.00),
('Router', 80.00),
('External HDD', 120.00);

CREATE TABLE Stock_produk (
    product_id INT PRIMARY KEY,
    quantity INT,
    FOREIGN KEY (product_id) REFERENCES Produk(product_id)
);

INSERT INTO Stock_produk (product_id, quantity)
SELECT product_id, 0 FROM Produk;

CREATE TABLE Pembelian (
    purchase_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT,
    quantity INT,
    purchase_date DATETIME,
    status VARCHAR(20),
    FOREIGN KEY (product_id) REFERENCES Produk(product_id)
);
```
Ini akan membuat database toko_db dengan tiga tabel: Produk, Stock produk, dan Pembelian, beserta data produk awal.

## Konfigurasi

1. **Koneksi Database**
sesuaikan host, user, password dengan yang anda miliki, terdapat pada app.js
```bash
    // Replace with your MySQL 
    const connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: 'kata_sandi_anda',  // Ganti dengan kata sandi MySQL Anda
    database: 'toko_db'
});
```
2. **Pastikan MySQL Berjalan**
Verifikasi bahwa server MySQL aktif dan database toko_db dapat diakses.

## Instalasi

1. **Kloning Repositori**

   ```bash
   git clone https://github.com/yourusername/admin-page.git
   cd admin-page
   ```

2. **install Dependensi**

   ```bash
   npm install
   ```

## Menjalankan Aplikasi

1. **Jalankan Server**

   ```bash
   node app.js
   ```

2. **Buka browser untuk akses halaman**

   Navigate to [http://localhost:3000](http://localhost:3000/purchases) to see the admin page in action.
