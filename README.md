# KELOMPOK 5 P2 - APPRISE
  - Hasan Fadilah (G6401231051)
  - Hannan Azhari Batubara (G6401231052)
  - Cokorda Gede Satria Widnyana Putra (G6401231064)
  - Jofattan Faiz Betryan (G6401231066)
  - Jordan Vieno Simamora (G6401231135)
  
![Tampilan Screenshot Aplikasi](https://raw.githubusercontent.com/hasanfadils/KDJK5-K2/refs/heads/main/Screenshoot/Apprise%20Logo.png)
[Sekilas Tentang](#sekilas-tentang) | [Instalasi&Setup](#instalasi--setup) | [Otomatisasi](#otomatisasi) | [Pembahasan](#pembahasan) | [Referensi](#referensi)

## Sekilas Tentang

**Apprise** adalah sebuah library dan command line tool (CLI) untuk mengirimkan notifikasi ke hampir semua layanan notifikasi populer, seperti Telegram, Discord, Slack, Amazon SNS, Gotify, Email (SMTP/Gmail), dan lainnya.
Tujuan utamanya adalah memberikan satu cara yang sederhana, ringan, dan seragam untuk mengirim notifikasi tanpa perlu menulis integrasi untuk setiap layanan satu per satu.

**Prasyarat**  
  - Python (versi terbaru disarankan, ≥ 3.7)  
  - pip (package manager Python)
    
**Fitur Utama:**
- One-to-Many Fan-Out (sekali kirim → banyak kanal) 
Satu aksi mengirim ke beberapa layanan sekaligus (Discord, Email/SMTP, Telegram, dll).
- Unified URL Schema + Dukungan Banyak Layanan
Semua target ditulis sebagai Apprise URL (discord://…, mailto(s)://…, tgram://…)—tanpa perlu SDK khusus tiap platform.
- Format Konten: Text / Markdown / HTML
Tentukan cara render pesan.
- Tag & Filter Target
Tambahkan ?tag=... pada URL (mis. chat, mail) lalu pilih tag saat mengirim



## Instalasi & Setup
**Instalasi**
- Membuat virtual environment dengan python 3.12
   
```bash
py -3.12 -m venv .venv
```

- Virtual Environment
   
```bash
.\.venv\Scripts\Activate.ps1
```

- Git clone 

digunakan untuk melakukan unduh sumber kode
git clone https://github.com/caronc/apprise-api.git
cd apprise-api

- Install dev

Lakukan langkah ini untuk memasang proyek dari folder saat ini ke venv dalam mode editable sekaligus menginstal paket ekstra “dev”, sehingga semua dependensi terpenuhi dan setiap perubahan kode langsung terbaca saat menjalankan Apprise API

```bash
pip install -e ".[dev]"
```

- Run server

Jalankan server di alamat http://127.0.0.1:8000/

```bash
python manage.py runserver
```

**Set Up**
-  Ctrl+Click http://127.0.0.1:8000/ untuk membuka Apprise API – Configuration Manager di browser.
  
 ![1](https://github.com/hasanfadils/KDJK5-K2/blob/93bcefe6ade6031f54ef63215ce6b7f771e7940b/Screenshoot/1.png)

- Buat Konfigurasi
  
![1](https://github.com/hasanfadils/KDJK5-K2/blob/9249ab64ab23c0af87e6004fbef0358dace28457/Screenshoot/2.png)
Configuration Manager → Configuration → YAML → Save
Menyimpan daftar target notifikasi di server dengan sebuah key.

- Isi YAML contoh (Discord + Email)
  
![1](https://github.com/hasanfadils/KDJK5-K2/blob/9249ab64ab23c0af87e6004fbef0358dace28457/Screenshoot/3.png)
Keterangan singkat: user%40domain.tld = encode @; 587 = mailto://…?mode=starttls; 465 = mailtos://… (tanpa mode=starttls); tag= untuk filter tujuan

Contoh urls:
  - "discord://1423711671544713310/ePj3SgU9kJk5ZrWICZXFjv7aN9-YHh1TSHjaqoqtvhd7XZEqSPn7wh5nEWQ-TN50Q7xu?tag=chat"
  - "mailto://cokgdsatria%40apps.ipb.ac.id:APP_PASSWORD_16@smtp.gmail.com:587/?mode=starttls&from=cokgdsatria@apps.ipb.ac.id&to=hasanfadilah@apps.ipb.ac.id,coksatria2005@gmail.com,jordanvienosimamora@gmail.com,hannanbatubara@apps.ipb.ac.id&tag=mail"
    
- Kirim dari GUI
  
![1](https://github.com/hasanfadils/KDJK5-K2/blob/9249ab64ab23c0af87e6004fbef0358dace28457/Screenshoot/4.png)
Notifications → Process As (Text/Markdown/HTML) → Title (opsional) → Body (wajib) → Tag (opsional) → Send Notification

- Notifikasi berhasil dikirim
  
![1](https://github.com/hasanfadils/KDJK5-K2/blob/9249ab64ab23c0af87e6004fbef0358dace28457/Screenshoot/5.png)


##  Maintenance

Tidak ada konfigurasi maintenance yang rumit.
Namun, untuk sistem server:
- Bisa menambahkan cron job untuk otomatisasi backup notifikasi log.
- Monitoring performa karena Apprise mengirim pesan secara asynchronous.

## Otomatisasi

Apprise API sangat ideal untuk otomatisasi melalui panggilan API (HTTP Request) ke alamat server.

Skrip Shell/Aplikasi untuk Mengirim Notifikasi:

Setelah konfigurasi (dengan Config ID) disimpan, Anda dapat mengintegrasikannya ke dalam skrip shell atau aplikasi Anda dengan memanggil endpoint notifikasi dan menyertakan Config ID dan tag yang relevan.

Contoh Panggilan API (Konseptual): Mengirim notifikasi ke semua layanan dengan tag chat (yaitu Discord dari konfigurasi di atas).
 ```bash
 # Contoh menggunakan cURL untuk POST request ke Apprise API
# (Ganti [CONFIG_ID] dengan ID yang tersimpan)
CONFIG_ID="5432c9ff@fa23935bb5acb906420698e6f712651844596aeb7c9a8684c3700e9"

curl -X POST http://127.0.0.1:8000/notify/${CONFIG_ID} \
     -H "Content-Type: application/json" \
     -d '{
           "title": "Peringatan Server",
           "body": "Memori kritis 90%. Segera periksa!",
           "tag": "chat" 
         }'
```



## Pembahasan

**Kelebihan :**
- Kurva Belajar Rendah: Berkat Unified URL Schema, pengembang tidak perlu mempelajari API yang berbeda-beda.
- Sangat Fleksibel: Kemampuan One-to-Many Fan-Out dan dukungan format Text/Markdown/HTML menjadikannya solusi notifikasi yang serbaguna.
- Efisiensi dan Reliabilitas: Menghemat waktu integrasi dan meningkatkan kepastian pesan terbaca melalui redundansi kanal.
- Fitur Tagging: Fitur Tag & Filter Target memungkinkan kontrol yang sangat baik atas siapa yang menerima pesan tanpa mengubah konfigurasi dasar.
  
**Kekurangan :**
- Lingkungan Development: Aplikasi ini berjalan di atas development server (Django) dan diperingatkan keras untuk tidak digunakan dalam pengaturan produksi tanpa server WSGI/ASGI.
- Ketergantungan Python/Django: Memerlukan pemahaman dasar tentang Python, venv, dan Django untuk instalasi dan deployment.
- Kerumitan URL: Meskipun seragam, URL untuk layanan kompleks (seperti SMTP/Email) bisa sangat panjang dan harus menyertakan detail encoding (%40 untuk @).
  
**Perbandingan :**
Apprise API menawarkan fleksibilitas terbesar dan biaya operasional terendah untuk manajemen notifikasi yang melibatkan puluhan kanal dari satu titik sentral, dengan syarat pengguna siap untuk melakukan self-hosting yang aman.

## Referensi
- Dokumentasi resmi: https://github.com/caronc/apprise
