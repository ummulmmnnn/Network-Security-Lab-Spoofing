# Laporan Praktikum: Keamanan Jaringan (Session Hijacking & IP Spoofing)

Repositori ini berisi dokumentasi dan hasil pengamatan praktikum mengenai kerentanan protokol tidak terenkripsi serta simulasi berbagai serangan Denial of Service (DoS) menggunakan teknik IP Spoofing.

## 1. Kesimpulan Hasil Praktikum
Praktikum ini membuktikan bahwa protokol seperti HTTP dan Telnet memiliki risiko keamanan fatal karena tidak adanya enkripsi. Melalui teknik *ARP Spoofing*, penyerang berhasil melakukan *Man-in-the-Middle* (MITM) untuk menyadap lalu lintas data dan mencuri kredensial dalam bentuk *plain text*. Selain itu, simulasi serangan DoS menunjukkan bahwa tanpa sistem validasi paket yang kuat, infrastruktur jaringan sangat mudah dilumpuhkan.

## 2. Perbedaan Metode IP Spoofing
Berdasarkan hasil pengamatan, setiap metode memiliki mekanisme unik dalam mengeksploitasi target:
* **Ping of Death (PoD):** Mengirimkan paket ICMP abnormal (65.000 byte) untuk melampaui kapasitas memori target saat penyusunan kembali fragmen.
* **SYN Flood:** Membanjiri port target dengan permintaan koneksi TCP SYN palsu untuk menjenuhkan antrean layanan server.
* **Teardrop:** Memanipulasi nilai *offset* fragmen agar tumpang tindih (*overlap*), memicu kegagalan sistem pada proses *reassembly*.
* **Land Attack:** Menyamakan alamat IP asal dan tujuan untuk menjebak sistem target dalam perulangan balasan tanpa akhir (*infinite loop*).

## 3. Analisis Transport Layer
Tipe *transport layer* utama yang digunakan adalah **TCP (Transmission Control Protocol)**.
* **Alasan:** Karakteristik TCP yang berbasis koneksi (*connection-oriented*) memungkinkan eksploitasi pada mekanisme *handshake* atau port layanan tertentu (seperti Telnet/NetBIOS). Penyerang memalsukan identitas pada lapisan ini untuk memaksa target mengalokasikan sumber daya secara ilegal.

## 4. Metode Pencegahan
* **ARP Spoofing:** Penerapan *Static ARP Entries* atau fitur *Dynamic ARP Inspection* (DAI) pada perangkat switch.
* **IP Spoofing:** Penggunaan *Ingress/Egress Filtering*, *Unicast Reverse Path Forwarding* (uRPF), serta migrasi ke protokol terenkripsi seperti **SSH** dan **HTTPS**.
