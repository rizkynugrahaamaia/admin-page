Admin Page untuk Manajemen Pembelian
Aplikasi ini adalah halaman admin sederhana yang dirancang untuk mengelola pembelian produk dan stok. Admin dapat melihat daftar produk, menambah pembelian baru, membatalkan pembelian, serta melacak jumlah stok. Aplikasi ini dibangun menggunakan Node.js, Express.js, MySQL, dan EJS untuk templating.




Prasyarat
Sebelum memulai, pastikan Anda telah menginstal:

Node.js (versi 14 atau lebih tinggi)
MySQL (versi 5.7 atau lebih tinggi)
Editor kode (contoh: VS Code)
Git (opsional, untuk mengkloning repositori)


Setup Database

Jalankan MySQL: Pastikan server MySQL Anda aktif.
Buat Database: Buka klien MySQL (misalnya MySQL Workbench atau baris perintah) dan jalankan perintah berikut untuk membuat database dan tabel:

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

Ini akan membuat database toko_db dengan tiga tabel: Produk, Stock_produk, dan Pembelian, beserta data produk awal.

sesuaikan mysql dengan setup anda yang terdapat pada app.js

     // Replace with your MySQL 
    host: 'localhost',
    user: 'root',
    password: '', 
    database: 'toko_db'