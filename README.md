# Tutorial 10 (Broadcast Chat)

**Prasetyo Adi Wijonarko**<br>
**2206830246**<br>
**Pemrograman Lanjut A / DEE**<br>

## 2.1. Original code of broadcast chat
![alt text](/image/broadcast-1.jpg)

Saya menjalankan program dengan membuka 4 terminal. 1 terminl melakukan command `cargo run --bin server` dan sisanya dilakukan command `cargo run --bin client`. Terminal yang berperan sebagai client, dapat mengirim pesanan. Berdasarkan gambar diatas,  masing-masing dari client mengirimi pesan dan server akan menerima pesan dari masing-masing client dan mengirim kembali ke semua client. 

## 2.2. Modifying the websocket port
![alt text](/image/broadcast-2.jpg)
Berdasarkan kode pada `src/bin/server.rs` dan `src/bin/client.rs`, keduanya menggunakan protokol WebSocket yang sama yang dikelola oleh library `tokio_websockets`. Ini memastikan bahwa kedua sisi, baik client maupun server, dapat berkomunikasi dengan protokol yang konsisten dan terdefinisi dengan baik. Selain itu, foto-foto yang disajikan menunjukkan bahwa program masih berjalan dengan baik meskipun port yang digunakan sudah diubah menjadi 8080. Penggantian port dilakukan dengan mengubah nilai port di kedua file. Pada `client.rs`, port diubah dalam Uri ClientBuilder yang berfungsi sebagai builder koneksi WebSocket pada client, sedangkan pada `server.rs`, port diubah pada listener yang bertugas sebagai TCP listener koneksi. Perintah print juga menunjukkan bahwa port sudah berhasil diubah. Meskipun ada perubahan ini, program masih berjalan dengan normal.

## 2.3. Small changes. Add some information to client
![alt text](/image/broadcast-3.jpg)
Dalam `server.rs`, dilakukan perubahan pada format teks broadcast dengan menambahkan informasi IP dan port dari sender di setiap clientnya. Perubahan tersebut dilakukan dari `bcast_tx.send(text.into())?;` menjadi `bcast_tx.send(format!("{addr} : {text}"))?;`. Selain itu, keterangan "From Adi's Computer" juga ditambahkan untuk memperjelasnya.