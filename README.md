# KELOMPOK 5 P2 - APPRISE
  - Hasan Fadilah (G6401231051)
  - Hannan Azhari Batubara (G6401231052)
  - Cokorda Gede Satria Widnyana Putra (G6401231064)
  - Jofattan Faiz Betryan (G6401231066)
  - Jordan Vieno Simamora (G6401231135)
  
![Tampilan Screenshot Aplikasi](https://raw.githubusercontent.com/hasanfadils/KDJK5-K2/refs/heads/main/Screenshoot/Apprise%20Logo.png)
[Sekilas Tentang](#sekilas-tentang) | [Instalasi&Setup](#instalasi--setup) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)

## Sekilas Tentang

**Apprise** adalah sebuah library dan command line tool (CLI) untuk mengirimkan notifikasi ke hampir semua layanan notifikasi populer, seperti Telegram, Discord, Slack, Amazon SNS, Gotify, Email (SMTP/Gmail), dan lainnya.
Tujuan utamanya adalah memberikan satu cara yang sederhana, ringan, dan seragam untuk mengirim notifikasi tanpa perlu menulis integrasi untuk setiap layanan satu per satu.


**Prasyarat**  
  - Python (versi terbaru disarankan, ≥ 3.7)  
  - pip (package manager Python)  

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

Fitur Utama:
- One-to-Many Fan-Out (sekali kirim → banyak kanal) 
Satu aksi mengirim ke beberapa layanan sekaligus (Discord, Email/SMTP, Telegram, dll).

Impact: Reliabilitas naik (redundansi kanal) & hemat waktu integrasi — pesan lebih pasti terbaca.

- Unified URL Schema + Dukungan Banyak Layanan
Semua target ditulis sebagai Apprise URL (discord://…, mailto(s)://…, tgram://…)—tanpa perlu SDK khusus tiap platform.

Impact: Kurva belajar rendah & biaya integrasi turun drastis; ganti/ tambah kanal cukup ubah URL.

- Format Konten: Text / Markdown / HTML
Tentukan cara render pesan.

Manfaat: Fleksibel—bisa plain text, basic formatting, atau HTML bila layanan mendukung.

- Tag & Filter Target
Tambahkan ?tag=... pada URL (mis. chat, mail) lalu pilih tag saat mengirim.

Manfaat: Kirim ke subset penerima tanpa mengubah YAML.


## Konfigurasi 
Beberapa konfigurasi yang dapat dilakukan:
- Menambahkan URL notifikasi (Telegram, Slack, Discord, dsb.) ke dalam skrip konfigurasi.
- Mengatur syntax notifikasi yang umum dan intuitif.
- Mengaktifkan dukungan gambar dan attachment (jika layanan mendukung).
Plugin tambahan (misalnya integrasi login pihak ketiga) tidak diperlukan, karena Apprise sudah support multi-platform notification secara native.


##  Maintenance

Tidak ada konfigurasi maintenance yang rumit.
Namun, untuk sistem server:
- Bisa menambahkan cron job untuk otomatisasi backup notifikasi log.
- Monitoring performa karena Apprise mengirim pesan secara asynchronous.

## Otomatisasi

Contoh script shell untuk instalasi dan mengirim notifikasi otomatis:
 ```bash
 #!/bin/bash
pip install apprise
apprise -t "Judul Pesan" -b "Isi notifikasi" "discord://token/..."
apprise -t "Hello via Email" -b "Ini pesan lewat Gmail" "mailto://user@gmail.com:password@smtp.gmail.com"
```

## Cara Pemakaian

Tampilan aplikasi: berbasis CLI, tidak memiliki GUI bawaan.
Fungsi utama:
- Mengirim notifikasi teks ke berbagai layanan (Telegram, Slack, Discord, Email/Gmail, dll).
- Mendukung attachment (gambar/file) jika layanan memungkinkan.
- Pesan dikirim secara asynchronous → respon cepat.
 ```bash
  apprise -t "Hello" -b "Ini pesan dari Apprise" "tgram://TOKEN/CHAT_ID"
apprise -t "Notifikasi Email" -b "Pesan lewat Gmail" "mailto://user@gmail.com:password@smtp.gmail.com"
```


## Pembahasan

**Kelebihan :**
- Satu library untuk hampir semua layanan notifikasi.
- Lightweight dan cepat.
- Syntax seragam dan intuitif.
- Mendukung attachment (gambar/file).
- Support banyak platform termasuk Email/Gmail.
  
**Kekurangan :**
- Tidak ada GUI bawaan (hanya CLI dan library).
- Fungsi terbatas hanya untuk notifikasi, bukan aplikasi chatting penuh.
- Bergantung pada API layanan pihak ketiga (jika berubah, perlu update).
  
**Perbandingan :**
- Dibanding coding manual API Telegram/Slack/SMTP, Apprise jauh lebih ringkas.
- Dibanding Pushover atau Firebase, Apprise lebih fleksibel (multi-platform), tapi mungkin tidak selengkap fitur native platform tertentu.


## Referensi
- Dokumentasi resmi: https://github.com/caronc/apprise
