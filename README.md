# Commit 1 Reflection Notes
Di bagian ini itu intinya aku udh mulai bikin web server sederhana pakai Rust, yg awalnya cuma nerima koneksi, sekarang udah bisa baca request dari client.

Disini yg aku pelajari itu salah satunya adalah fungsi handle_connection. Jadi setiap ada client yg connect ke server, koneksinya bakal dikirim ke function ini buat diproses. Di dalam function ini, aku pakai BufReader gitu buat baca data dari TcpStream. Tujuannya biar lebih gampang baca request dari client secara baris per baris.

Terus bagian ini:
```rust
.lines()
.map(|result| result.unwrap())
.take_while(|line| !line.is_empty())
.collect()
```

Awalnya emg agak bingung gitu, tapi setelah dipahami intinya itu:
- .lines() --> baca request per baris
- .map(|result| result.unwrap()) --> ambil isi dari setiap baris
- .take_while(|line| !line.is_empty()) --> berhenti baca kalau ketemu baris kosong (ini tanda akhir HTTP header)
- .collect() --> kumpulin semua baris jadi satu vector

Jadi intinya, program ini lagi baca HTTP request dari browser, tapi baru sampai tahap ditampilin aja ke terminal.

Dari sini aku jadi paham kalau:

HTTP request itu ternyata bentuknya text biasa
Ada struktur header yang dipisah baris kosong
Server itu kerjanya nunggu request terus-menerus (looping)

Menurut aku bagian ini penting banget karena ini dasar buat nanti bikin web server yang beneran bisa ngasih response ke client.